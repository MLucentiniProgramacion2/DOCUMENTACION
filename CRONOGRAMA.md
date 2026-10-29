# Cronograma

**Proyecto integrador · Programación II 2026**

Máximo Lucentini · Ver también el [plan de trabajo](PLAN_DE_TRABAJO.md)

## Etapa 2 · Catálogo y sincronización

| Fecha | Día | Tarea |
| --- | --- | --- |
| 30/10 | Vie | Puertos y adaptadores de persistencia del catálogo, y mappers entre entidad y dominio |
| 31/10 | Sáb | Sincronización completa por snapshot (CU-02): validación de referencias, una sola transacción, reintentos y registro del estado |
| 1/11 | Dom | Inicialización del catálogo al arrancar con la base vacía (CU-01) y sus tests |
| 2/11 | Lun | Listado de categorías (CU-06) |
| 3/11 | Mar | Búsqueda de profesionales (CU-05): filtros por categoría, nombre y estado habilitado |
| 4/11 | Mié | Búsqueda de profesionales (CU-05): filtro por disponibilidad y tests |
| 5/11 | Jue | Consulta del estado de sincronización (CU-09) y sincronización manual para administrador (CU-08) |
| 6/11 | Vie | Recepción de `CatalogUpdated` por Kafka (CU-03): registro de eventos procesados y exclusión mutua entre sincronizaciones |
| 7/11 | Sáb | Sincronización incremental (CU-04): lectura de cambios desde Redis y una transacción por versión |
| 8/11 | Dom | Sincronización incremental (CU-04): detección de discontinuidad, paso a snapshot y tests |
| 9/11 | Lun | Arranque con el catálogo ya cargado y comprobación periódica de la versión remota |
| 10/11 | Mar | Agenda vigente para turnos (CU-07), protegida con el token técnico de servicio |
| 11/11 | Mié | Tests de punta a punta de snapshot, incremental y recuperación. Documentación de la sincronización y la idempotencia en el repositorio de catálogo |

## Etapa 3 · Turnos y reservas

| Fecha | Día | Tarea |
| --- | --- | --- |
| 12/11 | Jue | Reglas de arquitectura con ArchUnit y validación del esquema en turnos |
| 13/11 | Vie | Dominio y tablas del proceso de reserva, con su máquina de estados |
| 14/11 | Sáb | Cliente REST de la cátedra en turnos y token técnico de servicio hacia catálogo |
| 15/11 | Dom | Consulta de turnos disponibles (CU-03) |
| 16/11 | Lun | Iniciar reserva (CU-04): hold y confirmación inicial por REST, con control de pedidos repetidos |
| 17/11 | Mar | Flujo del teléfono por Kafka (CU-05, CU-06): recepción del pedido y envío del teléfono |
| 18/11 | Mié | Procesamiento del resultado (CU-07): confirmación, rechazo, expiración, inválido y cancelación, con deduplicación por `eventId` |
| 19/11 | Jue | Estado de un proceso (CU-08), mis reservas (CU-09) y cancelación de una reserva propia (CU-10) |
| 20/11 | Vie | Reconciliación de procesos pendientes al arrancar y periódica (CU-11). Consulta administrativa (CU-12, opcional) |
| 21/11 | Sáb | Tests de una reserva confirmada, otra que expira y un evento duplicado o tardío. Modelo de datos y estados de la reserva en el repositorio de turnos; contratos entre los dos servicios en DOCUMENTACION |

## Etapa 4 · App KMP, robustez y documentación

| Fecha | Día | Tarea |
| --- | --- | --- |
| 22/11 | Dom | App: proyecto base, conexión con los servicios, registro y login |
| 23/11 | Lun | App: búsqueda de profesionales con filtros y categorías |
| 24/11 | Mar | App: disponibilidad, reserva con ingreso del teléfono y estado del proceso |
| 25/11 | Mié | App: mis reservas y cancelación. Timeouts, reintentos limitados y comportamiento ante caídas |
| 26/11 | Jue | Documentación general en DOCUMENTACION (diagrama de arquitectura, seguridad y ejecución del sistema completo) y README final de cada repositorio |
| 27/11 | Vie | Pruebas de punta a punta de todas las evidencias del enunciado |
