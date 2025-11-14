# Table of contents

## 1. Introduccion

* [Descripción](README.md)
* [Objetivos globales](1.-introduccion/objetivos-globales.md)
* [Justificación y alcance](1.-introduccion/justificacion-y-alcance.md)
* [Recursos y valoración económica](1.-introduccion/recursos-y-valoracion-economica.md)
* [Planificación](1.-introduccion/planificacion.md)
* [Planificación laboral](1.-introduccion/planificacion-laboral/README.md)
  * [Identificación de Riesgos laborales](1.-introduccion/planificacion-laboral/identificacion-de-riesgos-laborales.md)
  * [Identificación de incidentes de seguridad en sistemas informáticos](1.-introduccion/planificacion-laboral/identificacion-de-incidentes-de-seguridad-en-sistemas-informaticos.md)
  * [Asingacion de roles](1.-introduccion/planificacion-laboral/asingacion-de-roles.md)

## 2. Arquitectura del sistema

* [Visión general del sistema](2.-arquitectura-del-sistema/vision-general-del-sistema/README.md)
  * [Analisis, relacion de ODTS y grupos de interes](2.-arquitectura-del-sistema/vision-general-del-sistema/analisis-relacion-de-odts-y-grupos-de-interes.md)
  * [Concepto de la digitalizacion](2.-arquitectura-del-sistema/vision-general-del-sistema/concepto-de-la-digitalizacion/README.md)
    * [Impacto en los entornos IT y OT](2.-arquitectura-del-sistema/vision-general-del-sistema/concepto-de-la-digitalizacion/impacto-en-los-entornos-it-y-ot.md)
    * [Repercusiones de la falta de digitalización](2.-arquitectura-del-sistema/vision-general-del-sistema/concepto-de-la-digitalizacion/repercusiones-de-la-falta-de-digitalizacion.md)
    * [Tecnologías Habilitadoras Digitales más adecuadas para la situacion.](2.-arquitectura-del-sistema/vision-general-del-sistema/concepto-de-la-digitalizacion/tecnologias-habilitadoras-digitales-mas-adecuadas-para-la-situacion..md)
* [Tecnologías empleadas](2.-arquitectura-del-sistema/tecnologias-empleadas.md)
* [Diagrama de la arquitectura](2.-arquitectura-del-sistema/diagrama-de-la-arquitectura.md)
* [Relación entre las aplicaciones](2.-arquitectura-del-sistema/relacion-entre-las-aplicaciones.md)

## 3. Aplicaciones

* [3.1 Aplicación 1: Api](3.-aplicaciones/3.1-aplicacion-1-api/README.md)
  * [Diseño](3.-aplicaciones/3.1-aplicacion-1-api/diseno.md)
  * [Integracion](3.-aplicaciones/3.1-aplicacion-1-api/integracion.md)
  * [Pruebas realizadas](3.-aplicaciones/3.1-aplicacion-1-api/pruebas-realizadas.md)
  * [Diagrama de la base de datos](3.-aplicaciones/3.1-aplicacion-1-api/diagrama-de-la-base-de-datos.md)
  * [Conclusiones parciales](3.-aplicaciones/3.1-aplicacion-1-api/conclusiones-parciales.md)
  * [OpenApi Docs](3.-aplicaciones/3.1-aplicacion-1-api/openapi-docs/README.md)
    * ```yaml
      type: builtin:openapi
      props:
        models: true
        downloadLink: false
      dependencies:
        spec:
          ref:
            kind: openapi
            spec: proyecto-dam-api
      ```
* [3.2 Aplicación 2: App Repartidores](3.-aplicaciones/3.2-aplicacion-2-app-repartidores/README.md)
  * [Diseño](3.-aplicaciones/3.2-aplicacion-2-app-repartidores/diseno.md)
  * [Integracion](3.-aplicaciones/3.2-aplicacion-2-app-repartidores/integracion.md)
  * [Pruebas realizadas](3.-aplicaciones/3.2-aplicacion-2-app-repartidores/pruebas-realizadas.md)
  * [Conclusiones parciales](3.-aplicaciones/3.2-aplicacion-2-app-repartidores/conclusiones-parciales.md)
* [3.3 Aplicación 3: App Clientes](3.-aplicaciones/3.3-aplicacion-3-app-clientes/README.md)
  * [Diseño](3.-aplicaciones/3.3-aplicacion-3-app-clientes/diseno.md)
  * [Integracion](3.-aplicaciones/3.3-aplicacion-3-app-clientes/integracion.md)
  * [Pruebas realizadas](3.-aplicaciones/3.3-aplicacion-3-app-clientes/pruebas-realizadas.md)
  * [Conclusiones parciales](3.-aplicaciones/3.3-aplicacion-3-app-clientes/conclusiones-parciales.md)
* [3.4 Aplicación 4: Backoffice](3.-aplicaciones/3.4-aplicacion-4-backoffice/README.md)
  * [Diseño](3.-aplicaciones/3.4-aplicacion-4-backoffice/diseno.md)
  * [Integracion](3.-aplicaciones/3.4-aplicacion-4-backoffice/integracion.md)
  * [Pruebas realizadas](3.-aplicaciones/3.4-aplicacion-4-backoffice/pruebas-realizadas.md)
  * [Conclusiones parciales](3.-aplicaciones/3.4-aplicacion-4-backoffice/conclusiones-parciales.md)
* [3.5 Aplicación 5: Odoo](3.-aplicaciones/3.5-aplicacion-5-odoo/README.md)
  * [Diseño](3.-aplicaciones/3.5-aplicacion-5-odoo/diseno.md)
  * [Integracion](3.-aplicaciones/3.5-aplicacion-5-odoo/integracion.md)
  * [Pruebas realizadas](3.-aplicaciones/3.5-aplicacion-5-odoo/pruebas-realizadas.md)
  * [Conclusiones parciales](3.-aplicaciones/3.5-aplicacion-5-odoo/conclusiones-parciales.md)

## 4. Integración del sistema

* [Cómo se comunican entre sí las aplicaciones](4.-integracion-del-sistema/como-se-comunican-entre-si-las-aplicaciones.md)
* [Protocolos y formatos de intercambio de datos](4.-integracion-del-sistema/protocolos-y-formatos-de-intercambio-de-datos.md)
* [Problemas encontrados y soluciones](4.-integracion-del-sistema/problemas-encontrados-y-soluciones.md)

## 5. Pruebas globales

* [Estrategia de pruebas de todo el sistema](5.-pruebas-globales/estrategia-de-pruebas-de-todo-el-sistema.md)
* [Escenarios de integración](5.-pruebas-globales/escenarios-de-integracion.md)
* [Resultados y evidencias](5.-pruebas-globales/resultados-y-evidencias.md)

## 6. Conclusiones generales

* [Resumen de logros](6.-conclusiones-generales/resumen-de-logros.md)
* [Dificultades y cómo se resolvieron](6.-conclusiones-generales/dificultades-y-como-se-resolvieron.md)
* [Posibles mejoras futuras](6.-conclusiones-generales/posibles-mejoras-futuras.md)

## 7. Anexos

* [Manual de usuario](7.-anexos/manual-de-usuario.md)
* [Glosario de términos técnicos](7.-anexos/glosario-de-terminos-tecnicos.md)
* [Referencias / bibliografía](7.-anexos/referencias-bibliografia.md)

## 8. Gestión del proyecto: seguimiento por sprints

* [8.1 Sprint 1 (Fechas: 15/09/2025 – 12/10/2025)](8.-gestion-del-proyecto-seguimiento-por-sprints/8.1-sprint-1-fechas-15-09-2025-12-10-2025/README.md)
  * [Objetivos del sprint](8.-gestion-del-proyecto-seguimiento-por-sprints/8.1-sprint-1-fechas-15-09-2025-12-10-2025/objetivos-del-sprint.md)
  * [Problemas encontrados](8.-gestion-del-proyecto-seguimiento-por-sprints/8.1-sprint-1-fechas-15-09-2025-12-10-2025/problemas-encontrados.md)
  * [Resultados alcanzados](8.-gestion-del-proyecto-seguimiento-por-sprints/8.1-sprint-1-fechas-15-09-2025-12-10-2025/resultados-alcanzados.md)
* [8.2 Sprint 2 (Fechas: 15/09/2025 – 12/10/2025)](8.-gestion-del-proyecto-seguimiento-por-sprints/8.2-sprint-2-fechas-15-09-2025-12-10-2025/README.md)
  * [Objetivos del sprint](8.-gestion-del-proyecto-seguimiento-por-sprints/8.2-sprint-2-fechas-15-09-2025-12-10-2025/objetivos-del-sprint.md)
  * [Problemas encontrados](8.-gestion-del-proyecto-seguimiento-por-sprints/8.2-sprint-2-fechas-15-09-2025-12-10-2025/problemas-encontrados.md)
