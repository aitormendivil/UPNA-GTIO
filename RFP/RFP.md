
Para ir adelantando:

Proyecto desplegado minimamente funcional.
Algo que funcione

eso por un lado

Que alguno de los logs del sistema (clave valor) acceso api gateway,
Que sean enviados a elastic search.

Simplemente que se envien.

Como repaso de los logs.

Tenemos un contenedor en un docker. El contenedor manda los logs a un stdout. 
Fuera del contenedor en la maquina host, puede ser otro contenedor o un agente de la proxima maquina (firebeat) funciona con elastic otro es metricBeat
Se configuran igual (metricbeat y firebeat)

cuando vamos a dockerlogs, tail -f /var/lib/docker/containers/<id>/<id>.json.log 

Firebeat cuando recoge suficientes logs los manda a elastic search.

Exportar a json directamente desde el contenedor.

Se loguea como en kong en un json.

Elastic es una bbdd documental sin columnas,
Se usan indices, un indice es una tabla.

Tenemos indices.
Un indice no es nada en si mismo, una caja en la que metemos documentos, en este caso logs.
Llamamos al indice y configuramos firebeat para hacer que todos apunten el mismo fichero de configuracion.

En un json hay campos, esos campos pueden tener tipos (int, float, string)

Elstic search infiere esos tipos.
[user: "Pablo"] por detras elsatic search genera el mapping para almacenar dichos tipos.

Kong tiene muy claro el tipo de lo que almacena.

Si tenemos el [user: 3] va a fallar porque es otro tipo. Para fechas hay tambien un tipo y hay que especificarlo.

Otra forma es definir los mappings a mano pero por lo que vamos a hacer no merece la pena.

Lo que hace elastic con un indice, lo guarda en unos bloquers de datos llamados Shad primario es donde elastic search escribe. Que puede estar distribuido
en distintas maquinas. Asi tienes lo datos distribuidos.

Aumento de gasto de disco y tener esos datos en memoria.
Muchos Sads esta desaconsejado(2 maquinas de 4gb 120 sads?)

Puedes tener varias maquinas que manden logs al mismo indice. 100 indice con 1 sad por indice todo ok.

Juego de ver que es lo que esta bien o mal.

No pasarse del 70% de memoria de la RAM en elastic search. El problema es que esta hecho sobre java y el garabage colector es una kk

Es necesario hacer un post a la api de elastic y te crea el indice con un primario y una replica.

Hay un elastic gestionado en AWS pero es encesario pagarlo(caro). Se puede usar una T2 medium o small y gestionarlo nosotros.

Aunque se pierdan los datos los importante es que llegue.

Es necesario instalar metricbeat y cambiar los parametros necesarios que nos interesa hacer log de eso.

Lo siguiente es consultar esos datos.
Una tercera herramineta, kibana, grafana, que conectarlo a elastic search pàra hacer una dashboard y ver esos datos.

Tirar pòr lo sencillo.

Un par insatalar firebeat en una maquina y ver que se guardan los datos y ver si aparecen en el dashboard como prueba de concepto y lo añadimos al despliegue
en AWS.

[Demo de Aitor]

Kiabana sin postman o termnal.

vemos los indices y (_cat/indices) para ver los indices
El rotado lo gestiona firebeat.

GET _cat/shards para ver los shards ( con p primario)
wildcard *
ecs-7.4.2-2021.04.*

GET _cluster/health (nodos de datos o nodos master)
Ideal 3 nodos pequeños como master pero no hay que volverse loco.

AL ser de AWS hay ciertas peticiones que no te deja hacer ( activar snapshots o las restauraciones)

GET _cluster/state te dice los mappings

GET ecs-7.4.2-2021.04.12/_settings para ver las settings y para los mappings parecido (_mapping)
mappings generados por nosotros o inferidos.

Es necesario indicerle un tipo de documento dentro del ???

Crear un indice

PUT /index-test

GET _cat/indices/index-test 
GET /index-test/_settings

DELETE /index-test

PUT /index-test {
 "settings": {
    "index": {
      "number_of_shards": 1,
      "number_of_replicas": 1
    }
  },
  "mappings": {
    "properties": {
      "user": { "type": "text" }
     }
  }
}

No se puede cambiar el numero de shards primarios, pero los settings si, es necesario reindexar los indices si se quiere cambiar el numero de shards primarios.

POST index-test/_doc/
{
 "user": "eduard"
}

GET _cat/indices/index-test  //obtener numero de documentos.

Sacar las headers: shoulders toes knees
GET _cat/indices/index-test?v=true

Buscar: ( nos nos interesa buscar de este modo)

GET index-test/_search
{ 
  "query":{
    "term":{
      "user": "eduard"
     }
   }
 }
 
 Firebeat te gestiona todo esto automaticamnete.
 
------------------------------------------------------------------------------------------------------------------------------------------------------------------
 
Devolver todos.

GET index-test/_search
{ 
  "query":{
    "match_all":{}
   }
 }
 
 Importante el campo de Time bien. (iconito calendario)
 
Tasa de metricbeat


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
