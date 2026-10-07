<div align="center">

# AutoPin-CS

[English](README.md) · [中文](README.zh.md) · Español · [Deutsch](README.de.md) · [Français](README.fr.md)

[GitHub @frommmmmg](https://github.com/frommmmmg)

</div>

> **Este repositorio es un escaparate, no una publicación de código.** AutoPin-CS no es de código abierto, así que aquí no hay código: solo qué hace, cómo está construido y qué aspecto tiene. Si quieres hablar de él, escríbeme desde mi [perfil de GitHub](https://github.com/frommmmmg).

**Un planificador y gestor de flota para operaciones de contenido en redes sociales a gran escala.** Un servidor central reparte trabajo a una flota de clientes Windows, y una capa de agentes de IA permite que un operador maneje todo el sistema con lenguaje natural.

Operar una gran flota de clientes de escritorio desatendidos es sobre todo un problema de operaciones. ¿Cómo lanzas una versión nueva sin tumbar la flota? ¿Cómo pones en marcha una máquina nueva siempre de la misma manera? ¿Cómo encuentras la única máquina que falla en silencio? AutoPin-CS es el sistema construido alrededor de esas preguntas, y la mayor parte de su código sirve para que las respuestas sean repetibles, comprobables y recuperables.

![Arquitectura](assets/autopin-architecture.svg)

| | |
|---|---|
| **Mi papel** | Único diseñador y responsable del servidor, el cliente, el control de escritorio, las herramientas de despliegue y la documentación |
| **Estado** | En producción. Es un sistema comercial privado, así que no hay sitio público |
| **Escala** | Unos 1.300 archivos Python, unos 620 archivos de pruebas, más de 400 registros de decisiones de arquitectura y unos 290 análisis de errores |
| **Tecnología** | Python · Flask · uWSGI · MySQL · servicios de Windows · automatización del navegador · FFmpeg |

### Qué hace

**Servidor**
- **Planificación y administración centrales.** Un servicio Flask/uWSGI con MySQL gestiona tareas, pedidos, el registro de clientes, registros y resultados de tareas, copias de seguridad y analítica.
- **Contratos y disciplina de esquemas.** El esquema de cada tabla tiene versión y pertenece a un módulo, y la comprobación de disponibilidad retiene los planificadores hasta que la base de datos está en el estado esperado.

**Flota de clientes**
- **Demonios en Python con varios modos de operación**, que ejecutan flujos de automatización del navegador: un trabajador de larga duración, un modo de tarea única dirigido por el servidor y otros tipos de tareas.
- **Un agente de escritorio que atraviesa el aislamiento de sesiones de Windows.** Puede ver y manejar el escritorio real del usuario, de modo que el diagnóstico remoto incluye capturas y control de procesos en lugar de suposiciones a partir de los registros.
- **Preparación de vídeo.** Un flujo por lotes verificado que normaliza los vídeos a un perfil H.264/AAC conservador que aceptan incluso combinaciones antiguas de Windows y navegador.

**Ingeniería de versiones**
- **Una puerta de versiones que nunca se relaja.** Cada actualización de cliente se construye como paquete completo, se registra inactiva, **se verifica en una máquina canario real** y solo entonces se activa, con reversión lista. Una compilación correcta, un paquete que se descomprime o un único latido no cuentan como éxito.

**Una capa de agentes de IA**
- **Operaciones como habilidades de agente.** Poner en marcha una máquina nueva, diagnosticar un cliente remoto, revisar los planificadores, clasificar cuentas con problemas y preparar una versión están escritos como habilidades que un agente de IA puede ejecutar. Cada habilidad es una secuencia fija de pasos con puertas de verificación y lectura de evidencias, iniciada con una frase del operador.

## Capturas

*No se incluyen capturas a propósito: la consola de administración muestra datos de clientes y cuentas.*

## Cómo funciona

![Una versión solo se activa cuando una máquina canario real supera todas las puertas.](assets/autopin-release-gate.svg)
*Una versión solo se activa cuando una máquina canario real supera todas las puertas.*

![El operador habla en lenguaje natural; el agente ejecuta un manual fijo y comprueba la evidencia.](assets/autopin-agent-loop.svg)
*El operador habla en lenguaje natural; el agente ejecuta un manual fijo y comprueba la evidencia.*

<!--notes-->
## Notas de ingeniería

- **Las decisiones están escritas, y son muchas.** Más de 400 registros de decisiones de arquitectura explican por qué las cosas son como son, muchos de ellos sobre versionar y asignar propietario a los esquemas de la base de datos para que el arranque y las migraciones sean predecibles.
- **Cada error tiene un análisis y una búsqueda de hermanos.** Unos 290 registros de errores nombran la causa raíz, la prueba de regresión y la búsqueda del mismo defecto en otros sitios. Un error solo se cierra cuando esa búsqueda está hecha.
- **Evidencia en lugar de esperanza.** Una versión solo cuenta como buena con evidencia de máquina real: árbol de procesos estable, sesión de escritorio, éxito persistido y ningún fallo o reversión posterior. Las comprobaciones del paquete incluyen listas de miembros, sumas ZIP, longitud, SHA-256 y compatibilidad con el intérprete más antiguo de la flota.
- **La recuperación se diseña antes de necesitarla.** Las rutas de reversión, un camino de restauración verificado para la máquina canario y un manual de recuperación con instalador completo están escritos, y los registros del fallo original se conservan en lugar de sobrescribirse.
- **Los secretos no entran en el código ni en la línea de comandos.** Las credenciales viven en el llavero del sistema operativo y se entregan a las herramientas en el momento de usarlas.
- **Los agentes siguen las mismas reglas que las personas.** Las habilidades de los agentes están versionadas en el repositorio, llevan las mismas reglas de seguridad (no saltarse el canario, no adivinar de qué punto de entrada viene un registro) y deben terminar confirmando que el cambio se ha subido.

**Otras muestras:** [AffProof](https://github.com/frommmmmg/AffProof-showcase) · [Tonu.app](https://github.com/frommmmmg/Tonu.app-showcase) · [AffiliateScraper](https://github.com/frommmmmg/AffiliateScraper-showcase)

---

<div align="center">

<sub>Las capturas usan solo datos de ejemplo o públicos. © Todos los derechos reservados. Las descripciones pueden citarse con atribución; el software no se puede redistribuir.</sub>

</div>
