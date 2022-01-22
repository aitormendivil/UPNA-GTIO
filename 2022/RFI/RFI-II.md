# RFI II. Proyecto Cats & Dogs - Arquitectura Basada en Microservicios (DRAFT)

## Contexto

En un mundo tecnológico en constante cambio, la empresa Mendivil inc. (en adelante el cliente) necesita conocer la arquitectura técnica de un sistema de tipo cats & dogs.

Se espera que un proyecto de esta envergadura sea capaz de desplegarse de forma
fácil y sencilla tanto en sistemas locales como en proveedores de infraestructura
externos.

Así el sistema deberá estar adaptado tanto para integración continua como para despliegues
con cargas de trabajo masivas en producción.

Para ello el cliente espera propuestas basadas en sistemas distribuidos en microservicios usando
Docker como tecnología para la creación y despliegue de esos microservicios en contenedores.


## Objetivo

El Objetivo de este RFI consiste en conocer el estado del arte dentro de la arquitectura de las posibles empresas proveedoras de un proyecto de tipo cats & dogs. La fecha límite
se encuentra en la sección *Entrega*.

## Preguntas del RFI

La empresa proveedora deberá dar respuesta justificada a los siguientes puntos:

* ¿Cuáles son los microservicios de los que consiste el sistema cats & dogs?
* ¿Cuál es la funcionalidad de cada uno de los microservicios?
* ¿Cuál es la arquitectura de la solución?
* ¿Cómo es la comunicación entre microservicios?
* ¿Cómo se despliega el sistema en un entorno de test local?
* ¿Cómo se prueba la funcionalidad del sistema en un entorno de test local?
* ¿Cómo se lleva a cabo la autenticación, autorización y auditoria del sistema?
* ¿Por qué es escalable y elástica la solución?


## Respuestas a este RFI

* Se requiere la *justificación* (el ¿por qué?) de las respuestas
* Se requieren pruebas para todas las respuestas. Son válidas, código, documentación, capturas de pantalla, vídeos, actas de reuniones, conversaciones, e-mail, audios

## Consideraciones

* Cualquier otro aporte de interés en el ámbito de la mejora de la arquitectura del sistema
será bienvenida y considerado para una mayor puntuación en la evaluación
* Solo se valorarán arquitecturas basadas en microservicios
* Solo se valorarán microservicios basados en Docker como sistema de contenedores
* Durante la presentación se espera una demostración del sistema funcionando

## Entrega

* La fecha límite para la entrega del RFI será el: *17 de marzo de 2021*
* Se deberá realizar una presentación el mismo día *17 de marzo de 2021* en el
horario habitual de la asignatura
* La entrega será realizada mediante ficheros `.pdf`, o ficheros `.zip` con el código o documentación necesarias. No se admiten enlaces a recursos externos al `.zip`.
* Se puede incluir todo el código y documentación que el proveedor considere necesaria
* La tarea de MiAulario será previamente anunciada mediante anuncio en miAulario o e-mail.

## Evaluación

| Tema                                         | Puntuación |
| -------------                                |       ---: |
| Dockerfiles                                          | 5 |
| Docker Compose files                                 | 10 |
| Documentación código/ejecución                       | 5  |
| Documentación Arquitectura                           | 5  |
| Autenticación Autorización Auditoria                 | 5  |
| Presentación/Demo                                    | 20 |
| Total                                                | 50 |

## Modificaciones sobre este RFI

El cliente se guarda el derecho a modificar este RFI en cualquier momento, siendo obligado su aviso mediante anuncio en miAulario o e-mail a partir del día 24 de febrero del 2021.
