# RFP Proyecto Replicador

## Contexto

En un mundo tecnológico en constante cambio, la empresa Mendivil inc. (en adelante el cliente) abre la convocatoria para la compra del replicador con el que dará servicio los
próximos 7 años.

Los proyectos licitadores deberán incluir todas las características exigidas en los RFI publicados anteriormente, junto con la capacidad de funcionar en una nube pública,
obligatoriamente AWS y un sistema de métricas que permitan evaluar el comportamiento del servicio.

Uno de las diferencias fundamentales de este RFP respecto a los RFI anteriores es la necesidad de conocer los costes de la solución completa al detalle, y desglosados según los siguientes parámetros:
* Solución Cloud:
  * Entorno de desarrollo
  * Entorno de preproducción
  * Entorno de producción
* Entornos de desarrollo locales
* Entorno de CI/CD
* Costes en RRHH. Miembros del equipo
* Otros costes en licencias/infraestructuras

El coste de la solución será uno de los parámetros (aunque no el único) más importantes a la hora de decidir el ganador de la convocatoria. Más información en la sección: *Evaluaicón*

## Objetivo

El Objetivo de este RFP consiste en establecer la bases para la convocatoria de la compra del proyecto replicador. Es obligatorio haber participado en los tres RFI anteriores.

La información sobre la entrega de propuestas se encuentra en la sección *Entrega*.

## Preguntas a responder en el RFP

La empresa licitadora deberá dar respuesta justificada a los siguientes puntos:

* Todas las preguntas anunciadas en los RFI anteriores.

* ¿Cómo se despliega el sistema en AWS?
* ¿Cuáles son las métricas/logs para evaluar el funcionamiento del sistema?
* ¿Cuál es la arquitectura del sistema de métricas/logs?
* ¿Cómo se visualizan esas métricas/logs?
* Trabajo futuro o Desarrollos pendientes

## Respuestas a este RFP

* Se requiere la *justificación* (el ¿por qué?) de las respuestas
* Se requieren pruebas para todas las respuestas. Son válidas, código, documentación, capturas de pantalla, vídeos, actas de reuniones, conversaciones, e-mail, audios
* Se requiere una demo en directo del sistema funcionando. El objetivo es demostrar cómo funciona el sistema en la nube. Puede incluir:
  * Demo del despliegue
  * Demo de las métricas
  * Demo de CI/CD
* La demostración no deberá superar los 20 minutos. Superar este tiempo penalizará la puntuación

## Consideraciones

* Cualquier otro aporte de interés en el ámbito de la mejora de la arquitectura, automatización o funcionamiento del sistema
será bienvenida y considerado para una mayor puntuación en la evaluación
* Cualquier otro aporte de interés para el ahorro de costes de la solución será bienvendio
* Solo se valorarán arquitecturas basadas en microservicios
* Solo se valorarán arquitecturas basadas en AWS
* Solo se valorarán microservicios basados en Docker como sistema de contenedores
* Durante la presentación se espera una demostración del sistema funcionando en AWS

## Entrega

* La fecha límite para la entrega del RFP será el: *24 de mayo de 2021*
* Se deberá realizar una presentación el mismo día *24 de mayo de 2021* en el
horario habitual de la asignatura (Requisitos en la sección: *Respuestas a este RFP*)
* La entrega será realizada mediante ficheros `.pdf`, o ficheros `.zip` con el código o documentación necesarias.
* Se puede incluir todo el código y documentación que el licitador considere necesaria
* La tarea de MiAulario será previamente anunciada mediante anuncio en miAulario o e-mail.

## Evaluación

| Tema                                         | Puntuación |
| -------------                                |       ---: |
| Sistema funcionando en AWS                           | 20 |
| Sistema de métricas/logs                             | 10 |
| Costes                                               | 5  |
| Presentación/Demo                                    | 15 |
| Total                                                | 50 |

## Modificaciones sobre este RFI

El cliente se guarda el derecho a modificar este RFI en cualquier momento, siendo obligado su aviso mediante anuncio en miAulario o e-mail a partir del día 17 de mayo del 2021.
