# Recursos y valoración económica

### Recursos

* Ordenadores portátiles para desarrollo y pruebas.
* Tablets para los repartidores (cada uno con su identificador).
* Software: Visual Studio, Odoo, Figma, API REST server, gestor de proyectos.
* Espacios de trabajo físicos y virtuales.
* Licencias de software y conectividad continua por internet.

### Valoracion economica

* **Portatiles(son mas baratos)**: 349 € [PcComponentes](https://www.pccomponentes.com/portatiles-mejor-calidad-precio)
* **Tablets**: Entre 359 € y 499€ [PcComponentes](https://www.pccomponentes.com/mejores-tablets-calidad-precio) (Si quieres las mas baratas mejor vete a temu)
* **Portatiles**: 389€ [PcComponentes](https://www.pccomponentes.com/portatiles/16gb-ram/intel-i7)
* **Sillas ergonómicas y soportes**: Una silla ergonómica cuesta entre 80 € y 150 €, soportes para monitor unos 25 €.
* **Formación PRL/ciberseguridad**: Cursos introductorios por empleado oscilan entre 30 € y 100 €, pero suelen estar incorporados gratuitamente en proyectos académicos o vía convenios.
* **Internet**: Contrato mensual de fibra óptica básica rondando los 30 € al mes.



### Analisis de los costes

* **Costes Fijos:**
  * **Hosting y Nube Pública (AWS):** Alquiler mensual de servidores para alojar la base de datos centralizada y los servicios de API REST. Se estima un coste inicial reducido (aprox. 30-50 €/mes) que podría escalar según el volumen de datos y peticiones.
  * **Licencias de Software:** Aunque se prioriza el uso de software de código abierto (Odoo Community) y entornos de desarrollo con licencias académicas o gratuitas (Visual Studio Community, Figma), se debe contemplar la posible adquisición de licencias empresariales en el futuro para soporte o funcionalidades avanzadas.
  * **Conectividad:** Contrato de fibra óptica de alta velocidad para las instalaciones de BatoiLOGIC, necesario para garantizar la comunicación fluida entre el backoffice, los servidores en la nube y los dispositivos móviles de los repartidores (aprox. 30 €/mes).
*   **Costes Variables:**

    * **Actualizaciones y Mantenimiento:** Horas de trabajo del equipo de desarrollo para corregir errores, implementar mejoras menores y adaptar el sistema a nuevos requisitos o cambios normativos.
    * **Soporte Técnico:** Posible contratación de un servicio de soporte externo para la infraestructura en la nube o para la resolución de incidencias críticas.
    * **Ampliaciones de Infraestructura:** A medida que la empresa crezca (más pedidos, más repartidores, expansión territorial), será necesario aumentar la capacidad de los servidores (escalado vertical) o contratar más servicios en la nube (escalado horizontal), lo que incrementará el coste de hosting.
    * **Formación Continua:** Aunque la formación inicial puede estar cubierta, las nuevas versiones del software o la incorporación de personal requerirán acciones formativas puntuales.



    ### Análisis de Beneficios
* **Beneficios Económicos Directos:**
  * **Ahorro de Tiempo:** La automatización en la generación de rutas, albaranes y facturas, así como la comunicación instantánea con los repartidores, reducirá drásticamente las horas de trabajo administrativo.
  * **Reducción de Errores:** La centralización de la información y la eliminación de procesos manuales (como los albaranes en papel) minimizarán las pérdidas de paquetes, los errores de entrega y los desajustes de stock.
  * **Optimización de Recursos:** Una mejor planificación de rutas (incluso sin ser óptimas inicialmente) y el seguimiento en tiempo real de la flota permitirán un uso más eficiente del combustible y del tiempo de los repartidores, aumentando la capacidad diaria de envío sin necesidad de ampliar la flota inmediatamente.
*   **Beneficios Indirectos:**

    * **Mejora de la Productividad:** Al liberar a los empleados de tareas manuales y repetitivas, podrán centrarse en actividades de mayor valor, como la atención al cliente o la mejora de procesos.
    * **Mejora de la Imagen Corporativa:** Ofrecer a los clientes una aplicación con seguimiento en tiempo real de sus pedidos y un servicio fiable y sin retrasos posicionará a BatoiLOGIC como una empresa moderna y profesional.
    * **Mayor Competitividad y Eficiencia:** La capacidad de reaccionar rápidamente a las incidencias, gestionar el stock de forma inteligente (generación automática de pedidos a proveedores) y escalar el negocio sin perder el control dará a la empresa una ventaja competitiva clave en el mercado actual.



### Variabilidad Tecnica y Organizativa

* **Viabilidad Técnica:** El proyecto presenta un alto grado de madurez técnica(sin contar que est oes un proyecto de instituto). Se basa en tecnologías ampliamente conocidas y consolidadas en el sector:
  * **Odoo** como ERP es una solución robusta y flexible para la gestión empresarial.
  * **Arquitectura de microservicios vía API REST** es el estándar de facto para la comunicación entre aplicaciones (app móvil, backoffice, servidor).
  * **Bases de datos relacionales y ORM (Hibernate)** son tecnologías maduras para la persistencia de datos.
  * **Programación en segundo plano (servicios/demonios)** y **sockets (WebSockets)** son técnicas bien conocidas para la automatización y la comunicación bidireccional en tiempo real.
  * **Desarrollo móvil en Android** con gestión de GPS y persistencia local (SQLite) es una práctica común y bien documentada.
  * **Infraestructura en la nube (AWS)** es un servicio maduro, fiable y escalable. Dado que los alumnos de 2º de DAM poseen los conocimientos para implementar todas estas tecnologías (según los RA de los módulos), el proyecto es técnicamente viable con los recursos y conocimientos disponibles.
* **Viabilidad Organizativa:** La solución está diseñada específicamente para resolver los problemas actuales de BatoiLOGIC, por lo que su grado de aceptación por parte de los usuarios debería ser alto.
  * **Para los empleados de backoffice**, las nuevas herramientas (Windows Forms y Odoo) simplificarán su trabajo diario, eliminando tareas tediosas y propensas a errores.
  * **Para los repartidores**, la app móvil les proporcionará toda la información necesaria de manera clara y les permitirá comunicar incidencias al instante, acabando con la pérdida de albaranes y la improvisación de rutas. La funcionalidad de chat en tiempo real con el backoffice facilitará la resolución de problemas sobre la marcha.
  * **Para los clientes**, la nueva aplicación web/móvil mejorará significativamente su experiencia, dándoles control y visibilidad sobre sus compras.
