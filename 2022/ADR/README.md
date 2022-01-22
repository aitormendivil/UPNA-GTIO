
# Architecture decision record (ADR)

[Fuente Original](https://github.com/joelparkerhenderson/architecture_decision_record)

Un ADR o architectural decision record es un documento que captura una decisión importante de arquitectura, junto con el contexto, las alternativas contempladas y las consecuencias de la decisión. Aunque está pensado para arquitectura técnica se puede utilizar en muchos otros ámbitos.

Contenidos:

* [Definiciones](#definiciones)
* [Empezar a usar ADRs](#empezar-a-usar-adrs)
* [ADRs con herramientas](#adrs-con-herramientas)
* [ADRs con git](#adrs-con-git)
* [Nomenclatura](#nomenclatura)
* [Sugerencias para redactar buenos ADR](#sugerencias-para-redactar-buenos-adr)
* [Plantillas](#plantillas)
* [Consejos para el trabajo en equipo](#consejos-para-el-trabajo-en-equipo)
* [Para más información](#para-más-información)


## Definiciones

Un **architecture decision record** (ADR) es un documento que captura una decisión importante de arquitectura, junto con el contexto, las alternativas contempladas y las consecuencias de la decisión

Un **architecture decision** (AD) Es una elección de diseño de software para un requisito concreto.

Un **architecture decision log** (ADL) Es la colección completa de ADRs para un proyecto u organización.

Un **architecturally-significant requirement** (ASR) Es un requerimiento que tiene un efecto importante sobre el software.

Todas se embarcan dentro de **architecture knowledge management** (AKM) o gestión del conocimiento de la arquitectura.

El objetivo de este documento consiste en proveer una visión general de los ADRs, cómo crearlos y dónde encontrar más información.

Abreviaciones (Como ya vamos viendo por lo general se utiliza el inglés):

* **AD**: architecture decision
* **ADL**: architecture decision log
* **ADR**: architecture decision record
* **AKM**: architecture knowledge management
* **ASR**: architecturally-significant requirement


## Empezar a usar ADRs

Para comenzar a usar ADR, hable con sus compañeros de equipo sobre estos temas.

Identificación de la decisión:

* ¿Cómo de urgente o importantes es el AD?
* ¿Tiene que hacerse ahora o puede esperar hasta que se sepa más?
* Tanto la experiencia personal como colectiva, así como los métodos y prácticas de diseño reconocidos, pueden ayudar en la identificación de decisiones.
* Idealmente mantened una lista de decisiones pendientes que complemente la lista de tareas pendientes del producto.

Toma de decisiones:

* Existe una serie de técnicas de toma de decisiones, tanto generales como específicas de arquitectura de software, por ejemplo, [Dialogue Mapping](https://www.lucidchart.com/blog/what-is-dialogue-mapping).

Presentación y ejecución de decisiones:

* Los AD se utilizan en el diseño de software; por lo tanto, deben ser comunicados y aceptados por las partes interesadas del sistema que lo financian, lo desarrollan y lo operan.
* Los AD también deben ser (re)considerados al modernizar un sistema de software durante la evolución o mantenimiento del software.

Compartir decisiones (opcional):

* Muchos AD se repiten entre proyectos.

* Por lo tanto, las experiencias con decisiones pasadas, tanto buenas como malas, pueden ser valiosos activos reutilizables cuando se emplea una estrategia explícita de gestión del conocimiento.

Documentación de la decisión:

* Existen muchas plantillas y herramientas para la captura de decisiones.
* Ver procesos tradicionales de diseño de arquitectura e ingeniería de software, p. Ej. diseños de tabla sugeridos por IBM UMF y por Tyree y Akerman de CapitalOne.

Orientación para la toma de decisiones:

* Los pasos anteriores se adaptaron de la entrada de Wikipedia sobre [Decisión de arquitectura] (https://en.wikipedia.org/wiki/Architectural_decision)
* Existen una serie de técnicas de toma de decisiones, tanto generales como específicas de software y arquitectura de software, por ejemplo, [Dialogue Mapping](https://www.lucidchart.com/blog/what-is-dialogue-mapping).


## ADRs con herramientas

Puede comenzar a usar ADR con herramientas de la forma que desee.

Por ejemplo:

 * Si le gusta usar Google Drive y la edición en línea, puede crear un documento de Google o una hoja de Google.
 * Si desea utilizar el control de versiones del código fuente, como git, puede crear un archivo para cada ADR.
 * Si le gusta utilizar herramientas de planificación de proyectos, como Atlassian Jira, puede utilizar el rastreador de planificación de la herramienta.
 * Si le gusta usar wikis, como MediaWiki, puede crear una wiki de ADRs.


## ADRs con git

Crea un directorio para los ADRs.

```sh
$ mkdir adr
```

Para cada ADR crea un fichero de texto como:  `ADR001-base-de-datos.md`:

```sh
$ vi ADR001-base-de-datos.md
```

Escribe lo que quieras en el ADR. Puedes utilizar las plantillas recomendadas.

Haz un `commit` con el ADR y haz `push` al repositio.


## Nomenclatura

Si eliges crear ADRs usando archivos de texto, lo más probable es que necesites una convención de nombres.

Ejemplos:

* ADR###_elección_basedatos.md
* ADR###YYYYMMDD_timestamps.md
* gestion_contraseñas.md
* handle_exceptions.md
* ...

Ejemplo de convención de nombres

* El nombre utiliza verbos en presente de imperativo.
* El nombre utiliza minúsculas y guiones bajos.
* La extensión es markdown.

## Sugerencias para redactar buenos ADR

Características de un buen ADR:

* Fecha: identifica cuándo se hizo el anuncio
* Razón: explique la razón por la que se realizó el AD en particular
* Registro inmutable: las decisiones tomadas en un ADR publicado anteriormente no deben modificarse (para eso existe un nuevo ADR)
* Especificidad: cada ADR debe ser sobre un solo AD

Características de un buen contexto en un ADR:

* Explique la situación de su organización y las prioridades comerciales.
* Incluya el fundamento y las consideraciones basadas en las habilidades del equipo.

Características de las buenas consecuencias en un ADR:

* Enfoque correcto: "Tenemos que empezar a hacer X en lugar de Y"
* Enfoque incorrecto - No explique el AD en términos de "Pros" y "Contras" de haber realizado el AD en particular.

Un nuevo ADR puede reemplazar a un ADR anterior:

* Cuando se realiza un AD que reemplaza o invalida un ADR anterior, se debe crear un nuevo ADR


## Plantillas

Ejemplos recomendados

* [Español](plantilla.md)
* [Inglés](template.md)

Otros ejemplos de plantillas de ADRs en internet:

* [Plantilla de ADR por Michael Nygard](adr_template_by_michael_nygard.md) (simple y popular)
* [Plantilla de ADR para caso de negocio](adr_template_for_business_case.md) (más estilo MBA, con costes, con análisis [SWOT](https://en.wikipedia.org/wiki/SWOT_analysis))
* [Plantilla de ADR MADR](adr_template_madr.md) (más Markdown)
* [Plantilla de ADR usando Planguage](adr_template_using_planguage.md) (más orientada a la calidas)


## Consejos para el trabajo en equipo

Si está considerando usar ADRs con tu equipo, estos son algunos consejos que hemos aprendido trabajando con diferentes equipos.

Tienes la oportunidad de liderar a tus compañeros de equipo, hablando juntos sobre el "por qué", en lugar de exigir el "qué". Por ejemplo, los ADRs son una forma de que los equipos piensen de manera más inteligente y se comuniquen mejor. Los registros de decisiones no son valiosos si son solo un papeleo obligatorio después de
haber tomado una decisión.

Algunos equipos prefieren el nombre "decisiones" sobre la abreviatura "ADR". Cuando algunos equipos utilizan el nombre de carpeta "decisiones", es como si se enciendese una bombilla y el equipo comenzase a incluir más información en la carpeta, como decisiones de proveedores, decisiones de planificación, decisiones de programación, etc. Todos estos tipos de información pueden utilizar la misma plantilla.

En teoría, la inmutabilidad es ideal. En la práctica, la mutabilidad ha funcionado mejor para nuestros equipos. Insertamos la nueva información en el ADR existente, con un sello de fecha y una nota de que la información llegó después de la decisión. Este tipo de enfoque conduce a un "documento vivo" que todos podemos actualizar. Las actualizaciones típicas son cuando obtenemos información gracias a nuevos compañeros de equipo, nuevas ofertas o resultados del mundo real de nuestros usos, o cambios posteriores de terceros, como capacidades de proveedores, planes de precios, acuerdos de licencia, etc.

## Para más información

Introducción:

* [Architectural decision (wikipedia.org)](https://wikipedia.org/wiki/Architectural_decision)
* [Architecturally significant requirements (wikipedia.org)](https://wikipedia.org/wiki/Architecturally_significant_requirements)

Plantillas:

* [Documenting architecture decisions - Michael Nygard (thinkrelevance.com)](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions)
* [Markdown Architectural Decision Records (adr.github.io)](https://adr.github.io/madr/) - provided by the [adr GitHub organization](https://adr.github.io/)
* [Template for documenting architecture alternatives and decisions (stackoverflow.com)](http://stackoverflow.com/questions/7104735/template-for-documenting-architecture-alternatives-and-decisions)

En profundidad:

* [ADMentor XML project (github.com)](https://github.com/IFS-HSR/ADMentor)
* [Architectural Decision Guidance across Projects: Problem Space Modeling, Decision Backlog Management and Cloud Computing Knowledge (ifs.hsr.ch)](https://www.ifs.hsr.ch/fileadmin/user_upload/customers/ifs.hsr.ch/Home/projekte/ADMentor-WICSA2015ubmissionv11nc.pdf)
* [The Decision View's Role in Software Architecture Practice (computer.org)](https://www.computer.org/csdl/mags/so/2009/02/mso2009020036-abs.html)
* [Documenting Software Architectures: Views and Beyond (resources.sei.cmu.edu)](http://resources.sei.cmu.edu/library/asset-view.cfm?assetID=30386)
* [Architecture Decisions: Demystifying Architecture (utdallas.edu)](https://www.utdallas.edu/~chung/SA/zz-Impreso-architecture_decisions-tyree-05.pdf)
* [ThoughtWorks Technology Radar: Lightweight Architecture Decision Records (thoughtworks.com)](https://www.thoughtworks.com/radar/techniques/lightweight-architecture-decision-records)
