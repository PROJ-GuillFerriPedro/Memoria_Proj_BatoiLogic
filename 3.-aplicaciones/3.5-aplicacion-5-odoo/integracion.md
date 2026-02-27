# Integracion

{% file src="../../.gitbook/assets/odooTests.yaml" %}

{% code expandable="true" %}
```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: "CloudFormation template para Odoo con VPC y RDS (sin IAM)"

Parameters:
  OdooInstanceType:
    Type: String
    Default: t3.micro
    Description: Tipo de instancia EC2 para Odoo

  DBInstanceClass:
    Type: String
    Default: db.t3.micro
    Description: Clase de la instancia RDS

  DBName:
    Type: String
    Default: odoo
    Description: Nombre de la base de datos

  DBUsername:
    Type: String
    Default: odoo
    Description: Usuario maestro de la base de datos

  DBPassword:
    Type: String
    Default: "57gg-kgyy-q3nn"
    NoEcho: true
    Description: Contraseña de la base de datos
    MinLength: 8

  KeyName:
    Type: AWS::EC2::KeyPair::KeyName
    Description: Nombre del key pair para acceder a la instancia EC2
    Default: "vockey"

  LatestAmiId:
    Type: AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>
    Default: /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2

Resources:
  # ========== VPC y Networking ==========
  VPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsHostnames: true
      EnableDnsSupport: true
      Tags:
        - Key: Name
          Value: OdooVPC

  PublicSubnetAZ1:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref VPC
      CidrBlock: 10.0.1.0/24
      AvailabilityZone: !Select [0, !GetAZs ""]
      MapPublicIpOnLaunch: true
      Tags:
        - Key: Name
          Value: PublicSubnet-AZ1

  PublicSubnetAZ2:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref VPC
      CidrBlock: 10.0.2.0/24
      AvailabilityZone: !Select [1, !GetAZs ""]
      MapPublicIpOnLaunch: true
      Tags:
        - Key: Name
          Value: PublicSubnet-AZ2

  PrivateSubnetAZ1:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref VPC
      CidrBlock: 10.0.11.0/24
      AvailabilityZone: !Select [0, !GetAZs ""]
      Tags:
        - Key: Name
          Value: PrivateSubnet-AZ1

  PrivateSubnetAZ2:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref VPC
      CidrBlock: 10.0.12.0/24
      AvailabilityZone: !Select [1, !GetAZs ""]
      Tags:
        - Key: Name
          Value: PrivateSubnet-AZ2

  InternetGateway:
    Type: AWS::EC2::InternetGateway
    Properties:
      Tags:
        - Key: Name
          Value: OdooIGW

  AttachGateway:
    Type: AWS::EC2::VPCGatewayAttachment
    Properties:
      VpcId: !Ref VPC
      InternetGatewayId: !Ref InternetGateway

  PublicRouteTable:
    Type: AWS::EC2::RouteTable
    Properties:
      VpcId: !Ref VPC
      Tags:
        - Key: Name
          Value: Public-RT

  PublicRoute:
    Type: AWS::EC2::Route
    DependsOn: AttachGateway
    Properties:
      RouteTableId: !Ref PublicRouteTable
      DestinationCidrBlock: 0.0.0.0/0
      GatewayId: !Ref InternetGateway

  PublicSubnetRouteTableAssociation1:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      SubnetId: !Ref PublicSubnetAZ1
      RouteTableId: !Ref PublicRouteTable

  PublicSubnetRouteTableAssociation2:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      SubnetId: !Ref PublicSubnetAZ2
      RouteTableId: !Ref PublicRouteTable

  # NAT Gateway (solo 1 para ahorrar costos)
  NATGatewayEIP:
    Type: AWS::EC2::EIP
    DependsOn: AttachGateway
    Properties:
      Domain: vpc
      Tags:
        - Key: Name
          Value: NAT-EIP

  NATGateway:
    Type: AWS::EC2::NatGateway
    Properties:
      AllocationId: !GetAtt NATGatewayEIP.AllocationId
      SubnetId: !Ref PublicSubnetAZ1
      Tags:
        - Key: Name
          Value: NAT-Gateway

  PrivateRouteTable:
    Type: AWS::EC2::RouteTable
    Properties:
      VpcId: !Ref VPC
      Tags:
        - Key: Name
          Value: Private-RT

  PrivateRoute:
    Type: AWS::EC2::Route
    Properties:
      RouteTableId: !Ref PrivateRouteTable
      DestinationCidrBlock: 0.0.0.0/0
      NatGatewayId: !Ref NATGateway

  PrivateSubnetRouteTableAssociation1:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      SubnetId: !Ref PrivateSubnetAZ1
      RouteTableId: !Ref PrivateRouteTable

  PrivateSubnetRouteTableAssociation2:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      SubnetId: !Ref PrivateSubnetAZ2
      RouteTableId: !Ref PrivateRouteTable

  # ========== Security Groups ==========
  OdooSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Security group para Odoo
      VpcId: !Ref VPC
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 8069
          ToPort: 8069
          CidrIp: 0.0.0.0/0
      Tags:
        - Key: Name
          Value: Odoo-SG

  RDSSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Security group para RDS PostgreSQL
      VpcId: !Ref VPC
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 5432
          ToPort: 5432
          SourceSecurityGroupId: !Ref OdooSecurityGroup
      Tags:
        - Key: Name
          Value: RDS-SG

  # ========== RDS PostgreSQL ==========
  DBSubnetGroup:
    Type: AWS::RDS::DBSubnetGroup
    Properties:
      DBSubnetGroupDescription: Subnet group para RDS
      SubnetIds:
        - !Ref PrivateSubnetAZ1
        - !Ref PrivateSubnetAZ2
      Tags:
        - Key: Name
          Value: db-subnet-group

  RDSDatabase:
    Type: AWS::RDS::DBInstance
    DeletionPolicy: Snapshot
    Properties:
      DBInstanceIdentifier: odoo-postgres-db
      Engine: postgres
      EngineVersion: "15.12"
      DBInstanceClass: !Ref DBInstanceClass
      AllocatedStorage: "20"
      StorageType: gp3
      MasterUsername: !Ref DBUsername
      MasterUserPassword: !Ref DBPassword
      DBName: !Ref DBName
      DBSubnetGroupName: !Ref DBSubnetGroup
      VPCSecurityGroups:
        - !Ref RDSSecurityGroup
      MultiAZ: false
      BackupRetentionPeriod: 0
      PubliclyAccessible: true
      Tags:
        - Key: Name
          Value: OdooDatabase

  # ========== EC2 Odoo ==========
  OdooInstance:
    Type: AWS::EC2::Instance
    DependsOn: RDSDatabase
    Properties:
      ImageId: !Sub "{{resolve:ssm:/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2}}"
      InstanceType: !Ref OdooInstanceType
      KeyName: !Ref KeyName
      SubnetId: !Ref PublicSubnetAZ1
      SecurityGroupIds:
        - !Ref OdooSecurityGroup
      UserData:
        Fn::Base64: !Sub |
          #!/bin/bash -ex
          exec > >(tee /var/log/user-data.log|logger -t user-data -s 2>/dev/console) 2>&1

          # Update system
          yum update -y
          yum install -y git python3-pip python3-devel postgresql-devel gcc openldap-devel python3-wheel

          # Create odoo user
          useradd -m -d /opt/odoo -s /bin/bash odoo

          # Clone Odoo
          cd /opt/odoo
          git clone https://github.com/odoo/odoo.git --depth 1 --branch 15.0 /opt/odoo/odoo-server

          # FIX: Upgrade pip and force install dependencies
          pip3 install --upgrade pip
          pip3 install wheel

          # CRITICAL FIX: Ignore installed packages to avoid docutils conflict
          pip3 install --ignore-installed -r /opt/odoo/odoo-server/requirements.txt
          pip3 install psycopg2-binary python-ldap PyPDF2

          # Wait for RDS
          echo "Esperando a RDS..."
          sleep 90

          # Test connection
          export PGPASSWORD="${DBPassword}"
          for i in {1..30}; do
            if psql -h ${RDSDatabase.Endpoint.Address} -U ${DBUsername} -d postgres -c "SELECT 1" >/dev/null 2>&1; then
              echo "Conexión exitosa a RDS"
              break
            fi
            echo "Esperando a RDS... intento $i"
            sleep 10
          done

          # Create directories
          mkdir -p /etc/odoo /var/log/odoo /opt/odoo/custom-addons /opt/odoo/data

          # Create config
          cat > /etc/odoo/odoo.conf <<EOF
          [options]
          admin_passwd = admin
          db_host = ${RDSDatabase.Endpoint.Address}
          db_port = 5432
          db_user = ${DBUsername}
          db_password = ${DBPassword}
          db_name = ${DBName}
          addons_path = /opt/odoo/odoo-server/addons,/opt/odoo/custom-addons
          data_dir = /opt/odoo/data
          logfile = /var/log/odoo/odoo.log
          log_level = info
          workers = 4
          xmlrpc_port = 8069
          EOF

          # Set permissions
          chown -R odoo:odoo /opt/odoo /var/log/odoo /etc/odoo
          chmod 755 /var/log/odoo

          # Initialize database
          cd /opt/odoo/odoo-server
          sudo -u odoo ./odoo-bin -c /etc/odoo/odoo.conf -d ${DBName} -i base --without-demo=all --stop-after-init || true

          # Create systemd service
          cat > /etc/systemd/system/odoo.service <<EOF
          [Unit]
          Description=Odoo
          After=network.target

          [Service]
          Type=simple
          User=odoo
          Group=odoo
          ExecStart=/opt/odoo/odoo-server/odoo-bin -c /etc/odoo/odoo.conf
          Restart=on-failure
          RestartSec=10
          StandardOutput=journal
          StandardError=journal
          LimitNOFILE=65536

          [Install]
          WantedBy=multi-user.target
          EOF

          systemctl daemon-reload
          systemctl enable odoo.service
          systemctl start odoo.service

          echo "Instalación completada. Odoo en puerto 8069"

      Tags:
        - Key: Name
          Value: Odoo-Instance

Outputs:
  OdooURL:
    Description: URL para acceder a Odoo
    Value: !Sub "http://${OdooInstance.PublicIp}:8069"

  OdooPublicIP:
    Description: IP pública de la instancia Odoo
    Value: !GetAtt OdooInstance.PublicIp

  OdooSSHCommand:
    Description: Comando SSH para acceder a Odoo
    Value: !Sub "ssh -i ${KeyName}.pem ec2-user@${OdooInstance.PublicIp}"

  RDSEndpoint:
    Description: Endpoint de la base de datos RDS
    Value: !GetAtt RDSDatabase.Endpoint.Address

  CheckOdooScript:
    Description: Script para verificar el estado de Odoo (ejecutar via SSH)
    Value: !Sub "ssh -i ${KeyName}.pem ec2-user@${OdooInstance.PublicIp} 'sudo /home/ec2-user/check-odoo.sh'"

```
{% endcode %}

Para facilidad de creacion se ha creado un cloud formation para ser mas rapido, pero aun asi voy a explicar como se crearia de forma manual

El cloud formation lo que hace es crear una base de datos de datos postgre 15-2 en rds y luego crea una instancia odoo que ejecutara los siguientes comandos:

Este es para actualizar todo e instalar cosas que necesitara odoo

{% code expandable="true" %}
```
yum update -y
yum install -y git python3-pip python3-devel postgresql-devel gcc openldap-devel python3-wheel
```
{% endcode %}

Este lo que ara es crear un usuario para odoo y clonar la version 15 de odoo, tambien instalara dependencias necesarias

{% code expandable="true" %}
```
useradd -m -d /opt/odoo -s /bin/bash odoo

# Clone Odoo
cd /opt/odoo
git clone https://github.com/odoo/odoo.git --depth 1 --branch 15.0 /opt/odoo/odoo-server

# FIX: Upgrade pip and force install dependencies
pip3 install --upgrade pip
pip3 install wheel

# CRITICAL FIX: Ignore installed packages to avoid docutils conflict
pip3 install --ignore-installed -r /opt/odoo/odoo-server/requirements.txt
pip3 install psycopg2-binary python-ldap PyPDF2
```
{% endcode %}

Luego va a comprobar que la base de datos se pueda acceder

{% code expandable="true" %}
```
echo "Esperando a RDS..."
sleep 90

# Test connection
          export PGPASSWORD="${DBPassword}"
          for i in {1..30}; do
            if psql -h ${RDSDatabase.Endpoint.Address} -U ${DBUsername} -d postgres -c "SELECT 1" >/dev/null 2>&1; then
              echo "Conexión exitosa a RDS"
              break
            fi
            echo "Esperando a RDS... intento $i"
            sleep 10
          done
```
{% endcode %}

Luego creara la carpeta y el archivo de configuracion de odoo

{% code expandable="true" %}
```
# Create directories
          mkdir -p /etc/odoo /var/log/odoo /opt/odoo/custom-addons /opt/odoo/data

          # Create config
          cat > /etc/odoo/odoo.conf <<EOF
          [options]
          admin_passwd = admin
          db_host = ${RDSDatabase.Endpoint.Address}
          db_port = 5432
          db_user = ${DBUsername}
          db_password = ${DBPassword}
          db_name = ${DBName}
          addons_path = /opt/odoo/odoo-server/addons,/opt/odoo/custom-addons
          data_dir = /opt/odoo/data
          logfile = /var/log/odoo/odoo.log
          log_level = info
          workers = 4
          xmlrpc_port = 8069
          EOF

          # Set permissions
          chown -R odoo:odoo /opt/odoo /var/log/odoo /etc/odoo
          chmod 755 /var/log/odoo

```
{% endcode %}

I finalmente iniciremos odoo y crearemos un servicio para que se vuelva a enchufar cuando se apague

{% code expandable="true" %}
```
 # Initialize database
          cd /opt/odoo/odoo-server
          sudo -u odoo ./odoo-bin -c /etc/odoo/odoo.conf -d ${DBName} -i base --without-demo=all --stop-after-init || true

          # Create systemd service
          cat > /etc/systemd/system/odoo.service <<EOF
          [Unit]
          Description=Odoo
          After=network.target

          [Service]
          Type=simple
          User=odoo
          Group=odoo
          ExecStart=/opt/odoo/odoo-server/odoo-bin -c /etc/odoo/odoo.conf
          Restart=on-failure
          RestartSec=10
          StandardOutput=journal
          StandardError=journal
          LimitNOFILE=65536

          [Install]
          WantedBy=multi-user.target
          EOF

          systemctl daemon-reload
          systemctl enable odoo.service
          systemctl start odoo.service

          echo "Instalación completada. Odoo en puerto 8069"
```
{% endcode %}

Foto de odoo funcionando en aws

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Creacion con docker

{% @github-files/github-code-block url="https://github.com/PROJ-GuillFerriPedro/Aplicaion-odoo-empleados/blob/main/docker-compose.yml" %}

Con docker se van a crear 3 cosas:

1. Una insctancia de odoo
2. Una base de datos de postgresql 15
3.
