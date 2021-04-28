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

