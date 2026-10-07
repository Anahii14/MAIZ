# Guía técnica del proceso de desarrollo de software

## Propósito y alcance

Esta guía describe el proceso de elaboración de software desde la perspectiva de ingeniería de sistemas. Su foco de trabajo está en las primeras cuatro fases del ciclo de vida del desarrollo de software (SDLC): **análisis de requisitos, diseño del sistema, desarrollo o codificación y pruebas**. También resume las otras etapas del ciclo de vida y presenta prácticas, herramientas y ejemplos que ayudan a aplicar esas cuatro fases de manera coordinada.

El proceso puede ejecutarse de forma secuencial o iterativa. En ambos casos, las decisiones deben ser trazables: cada necesidad relevante se convierte en requisitos verificables, los requisitos orientan el diseño y la implementación, y las pruebas aportan evidencia de que el producto satisface lo especificado.

---

## 1. Proceso general: descripción de cada fase

| Fase | Actividades principales | Entregable principal |
|---|---|---|
| **1. Análisis de requisitos** | Identificar necesidades y objetivos; recopilar requisitos con usuarios y partes interesadas; analizar, priorizar y documentar requisitos; definir alcance, restricciones, supuestos y criterios de aceptación. | **Documento de requisitos** (por ejemplo, una especificación de requisitos de software, SRS). |
| **2. Diseño del sistema** | Diseñar la arquitectura; modelar datos; diseñar interfaces; definir componentes, responsabilidades, contratos e interacciones; analizar decisiones técnicas y riesgos. | **Documento de diseño** (diseño de arquitectura y diseño técnico, con diagramas y modelos pertinentes). |
| **3. Desarrollo / codificación** | Programar módulos conforme al diseño y los requisitos; seguir estándares; usar control de versiones; revisar código; ejecutar comprobaciones y pruebas automatizadas durante la implementación. | **Código fuente**, junto con su historial de cambios y configuración necesaria para construirlo. |
| **4. Pruebas** | Preparar casos y datos de prueba; ejecutar pruebas unitarias, de integración, del sistema y de aceptación; registrar defectos, resultados y evidencias; verificar correcciones. | **Informe de pruebas**, con alcance, resultados, defectos, riesgos pendientes y conclusión de calidad. |

### 1.1 Análisis de requisitos

El equipo comprende el problema antes de decidir cómo resolverlo. Identifica usuarios y otras partes interesadas, estudia procesos actuales y recopila necesidades mediante entrevistas, talleres, observación, revisión documental o prototipos. Después aclara ambigüedades, conflictos, prioridades y restricciones.

Los requisitos deben poder comprobarse. Por ejemplo, en lugar de “el sistema será rápido”, se puede especificar: “el 95 % de las búsquedas de productos responderá en menos de dos segundos bajo la carga acordada”. Se define también qué queda dentro y fuera del alcance, así como los criterios de aceptación.

**Entregable:** documento de requisitos versionado y aprobado por las partes correspondientes. Puede contener contexto, alcance, actores, requisitos funcionales y no funcionales, reglas de negocio, interfaces, restricciones, dependencias y criterios de aceptación.

### 1.2 Diseño del sistema

El diseño transforma los requisitos en una solución técnica. Define la arquitectura y sus límites, los componentes, sus responsabilidades y comunicaciones, el modelo de datos, las interfaces de usuario y las interfaces entre sistemas. Considera atributos de calidad como seguridad, disponibilidad, rendimiento, mantenibilidad y escalabilidad.

Las decisiones importantes deben documentar alternativas, razones, impactos y riesgos. El diseño no tiene que anticipar cada línea de código, pero sí debe ofrecer al equipo suficiente claridad para implementar y probar de forma coherente.

**Entregable:** documento de diseño con vistas arquitectónicas, diagramas pertinentes, contratos de interfaces, modelo de datos, decisiones técnicas y requisitos de calidad asociados.

### 1.3 Desarrollo / codificación

El equipo implementa los componentes siguiendo el diseño y los estándares acordados. Organiza el trabajo en cambios pequeños y revisables, mantiene el código en un sistema de control de versiones, utiliza revisiones de código y automatiza, cuando sea viable, el análisis estático, la compilación y las pruebas.

El código debe ser comprensible, seguro y mantenible. Los cambios que alteren requisitos o diseño se revisan para preservar trazabilidad y actualizar la documentación relacionada.

**Entregable:** código fuente ejecutable o construible, con dependencias y configuración documentadas, cambios versionados y pruebas automatizadas asociadas.

### 1.4 Pruebas

Las pruebas evalúan el producto y sus componentes frente a requisitos y criterios de aceptación. Se planifican desde etapas tempranas: el diseño de pruebas puede revelar requisitos ambiguos y las pruebas unitarias acompañan la codificación. Cada defecto se registra con pasos de reproducción, resultado esperado, resultado observado y evidencia relevante.

Tras corregir un defecto, se repite la prueba correspondiente y se consideran pruebas de regresión para detectar efectos secundarios.

**Entregable:** informe de pruebas con versiones evaluadas, entorno, casos ejecutados, resultados, defectos abiertos o corregidos, limitaciones y recomendación de salida.

---

## 2. Tipos de requisitos

Los requisitos expresan necesidades y condiciones que el sistema debe satisfacer. Se redactan de forma clara, única, verificable y trazable. Conviene asignarles identificadores, prioridad, fuente, criterio de aceptación y estado.

### A. Requisitos funcionales

Describen **qué debe hacer** el sistema: servicios, comportamientos, reglas de negocio y respuestas ante acciones o eventos.

| Ejemplo | Criterio verificable ilustrativo |
|---|---|
| Registrar usuarios | Con datos válidos, el sistema crea una cuenta con identificador único; si el correo ya existe, informa el conflicto sin duplicar la cuenta. |
| Generar reportes de ventas | Un usuario autorizado puede generar un informe por rango de fechas y exportar los resultados al formato definido. |
| Realizar inicio de sesión | El sistema permite iniciar sesión con credenciales válidas y rechaza las inválidas sin revelar cuál dato falló. |
| Buscar productos | La búsqueda devuelve productos que coinciden con los filtros disponibles y respeta los permisos de acceso. |
| Gestionar inventarios | Un usuario autorizado puede consultar y actualizar existencias, y el sistema conserva el registro de movimientos definido por las reglas de negocio. |

### B. Requisitos no funcionales

Describen **cómo debe funcionar** el sistema o qué nivel de calidad debe alcanzar. Deben expresarse con métricas, condiciones de medición y umbrales cuando sea posible; calificativos aislados como “seguro” o “escalable” no bastan como criterios de aceptación.

| Atributo / ejemplo | Especificación medible ilustrativa |
|---|---|
| Rendimiento: “El sistema debe responder en menos de 2 segundos” | El 95 % de las solicitudes de búsqueda responde en menos de 2 segundos con la carga y el entorno de prueba acordados. |
| Seguridad: “El sistema debe ser seguro y proteger los datos” | Los datos sensibles se protegen en tránsito y en almacenamiento conforme a la política aplicable; el acceso requiere autenticación y autorización. |
| Disponibilidad: “El sistema debe estar disponible 24/7” | Disponibilidad objetivo de 99,9 % mensual, con exclusiones de mantenimiento previamente definidas y un método acordado de medición. |
| Escalabilidad: “El sistema debe ser escalable” | El sistema admite el aumento previsto de usuarios o transacciones sin exceder los umbrales de latencia y error especificados. |

Otros atributos habituales incluyen usabilidad, accesibilidad, compatibilidad, mantenibilidad, portabilidad, observabilidad y recuperación ante fallos.

---

## 3. Ciclo de vida del software (SDLC)

Un ciclo de vida completo suele contemplar las siguientes seis fases:

1. **Requisitos:** determinar qué problema se resolverá, para quién y con qué restricciones.
2. **Diseño:** definir cómo se organizará la solución y cómo cumplirá los requisitos.
3. **Desarrollo:** construir los componentes y mantenerlos bajo control de cambios.
4. **Pruebas:** verificar comportamientos y evaluar si el producto satisface los criterios acordados.
5. **Implementación:** desplegar la versión aprobada en el entorno previsto y habilitar su uso.
6. **Mantenimiento:** corregir defectos, atender cambios y conservar la seguridad y utilidad del sistema.

Esta guía detalla las primeras cuatro fases. La implementación y el mantenimiento se incluyen para mostrar el contexto del ciclo completo, no como procedimientos detallados.

### Relación secuencial e iterativa

En una secuencia tradicional, los requisitos orientan el diseño; el diseño guía la codificación; y el producto construido se verifica mediante pruebas. Los resultados de cada etapa alimentan la siguiente. Por ejemplo, un criterio de aceptación de un requisito se traduce en casos de prueba, y una decisión de diseño determina qué componentes se deben integrar.

En la práctica hay retroalimentación. Una prueba puede descubrir que un requisito es ambiguo, que una arquitectura no cumple un objetivo de rendimiento o que un cambio de alcance obliga a revisar el modelo de datos. El equipo vuelve a la fase pertinente, actualiza los artefactos y registra el cambio. En procesos iterativos, esos ciclos ocurren deliberadamente en incrementos pequeños; en procesos más secuenciales, se controlan mediante revisiones y gestión formal de cambios.

La trazabilidad conecta cada requisito con elementos de diseño, cambios de código y pruebas. Así se puede valorar el impacto de una modificación y comprobar qué se ha cubierto.

---

## 4. Metodologías de desarrollo

| Metodología | Características | Cuándo usarla y consideraciones |
|---|---|---|
| **Cascada** | Enfoque secuencial: cada fase se completa y revisa antes de iniciar la siguiente. La documentación y las aprobaciones suelen ser formales. | Adecuada para proyectos pequeños con requisitos estables, alcance conocido y necesidad de hitos previsibles. Los cambios tardíos pueden resultar costosos. |
| **Iterativa** | La solución se desarrolla mediante ciclos de análisis, diseño, construcción y evaluación. Cada iteración refina la solución con aprendizaje y retroalimentación. | Útil cuando los requisitos pueden cambiar o hay incertidumbre técnica. Requiere priorizar y controlar el alcance de cada iteración. |
| **Incremental** | El producto se entrega en partes funcionales; cada incremento agrega capacidades utilizables a una base existente. | Conveniente para entregar valor temprano, reducir el tamaño de las entregas y validar capacidades gradualmente. Los incrementos deben integrarse sobre una arquitectura coherente. |
| **Ágil (Scrum)** | Trabajo organizado en sprints cortos, con objetivos de sprint, backlog priorizado, revisión frecuente y colaboración continua entre equipo y partes interesadas. Scrum define roles, eventos y artefactos para inspeccionar y adaptar el trabajo. | Adecuada para productos dinámicos, con retroalimentación frecuente y equipos colaborativos. Necesita disponibilidad de las partes interesadas, objetivos claros y disciplina para no convertir el sprint en una lista descontrolada de tareas. |

Las metodologías no sustituyen el análisis ni las pruebas: cambian cómo se planifican y distribuyen. Un equipo puede, por ejemplo, documentar criterios de aceptación y arquitectura ligera en cada incremento, en vez de esperar a producir un único paquete documental al final.

---

## 5. Arquitecturas de software

La arquitectura define la estructura de alto nivel del sistema, sus elementos, relaciones y decisiones que condicionan atributos de calidad.

| Arquitectura | Descripción | Usos y consideraciones |
|---|---|---|
| **Cliente-servidor** | Uno o más clientes solicitan servicios a un servidor que procesa solicitudes y accede a recursos compartidos. | Muy común en sistemas web y aplicaciones móviles. Deben diseñarse la disponibilidad del servidor, la seguridad de comunicaciones y la gestión de carga. |
| **MVC (Modelo-Vista-Controlador)** | Separa el modelo (datos y reglas), la vista (presentación) y el controlador (coordina entradas y acciones). | Muy usado en aplicaciones web. Facilita separar responsabilidades, aunque no determina por sí solo toda la arquitectura ni garantiza que la lógica quede correctamente aislada. |
| **Capas (N-Layer)** | Agrupa responsabilidades en capas, por ejemplo presentación, aplicación o negocio, acceso a datos e infraestructura. | Útil para organizar sistemas empresariales y establecer límites claros. Las dependencias entre capas deben controlarse para evitar acoplamiento y saltos indebidos. |
| **Microservicios** | Divide el sistema en servicios pequeños, desplegables de forma independiente y organizados alrededor de capacidades de negocio, comunicados mediante interfaces. | Puede ser apropiada cuando existen necesidades de escalado, despliegue o autonomía diferenciadas. Aumenta la complejidad operativa, de observabilidad, consistencia de datos y comunicación distribuida; no es una elección automática para todo sistema. |

La selección se basa en requisitos y restricciones concretos: tamaño del equipo, complejidad del dominio, carga, operación, capacidades de despliegue y costo de mantenimiento.

---

## 6. Modelado UML: diagramas más usados

UML (Unified Modeling Language) ofrece notaciones para representar aspectos de un sistema. Los diagramas se eligen según la pregunta que se necesita responder; no es obligatorio producir todos en cada proyecto.

| Diagrama | Propósito |
|---|---|
| **Casos de uso** | Representa actores externos y funcionalidades con las que interactúan. Ayuda a delimitar el alcance funcional y las relaciones entre actores y casos de uso. |
| **Clases** | Muestra la estructura estática: clases, atributos, operaciones y relaciones como asociación, herencia y composición. Ayuda a razonar sobre el modelo del dominio y el diseño orientado a objetos. |
| **Secuencia** | Muestra, en orden temporal, mensajes e interacciones entre actores u objetos para realizar un escenario. Es útil para aclarar contratos y responsabilidades de una operación. |
| **Actividades** | Representa flujos de trabajo, decisiones, paralelismo y condiciones de un proceso. Permite describir procesos de negocio o algoritmos. |

Los diagramas deben tener un propósito, nombres consistentes y el nivel de detalle adecuado. Si el diseño cambia, los modelos relevantes también deben actualizarse para no contradecir la implementación.

---

## 7. Base de datos

El diseño de datos convierte las necesidades de información del sistema en estructuras que preservan significado, consistencia y acceso eficiente.

- **Modelo entidad-relación (E-R):** diseño conceptual que identifica entidades (por ejemplo, Cliente, Venta y Producto), sus atributos y relaciones. Una relación puede tener cardinalidad uno a uno, uno a muchos o muchos a muchos.
- **Tablas:** en una base relacional, organizan registros por entidad o concepto. Ejemplos: `usuarios`, `productos` y `ventas`. Las columnas representan atributos y cada fila una instancia.
- **Llaves primarias:** identifican de manera única cada fila, no admiten duplicados y normalmente no deben ser nulas. Ejemplo: `id_usuario`.
- **Relaciones:** conectan datos, normalmente con llaves foráneas. Por ejemplo, `ventas.id_cliente` puede referenciar `clientes.id_cliente`, expresando qué cliente realizó cada venta.
- **Integridad:** asegura consistencia mediante restricciones, tipos de datos, unicidad, llaves primarias y foráneas, reglas de negocio y transacciones. También incluye decidir cómo tratar borrados, actualizaciones, concurrencia y datos inválidos.

Antes de implementar el modelo, conviene definir reglas como si una venta puede existir sin cliente, cómo se registran los cambios de stock y qué operaciones deben ser atómicas. El diseño debe evitar duplicidad innecesaria y considerar consultas y volúmenes previstos.

---

## 8. Tipos de pruebas

Las pruebas se distinguen por el alcance que evalúan. No son etapas aisladas: se diseñan desde los requisitos y se ejecutan a distintos niveles durante el desarrollo.

| Tipo | Qué evalúa | Ejemplo |
|---|---|---|
| **Pruebas unitarias** | Una unidad pequeña, como una función, clase o módulo, de manera aislada; verifican resultados para entradas y condiciones relevantes. | Comprobar que una función calcula correctamente el stock después de registrar una entrada. |
| **Pruebas de integración** | La interacción entre componentes, servicios o sistemas y el intercambio de datos entre ellos. | Verificar que el módulo de ventas persiste la venta y actualiza el inventario dentro de la transacción esperada. |
| **Pruebas del sistema** | El sistema completo frente a requisitos funcionales y no funcionales en un entorno representativo. | Ejecutar el flujo de compra completo y medir el tiempo de respuesta bajo la carga prevista. |
| **Pruebas de aceptación (UAT)** | Si el comportamiento satisface necesidades y criterios acordados desde la perspectiva del usuario o representante del negocio. | Un usuario valida que puede consultar existencias y generar el informe requerido con los permisos definidos. |

Cada caso debería indicar identificador, requisito asociado, precondiciones, datos, pasos, resultado esperado y resultado obtenido. Según el riesgo, también se planifican pruebas de regresión, rendimiento, seguridad, accesibilidad, compatibilidad y recuperación.

---

## 9. Seguridad del software

La seguridad se considera desde los requisitos y el diseño, se aplica en el código y se verifica mediante pruebas y revisiones. Los controles concretos dependen del tipo de datos, el riesgo, el entorno y las obligaciones aplicables.

- **Autenticación:** verifica la identidad del usuario o servicio. Debe proteger credenciales, aplicar políticas adecuadas y evitar revelar información sensible en mensajes de error.
- **Autorización:** determina qué acciones puede realizar una identidad autenticada. Debe comprobarse en el servidor para cada operación y recurso protegido.
- **Cifrado:** protege la confidencialidad e integridad de datos sensibles en tránsito y, cuando corresponda, en almacenamiento. Las claves deben gestionarse de forma segura y separada de los datos protegidos.
- **Control de acceso:** organiza permisos mediante roles y privilegios, aplicando el principio de mínimo privilegio y revisando permisos por recurso y función.
- **Respaldo de datos:** mantiene copias periódicas protegidas y verificables. Deben definirse retención, acceso y pruebas de restauración; una copia no comprobada no garantiza recuperación.
- **Validación de entradas:** valida tipo, formato, longitud y rango en el límite de confianza. Para consultas a bases de datos se usan consultas parametrizadas; la validación complementa, pero no sustituye, la codificación segura contextual.
- **Auditoría y monitoreo:** registra eventos relevantes de seguridad y operación con protección contra alteración y acceso indebido. Se evitan contraseñas, tokens y otros secretos en los registros; se establecen alertas y procedimientos de respuesta.

Durante requisitos y diseño se identifican activos, amenazas y límites de confianza; durante codificación se siguen prácticas seguras y se revisan dependencias; durante pruebas se validan controles y se comprueba que los errores no filtren datos.

---

## 10. Control de versiones (Git)

**Git** es un sistema de control de versiones distribuido. Cada clon contiene el historial del repositorio, lo que permite trabajar localmente, comparar cambios, crear ramas y recuperar versiones anteriores. **GitHub** y **GitLab** son plataformas que alojan repositorios y ofrecen colaboración, revisiones, seguimiento de tareas y, según la configuración, automatización de integración y entrega.

### Flujo básico

1. **Clonar (`clone`):** obtener una copia local del repositorio remoto y su historial.
2. **Modificar:** crear una rama o trabajar según la política del equipo; cambiar archivos y revisar las diferencias.
3. **Commit (`commit`):** guardar un conjunto coherente de cambios en el historial local con un mensaje descriptivo.
4. **Push (`push`):** publicar los commits locales en el repositorio remoto.
5. **Pull (`pull`):** incorporar cambios remotos a la rama local; antes de integrar, revisar conflictos y el efecto de esos cambios.
6. **Merge (`merge`):** combinar los cambios de una rama con otra, normalmente tras revisión y validaciones. Los conflictos se resuelven de forma explícita y se comprueba el resultado.

**Beneficios:** historial auditable, colaboración paralela, revisión de cambios, recuperación ante errores y respaldo distribuido. Git no sustituye las copias de seguridad ni las políticas para proteger ramas, secretos y permisos del repositorio.

---

## 11. Herramientas y tecnologías recomendadas

La selección debe responder a los requisitos, las competencias del equipo, el ecosistema disponible, el costo y la operación a largo plazo; las opciones de esta tabla son ejemplos, no una receta universal.

| Categoría | Opciones |
|---|---|
| **Lenguajes** | PHP, Python, JavaScript, Java |
| **Frameworks** | Laravel, Django, Spring Boot, .NET |
| **Bases de datos** | MySQL, PostgreSQL, SQL Server, MongoDB |
| **Front-end** | HTML/CSS, React, Vue.js, Bootstrap |
| **Herramientas** | VS Code (edición y desarrollo), Figma (prototipos e interfaces), Postman (pruebas de API), Draw.io (diagramas) |

Antes de adoptar una tecnología, se valida su compatibilidad con los requisitos de seguridad, rendimiento, mantenimiento, despliegue y licenciamiento pertinentes.

---

## 12. Documentación del software

La documentación debe mantenerse coherente con el sistema y estar disponible para las personas que la necesitan. Su extensión se adapta al riesgo, la complejidad y las necesidades del equipo.

| Documento | Función |
|---|---|
| **Documento de Requisitos (SRS)** | Define qué debe hacer el sistema, sus restricciones, atributos de calidad y criterios de aceptación. Sirve de referencia para diseño, implementación y pruebas. |
| **Diseño Técnico** | Explica arquitectura, componentes, datos, interfaces, decisiones y aspectos técnicos relevantes para construir y evolucionar el sistema. |
| **Manual de Usuario** | Guía a los usuarios en tareas, flujos, permisos y resolución de situaciones habituales. |
| **Manual Técnico** | Describe instalación, configuración, operación, mantenimiento, soporte y recuperación para personal técnico autorizado. |
| **Casos de Prueba** | Especifican escenarios, precondiciones, datos, pasos y resultados esperados para validar el comportamiento del sistema. |

Los documentos deben indicar versión o fecha y responsable cuando el proceso lo requiera. Un repositorio puede conservar requisitos, decisiones, modelos, casos de prueba y guías junto con los cambios del producto.

---

## 13. Métricas del software

Las métricas permiten observar calidad y evolución, siempre que se definan de forma consistente. Un indicador aislado no explica por sí solo la causa de un problema ni debe usarse sin contexto.

| Métrica | Descripción | Ejemplo |
|---|---|---|
| **Tiempo de respuesta** | Tiempo entre una solicitud y la respuesta del sistema; puede medirse por percentiles y tipo de operación. | Una búsqueda responde en 1,5 segundos en la condición de carga especificada. |
| **Tasa de errores (bugs)** | Cantidad de defectos registrados, idealmente segmentada por severidad, módulo y periodo. | Se encontraron 3 bugs en el módulo de reportes durante el ciclo de pruebas. |
| **Disponibilidad** | Porcentaje del tiempo medido durante el que el servicio está operativo conforme a una definición acordada. | Objetivo mensual de disponibilidad de 99,9 %. |
| **Satisfacción del usuario** | Percepción recogida con encuestas u otros métodos y expresada con una escala y población definidas. | 90 % de respuestas favorables en la encuesta posterior a la entrega. |
| **Cobertura de pruebas** | Proporción de elementos ejecutados por pruebas; por ejemplo, líneas o ramas cubiertas. No equivale a demostrar ausencia de defectos. | 85 % de cobertura de líneas en el código medido, junto con análisis de casos y riesgos pendientes. |

Para que una métrica sea útil, se documentan fórmula, fuente, periodo, alcance y limitaciones. Se priorizan medidas que ayuden a tomar decisiones y mejorar el producto, no solo a cumplir un número.

---

## 14. Procedimiento completo paso a paso (resumen)

Los pasos **1 a 7** cubren el trabajo central de requisitos, diseño, desarrollo y pruebas:

1. **Identificar el problema y los objetivos del sistema.** Precisar quién necesita una solución, qué resultado se espera y cómo se reconocerá el éxito.
2. **Recopilar y analizar los requisitos con los usuarios.** Aclarar necesidades, restricciones, reglas y prioridades con las partes interesadas.
3. **Definir el alcance y documentar los requisitos.** Establecer límites, criterios verificables, supuestos y exclusiones; revisar y aprobar la línea base correspondiente.
4. **Diseñar la arquitectura, base de datos e interfaces.** Traducir requisitos en componentes, datos, interacciones y decisiones técnicas.
5. **Seleccionar tecnología y herramientas adecuadas.** Contrastar opciones con requisitos, capacidades del equipo, seguridad, costos y operación.
6. **Desarrollar los módulos según el diseño.** Codificar en cambios controlados, aplicar estándares y revisar la implementación.
7. **Realizar pruebas (unitarias, integración, sistema, aceptación).** Ejecutar los casos, registrar defectos, verificar correcciones y documentar resultados.
8. **Implementar el sistema en el entorno de producción.** Preparar y desplegar una versión aprobada siguiendo el procedimiento operativo aplicable.
9. **Capacitar a los usuarios y entregar el sistema.** Proporcionar orientación, documentación y canales de soporte.
10. **Monitorear el sistema y corregir errores.** Observar operación, incidencias y comportamiento frente a los objetivos acordados.
11. **Mantener y mejorar el sistema continuamente.** Priorizar correcciones, actualizaciones y nuevas necesidades con control de cambios.
12. **Documentar todo el proceso y los resultados.** Conservar decisiones, versiones, pruebas, incidencias y aprendizajes para facilitar operación y evolución.

Aunque se enumeran en orden, la retroalimentación puede hacer que el equipo revise requisitos, diseño o código antes de cerrar un incremento.

---

## 15. Ejemplo práctico: sistema web de gestión de inventarios

### Fase 1 — Requisitos

Se identifican usuarios, por ejemplo, administrador, encargado de almacén y personal de ventas. El alcance funcional incluye:

- Registrar, consultar y actualizar productos y sus datos relevantes.
- Registrar **entradas** y **salidas** de inventario con cantidad, fecha y motivo.
- Consultar existencias actuales y detectar productos por debajo de un umbral definido.
- Generar reportes de movimientos y existencias por periodo o producto.
- Aplicar permisos de modo que solo personal autorizado modifique datos.

Se definen reglas de negocio (por ejemplo, si se permiten existencias negativas), criterios de aceptación y requisitos no funcionales medibles de seguridad, disponibilidad y rendimiento. **Entregable:** documento de requisitos con alcance, actores, reglas, prioridades y casos de aceptación.

### Fase 2 — Diseño

Se propone una arquitectura web **MVC**, sujeta a validar que satisface las necesidades. Se definen módulos y contratos entre interfaz, lógica de negocio y persistencia. El modelo de datos puede incluir `usuarios`, `productos`, `proveedores` y `movimientos_inventario`; cada movimiento referencia el producto y conserva tipo, cantidad, fecha y usuario responsable. La existencia actual puede calcularse desde movimientos o mantenerse como dato derivado con reglas transaccionales explícitas.

Se diseñan interfaces para consultar productos, registrar movimientos y generar reportes, además de diagramas de casos de uso, modelo de datos y secuencia para el registro de una salida. **Entregable:** documento de diseño con arquitectura, modelo, interfaces y decisiones.

### Fase 3 — Desarrollo / codificación

Se implementan los módulos de **usuarios**, **productos**, **proveedores**, **ventas** y **reportes**, además de la lógica necesaria para entradas, salidas y control de stock. El acceso a operaciones se valida en el servidor; las escrituras relacionadas se realizan de forma consistente y los datos de entrada se validan.

El equipo trabaja con Git, commits pequeños y revisiones de código. Los módulos incorporan pruebas unitarias para reglas críticas, como evitar una salida superior a las existencias disponibles si esa regla forma parte del requisito. **Entregable:** código versionado, pruebas automatizadas y configuración de construcción documentada.

### Fase 4 — Pruebas

- **Unitarias:** cálculo de existencias, validación de cantidades y reglas de movimientos.
- **Integración:** persistencia de una entrada y actualización consistente de la existencia; asociación entre productos, usuarios y movimientos.
- **Sistema:** flujo completo de consulta, movimiento y generación de reporte con permisos y requisitos de calidad.
- **Aceptación:** usuarios representativos confirman que pueden registrar entradas y salidas, consultar stock y obtener los reportes acordados.

Se prueban también entradas inválidas, intentos de acceso sin permiso y escenarios límite. **Entregable:** informe de pruebas que relaciona resultados con requisitos, defectos y riesgos residuales.

---

## 16. Errores comunes y cómo evitarlos

| Error común | Cómo evitarlo |
|---|---|
| Programar sin analizar requisitos | Realizar un buen levantamiento y análisis; acordar alcance y criterios de aceptación antes de implementar cada capacidad. |
| No documentar el sistema | Documentar desde el inicio hasta el final y mantener los artefactos relevantes alineados con el producto. |
| No realizar pruebas suficientes | Aplicar pruebas en todas las fases: revisar requisitos y diseño, probar unidades e integración y validar el sistema y la aceptación. |
| No usar control de versiones | Usar Git y un repositorio compartido, definir prácticas de ramas y revisar los cambios. |
| Ignorar la seguridad | Incorporar controles de seguridad en requisitos, diseño, codificación y pruebas; revisar permisos, entradas y datos sensibles. |
| No mantener el sistema | Planificar mantenimiento continuo, responsables, monitoreo, gestión de defectos y actualización de dependencias. |
| No considerar al usuario final | Involucrar usuarios y validar con ellos prototipos, criterios y resultados de aceptación. |
| Elegir tecnología inadecuada | Evaluar alternativas contra requisitos, competencias, seguridad, costos y necesidades de operación antes de decidir. |
| Falta de planificación | Definir alcance, prioridades, tiempo, recursos, riesgos y criterios de salida; revisar el plan cuando cambien las condiciones. |

---

## 17. Conclusiones finales y conclusión general

### Conclusiones clave

- El desarrollo de software es un proceso ordenado y sistemático que inicia con el análisis de requisitos.
- Seguir una metodología adecuada, como Ágil o Cascada, mejora la calidad, el tiempo y la gestión del proyecto cuando se ajusta al contexto y a la incertidumbre.
- Las pruebas son esenciales para aportar evidencia de que el software funciona correctamente y cumple con las necesidades y criterios acordados.
- La documentación permite comprender, usar, mantener y dar soporte al sistema a lo largo del tiempo.
- El uso de buenas prácticas, herramientas adecuadas y trabajo en equipo ayuda a construir software de calidad, seguro y confiable.
- Desarrollar software no es solo escribir código: es comprender problemas, diseñar soluciones y generar valor.
- Un proceso coherente contribuye a que el software sea de calidad, eficiente y escalable según objetivos verificables.
- La planificación, el análisis y el diseño son tan importantes como la programación.
- Las pruebas y la evaluación contribuyen a sistemas confiables y centrados en el usuario.

### Conclusión general

Un proceso de desarrollo eficaz conecta de forma trazable las necesidades de las personas con una solución técnica comprobable. Requisitos claros reducen ambigüedades; un diseño adecuado orienta una implementación mantenible; prácticas disciplinadas de codificación y control de versiones facilitan la colaboración; y pruebas planificadas detectan fallos y validan resultados. La combinación de estas prácticas, junto con seguridad, documentación y mejora continua, ofrece una base sólida para desarrollar software útil y sostenible.
