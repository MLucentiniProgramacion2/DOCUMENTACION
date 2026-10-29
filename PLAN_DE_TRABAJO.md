# Plan de trabajo

**Proyecto integrador · Programación II 2026 · Universidad de Mendoza**

Máximo Lucentini

El sistema permite reservar turnos con profesionales. Está formado por una app Android (Kotlin Multiplatform) y dos servicios backend en Java, cada uno con su propia base de datos, que se integran con el servicio de la cátedra por REST, Redis y Kafka. El trabajo se divide en cuatro etapas, y cada una es un milestone en GitHub.

El detalle día por día está en [CRONOGRAMA.md](CRONOGRAMA.md).

La documentación general del sistema vive en este repositorio, y la específica de cada servicio y de la app, en su propio repositorio. El criterio está en el [README](README.md).

## 1. Análisis y base de los servicios

Dejar los dos servicios funcionando con la seguridad resuelta, para después solo sumar lógica de negocio.

- Casos de uso de los dos servicios: catálogo (CU-01 a CU-09) y turnos (CU-01 a CU-12).
- Infraestructura de cada servicio: Docker Compose con su propio PostgreSQL y su ADR.
- Base JHipster de turnos, que es el dueño de los usuarios: registro, login y emisión del JWT.
- Base JHipster de catálogo, sin usuarios: solo valida el JWT que emite turnos.
- GitHub Actions en los dos repositorios, para que cada PR compile y corra los tests automáticamente.

**Terminada cuando:** un usuario se registra y se loguea en turnos, y catálogo acepta ese token y rechaza uno inválido.

## 2. Catálogo y sincronización

Implementar los 9 casos de uso del catálogo en arquitectura hexagonal.

- Reglas de arquitectura verificadas con ArchUnit en cada build.
- Dominio y tablas del catálogo y del estado de sincronización, con Liquibase.
- Cliente REST de la cátedra para obtener el snapshot.
- Sincronización completa por snapshot en una sola transacción, e inicialización al arrancar (CU-02, CU-01).
- Sincronización automática al recibir `CatalogUpdated`, al arrancar y con una comprobación periódica por si se pierde un aviso, con protección contra mensajes duplicados (CU-03).
- Sincronización incremental versión por versión, pasando a snapshot si hay un hueco (CU-04).
- Búsqueda local con filtros por categoría, nombre, estado habilitado y disponibilidad, y listado de categorías (CU-05, CU-06).
- Agenda vigente para turnos, protegida con un token técnico de servicio (CU-07).
- Sincronización manual y consulta del estado de sincronización (CU-08, CU-09).

**Terminada cuando:** funcionan una inicialización por snapshot, una actualización incremental y una recuperación tras una discontinuidad, con sus tests.

## 3. Turnos y reservas

Implementar en arquitectura hexagonal los casos de uso de turnos, para que un usuario pueda reservar de punta a punta.

- Reglas de arquitectura con ArchUnit, igual que en catálogo.
- Cliente REST de la cátedra en turnos y token técnico de servicio para consultar a catálogo.
- Disponibilidad: agenda vigente del catálogo menos las ocupaciones de la cátedra (CU-03).
- Máquina de estados de la reserva, asociada al usuario.
- Hold y confirmación por REST (CU-04), y el flujo del teléfono por Kafka con sus resultados (CU-05 a CU-07).
- Estado de un proceso, y ver y cancelar las reservas propias sin acceso a las de otros usuarios (CU-08 a CU-10).
- Retomar los procesos pendientes al reiniciar (CU-11).
- Consulta administrativa de solo lectura (CU-12, opcional).

**Terminada cuando:** se completan una reserva confirmada y otra que expira, y un evento duplicado o tardío no altera el estado final.

## 4. App KMP, robustez y documentación

- App Android con registro, login, búsqueda, reserva, mis reservas y cancelación.
- Timeouts, reintentos limitados y comportamiento ante caídas de la cátedra o del otro servicio.
- Documentación que pide el enunciado, repartida así:
  - en el repositorio DOCUMENTACION, la general: diagrama de arquitectura, contratos entre los dos servicios, seguridad y ejecución del sistema completo;
  - en cada repositorio, la específica: README con configuración, ejecución y tests, modelo de datos, y estrategias de sincronización, idempotencia y estados de la reserva.
- Evidencias del enunciado preparadas para la presentación.

**Terminada cuando:** el flujo completo funciona desde la app Android y cada evidencia del enunciado se puede mostrar.
