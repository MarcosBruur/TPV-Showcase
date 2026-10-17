# Decisiones técnicas

[Volver a la presentación](../README.md)

Esta sección explica las decisiones observables en el código. Sus motivos se presentan como análisis técnico de la implementación, no como un registro histórico de decisiones del autor.

| Decisión observada | Beneficio | Costo o límite |
| --- | --- | --- |
| SPA Vue y API REST | Separa interacción y reglas del servidor | Requiere coordinar sesión, navegación y errores |
| Monolito modular Django | Reúne dominios relacionados con transacciones y un ORM común | Los módulos comparten proceso y base |
| SQLite | Simplifica una instalación local | Tiene límites de concurrencia y no ofrece bloqueo de filas como otros motores |
| Pinia para sesión y carrito | Centraliza estado usado entre pantallas | El carrito sin registrar vive en memoria |
| Estados explícitos de venta | Permite separar atención y cobro | Exige reconciliar stock al editar y cobrar |
| Datos históricos por renglón | Conserva el contexto de la operación | Duplica algunos datos del catálogo deliberadamente |
| Baja lógica del producto | Retira productos sin borrar su historial operativo | Las consultas deben distinguir activos e inactivos |
| Cookie HttpOnly para refresh | Restringe el acceso del JavaScript al token de renovación | El access token sigue persistido en localStorage |
| Reserva durable de serie fiscal | Coordina emisiones y resultados inciertos | La recuperación depende del estado y del servicio externo |
| Build integrado en recursos Django | Permite entregar la interfaz junto al backend | El despliegue debe mantener sincronizados plantilla y recursos |

## Límites conocidos

La configuración actual utiliza SQLite; migrar a PostgreSQL exige cambiar configuración y dependencias y validar comportamiento. Las transacciones IMMEDIATE y el timeout mitigan contención, pero no prueban capacidad para una carga determinada.

La numeración comercial de tickets se apoya en el último identificador, sin un contador transaccional dedicado. No debe confundirse con la coordinación de series de facturación.

El cálculo tributario de venta y los parámetros de emisión fiscal pertenecen a circuitos distintos. La implementación revisada calcula el impuesto persistido de venta con tasa cero; eso no permite concluir una cobertura tributaria general.

No se verificaron métricas de rendimiento, disponibilidad, recuperación ante desastre ni un despliegue productivo. Tampoco se presenta la interfaz responsive como validación en todos los dispositivos.

## Evolución técnica posible

Las siguientes son propuestas, no compromisos ni funciones terminadas: evaluar otro motor bajo carga real; fortalecer numeración concurrente; revisar persistencia de sesión y CSP; ampliar automatización de pruebas de interfaz; y formalizar despliegue, respaldo y observabilidad.
