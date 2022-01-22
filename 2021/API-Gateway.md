# API Gateway

Un API Gateway, como su nombre indica consiste en la puerta de entrada de nuestro sistema de microservicios.

Los microservicios exponen APIs para que un cliente se comunique con ellos, o para comunicarse entre sí. Pero, ¿qué ocurre si un servicio no se tiene que poder comunicar con otro por razones de seguridad? o ¿cómo hago is quiero ofrecer distintos productos (APIs) a distintos clientes?

Dentro de los sistemas SaaS basados en servicios necesitamos una forma de ofrecer:
* Autorización
* Autenticación
* Granularidad en el acceso a los servicios, o a los endpoints (rutas)
* Multy-tenancy (Distintos clientes pueden consumir los servicios, existiendo una separación lógica de los datos. En este caso si existe persistencia siempre será necesario desarrollo también a nivel de servicio)
* Auditoria/Logs
* Control del tráfico
* Modificación de las peticiones
  * Versionado de la API en el endpoint
  * Homogeneización de los endpoints
  * Añadir/eliminar cabeceras, parámetros del querystring

![url](./img/gateway.png)

**Ejercicio**

> Proxy VS proxy inverso.

> Pensar en formas de crear un sistema multitenant con un apigateway.

## Soluciones en el mercado

* [Amazon API Gateway](https://aws.amazon.com/api-gateway/)
* [Google Cloud APIGee](https://cloud.google.com/apigee?hl=es)
* [Azure API Gateway](https://azure.microsoft.com/es-es/services/api-management/#features)
* [Kong](https://konghq.com)

## Kong

> En nuestro proyecto final vamos a trabajar con Kong como API Gateway, y es necesario para el [RFI II](RFI/RFI-II.md) por lo que cuanto antes os sintáis cómodos con Kong mejor.

**Ejercicio**

> Realizar el 5 min Quickstart usando Docker en vez de instalar Kong en la máquina.
https://docs.konghq.com/gateway-oss/2.3.x/getting-started/quickstart/
(La parte de gRPC no es necesaria)

> Pensar y Probar los plugins necesarios para conseguir AAA (Una vez decididos, documentarlo).

### Referencias

https://docs.microsoft.com/en-us/azure/architecture/microservices/design/gateway
