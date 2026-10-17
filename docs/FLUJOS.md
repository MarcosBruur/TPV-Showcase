# Flujos de negocio

[Volver a la presentación](../README.md)

## Modalidades y operadores

| Modalidad | Vendedor | Cajero | Administrador |
| --- | --- | --- | --- |
| SINGLE | Registra ventas con caja central abierta | Cobra ventas registradas en su turno | TPV, cobros y administración |
| MULTIPLE | Consulta inventario | Vende y cobra desde TPV | TPV y administración |

Cada turno pertenece a un usuario. La modalidad no representa un modelo de cajas compartidas con varios participantes. Cambiarla requiere cerrar las cajas; para pasar a MULTIPLE también deben resolverse las ventas registradas.

## Registro y cobro en SINGLE

```mermaid
sequenceDiagram
    actor V as Vendedor
    participant UI as Interfaz
    participant API as API de ventas
    participant DB as Persistencia
    actor C as Cajero
    V->>UI: Carga productos y nombre del cliente
    UI->>API: Registrar venta
    API->>API: Validar rol, modalidad, caja y stock
    API->>DB: Guardar REGISTRADA y descontar stock
    DB-->>UI: Venta pendiente de cobro
    C->>UI: Abre pendiente y confirma cantidades y pago
    UI->>API: Cobrar venta
    API->>API: Validar turno y estado
    API->>DB: Reconciliar stock y guardar COMPLETADA
    DB-->>UI: Ticket y resultado del cobro
```

El descuento de stock al registrar actúa como reserva. Al cobrar, el sistema devuelve la reserva anterior y descuenta las cantidades finales dentro de una transacción. Los productos que permanecen en la operación conservan sus valores históricos; los agregados toman los valores vigentes.

Una venta directa completada también requiere turno abierto. La anulación administrativa restituye stock, incluso si la venta todavía estaba registrada.

## Caja y compras

El fondo inicial se combina con ventas cobradas en efectivo y egresos activos en efectivo pagados desde caja. El cierre compara el efectivo informado con ese saldo esperado.

**Saldo esperado = fondo inicial + ventas en efectivo − egresos de efectivo computables.**

Las compras activas ingresan mercadería y pueden actualizar el costo. Los borradores no ingresan stock. Anular una compra revierte el ingreso.

## Emisión fiscal

```mermaid
flowchart TD
    V["Venta COMPLETADA"] --> P["Validar operador y datos fiscales"]
    P --> R["Reservar serie y guardar PREPARANDO"]
    R --> E["Persistir número y estado ENVIANDO"]
    E --> W["Solicitar autorización WSFE"]
    W --> A["AUTORIZADA: guardar resultado y generar PDF"]
    W --> X["RECHAZADA: conservar motivo"]
    W --> I["INCIERTA: requiere confirmación"]
    I --> C["Consultar autorización existente"]
    C --> A
    C --> I
```

Es un esquema de los caminos principales, no la totalidad de las transiciones. También puede rechazarse una preparación interrumpida antes de enviar.

WSAA proporciona acceso al servicio fiscal y WSFE gestiona la autorización. El backend conserva estado y resultado para resolver respuestas inciertas por consulta. Las llamadas externas no se mantienen dentro de una transacción SQL prolongada.

El ticket comercial, el presupuesto informativo y la factura autorizada son documentos distintos. Generar un presupuesto no registra una venta ni reserva stock.
