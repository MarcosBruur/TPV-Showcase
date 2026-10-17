# Mapa conceptual de la API

[Volver a la presentación](../README.md)

Las rutas se documentan como mapa de responsabilidades de la implementación privada. Este repositorio no publica un servidor ni credenciales. No es una especificación exhaustiva de cuerpos, respuestas y permisos.

| Área | Rutas representativas | Responsabilidad |
| --- | --- | --- |
| Sesión | /api/auth/login/, /refresh/, /logout/, /me/ bajo /api/auth/ | Inicio, renovación, cierre y perfil |
| Usuarios | /api/auth/users/ | Administración de operadores |
| Catálogo | /api/pos/categories/, /api/pos/products/ | Consulta y mantenimiento |
| Clientes comerciales | /api/pos/customers/ | Clientes del dominio de ventas |
| Inventario | /api/pos/products/{id}/adjust_stock/ | Ajustes autorizados |
| Caja | /api/pos/cash-shifts/, /api/pos/cash-shifts/current/ | Turnos e información de caja |
| Apertura y cierre | /api/pos/cash-shifts/open_shift/, /api/pos/cash-shifts/{id}/close_shift/ | Operación del turno |
| Ventas | /api/pos/sales/, /api/pos/sales/registered/ | Registro, historial y pendientes |
| Cobro y anulación | /api/pos/sales/{id}/collect/, /api/pos/sales/{id}/cancel/ | Cambios de estado con reglas de negocio |
| Presupuesto | /api/pos/sales/budget_pdf/ | PDF informativo |
| Egresos | /api/pos/expense-categories/, /api/pos/expenses/ | Compras y gastos |
| Indicadores | /api/pos/dashboard/ | Métricas administrativas |
| Comercio | /api/config/ | Configuración e identidad comercial |
| Catálogos fiscales | /api/facturacion/catalogos/ | Opciones para la emisión |
| Facturación de venta | /api/facturacion/ventas/{id}/ | Consulta y solicitud de emisión |
| Recuperación fiscal | /api/facturacion/ventas/{id}/consultar/ | Confirmación de un resultado |
| PDF fiscal | /api/facturacion/ventas/{id}/pdf/ | Descarga autenticada |

## Criterios del contrato

Los precios de una venta los determina el servidor. Los permisos dependen de rol, modalidad y operación; conocer una ruta no concede acceso.

Las mutaciones del ciclo de ventas se realizan mediante acciones específicas. El ViewSet de ventas no habilita actualización y borrado genéricos.

Los listados incorporan paginación y filtros según el recurso. Algunas respuestas agregan totales del conjunto filtrado, independientes de la página visible.
