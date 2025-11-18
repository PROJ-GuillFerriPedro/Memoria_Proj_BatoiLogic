# 3.5 Aplicación 5: Odoo

{% embed url="https://github.com/PROJ-GuillFerriPedro/Aplicaion-odoo-empleados" %}



## Introducción

TODO: Estudi de la implementació d’un sistema ERP-CRM en el sistema operatiu\
seleccionat.

Implementar Odoo en un servidor Ubuntu pueden traer varias ventajas en torno a la excalabilidad y seguridad:​

### Integración y Centralización

* Odoo permite gestionar todas las áreas del negocio (ventas, compras, contabilidad, recursos humanos, inventario, etc.) en una única plataforma centralizada.​
* Facilita la integración de procesos y elimina la duplicidad de información, mejorando la colaboración y la visibilidad interna.​

### Automatización y Eficiencia

* Automatiza múltiples tareas y flujos de trabajo, como facturación, inventarios, reportes y gestión de clientes, ayudando a reducir errores manuales y tiempo de operación.​
* Gracias a sus módulos extensibles y personalizables, se adapta fácilmente a las necesidades y crecimiento de la empresa.​

### Escalabilidad y Flexibilidad

* Puede comenzar con pocos módulos y crecer fácilmente añadiendo más funcionalidades a medida que el negocio lo requiera, sin necesidad de cambiar de sistema.​
* Admite personalizaciones profundas a nivel de procesos y módulos por su naturaleza open source.​

### Seguridad, Soporte y Actualización

* Ubuntu Server ofrece un entorno seguro, estable y ampliamente soportado por la comunidad open source, asegurando actualizaciones regulares y alta compatibilidad con Odoo.​
* Se pueden implementar fácilmente buenas prácticas de seguridad, como HTTPS y autenticación, aprovechando herramientas estándar de Linux.​

### Reducción de Costos

* Elimina la necesidad de múltiples sistemas independientes y licencias de software adicionales, reduciendo costes operativos y de mantenimiento.​
* Al estar sobre Ubuntu y siendo Odoo de código abierto, se reduce la dependencia de proveedores y licenciamiento privativo. ​

### Accesibilidad y Personalización

* Odoo en Ubuntu puede ejecutarse tanto en la nube como en servidores locales, adaptándose a la infraestructura que mejor convenga a la empresa.​
* Permite implementar reglas automatizadas, paneles de control personalizados y reportes en tiempo real, facilitando la toma de decisiones.​
* Puedes correrlo en un servicio como docker para facilitar la instalacion

## Objetivos

## Requisitos específicos

* **Hardware mínimo**: 1 vCPU, 1 GB de RAM, 15 GB de espacio en disco.
* **Hardware recomendado**: 4 vCPU, 4 GB de RAM, 25 GB de disco, especialmente si se prevé crecimiento o uso intensivo de módulos adicionales.​
* **Software**:
  * Ubuntu Server 22.04 a 24.04 LTS, actualizado.
  * PostgreSQL como motor de base de datos (por ejemplo, versión 16).
  * Python 3.x, dependiendo de la versión de Odoo que se desee instalar.
  * Nginx como proxy inverso (opcional pero recomendado para producción).
  * Node.js para la generación de archivos estáticos.​
