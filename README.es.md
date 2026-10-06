<div align="center">

# AutoPin-CS

[English](README.md) · [中文](README.zh.md) · Español · [Deutsch](README.de.md) · [Français](README.fr.md)

</div>

> **Este repositorio es un escaparate, no una publicación de código.** AutoPin-CS es un proyecto privado, así que aquí no hay código: solo qué hace, cómo está construido y qué aspecto tiene. Si quieres hablar de él, escríbeme desde mi [perfil de GitHub](https://github.com/frommmmmg).

**Un planificador y gestor de flota para operaciones de contenido en redes sociales a gran escala.** Un servidor central reparte trabajo a una flota de clientes Windows, y una capa de agentes de IA permite que un operador maneje todo el sistema con lenguaje natural.

![Arquitectura de AutoPin-CS](assets/autopin-architecture.svg)

**Puntos clave**

- **Planificación y administración centrales.** Un servicio Flask/uWSGI con MySQL gestiona tareas, clientes, pedidos y analítica.
- **Una flota de clientes con demonios en Python** que ejecutan flujos de automatización del navegador, con varios modos de operación según el tipo de trabajo.
- **Lanzamientos seguros.** Cada actualización de cliente se construye como paquete completo, se registra, **se verifica en una máquina canario real** y solo entonces se activa, con reversión lista. El despliegue total sin canario está prohibido por diseño.
- **Operaciones como habilidades de agente.** Dar de alta una máquina nueva, diagnosticar un cliente remoto, revisar los planificadores y preparar una versión están escritos como habilidades que un agente de IA puede ejecutar con una instrucción de una línea.
- **Disciplina de ingeniería por escrito.** ADR, contratos del sistema, manuales operativos y un proceso de registro de errores que busca defectos hermanos antes de cerrar uno.
- **Escala.** Miles de archivos entre servidor, cliente, control de escritorio, despliegue y pruebas.

**Tecnología:** Python · Flask · uWSGI · MySQL · servicios de Windows · automatización del navegador tipo Playwright · FFmpeg

## Capturas

*No se incluyen capturas a propósito: la consola de administración muestra datos de clientes y cuentas.*

## Cómo funciona

![Una versión solo se activa cuando una máquina canario real supera todas las puertas.](assets/autopin-release-gate.svg)
*Una versión solo se activa cuando una máquina canario real supera todas las puertas.*

![El operador habla en lenguaje natural; el agente ejecuta un manual fijo y comprueba la evidencia.](assets/autopin-agent-loop.svg)
*El operador habla en lenguaje natural; el agente ejecuta un manual fijo y comprueba la evidencia.*

---

<div align="center">

<sub>Las capturas usan solo datos de ejemplo o públicos. © Todos los derechos reservados. Las descripciones pueden citarse con atribución; el software no se puede redistribuir.</sub>

</div>
