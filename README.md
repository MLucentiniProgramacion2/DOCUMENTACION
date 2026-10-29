# DOCUMENTACION

**Proyecto integrador · Programación II 2026 · Universidad de Mendoza**

Máximo Lucentini

Documentación general del sistema de reserva de turnos con profesionales. El sistema está formado por una app Android (Kotlin Multiplatform) y dos servicios backend en Java, cada uno con su propia base de datos PostgreSQL, que se integran con el servicio de la cátedra por REST, Redis y Kafka.

## Repositorios del sistema

| Repositorio | Contenido |
| --- | --- |
| [catalogo-service](https://github.com/MLucentiniProgramacion2/catalogo-service) | Servicio de catálogo: copia local de categorías, profesionales y horarios, sincronizada con la cátedra, y búsqueda sobre esos datos |
| [turnos-service](https://github.com/MLucentiniProgramacion2/turnos-service) | Servicio de turnos: usuarios, autenticación (emite el JWT), disponibilidad y proceso de reserva |
| [turnos-app-kmp](https://github.com/MLucentiniProgramacion2/turnos-app-kmp) | App Android en Kotlin Multiplatform |
| DOCUMENTACION (este repositorio) | Documentación general del sistema |

## Dónde está cada documentación

**En este repositorio** está lo que abarca a todo el sistema o a más de un componente:

| Documento | Contenido |
| --- | --- |
| [PLAN_DE_TRABAJO.md](PLAN_DE_TRABAJO.md) | Las cuatro etapas del proyecto |
| [CRONOGRAMA.md](CRONOGRAMA.md) | Las tareas de cada día |
| Arquitectura del sistema (etapa 4) | Diagrama con la app, los dos servicios, sus bases y las integraciones con la cátedra |
| Contratos entre servicios (etapa 3) | Operaciones que turnos consume de catálogo, DTO, autenticación y errores |
| Seguridad (etapa 4) | JWT de usuario, token técnico de servicio y autorización entre componentes |
| Ejecución del sistema completo (etapa 4) | Orden y pasos para levantar los dos servicios y la app juntos |

**En cada repositorio** está la documentación específica de ese servicio o de la app:

- README con requisitos, configuración, ejecución y cómo correr los tests;
- casos de uso (`docs/use-cases/`);
- decisiones técnicas como ADR (`docs/adr/`);
- modelo de datos del servicio;
- estrategias propias del servicio: sincronización completa e incremental en catálogo, y máquina de estados de la reserva en turnos, con su idempotencia y recuperación.
