# Estado y validación

[Volver a la presentación](../README.md)

**Fecha de revisión documental: 16 de octubre de 2026.**

La documentación se elaboró a partir de la estructura, dependencias, modelos, rutas, configuración y flujos del proyecto privado disponible localmente. Incluye cambios locales visibles; no se limita a un release etiquetado.

## Qué se puede afirmar

- Existen implementaciones para catálogo, ventas, cobros, turnos, compras, gastos, usuarios y configuración comercial.
- Hay integración fiscal en la interfaz y en la API, además de clientes de consola WSAA/WSFE.
- Existen pruebas de backend para dominios de autenticación, configuración, ventas y facturación.
- También hay archivos de pruebas de servicios del frontend; package.json no declara un script de tests.
- El frontend declara un comando de compilación con Vite.

## Qué no se verificó en esta preparación

No se ejecutaron la suite de la aplicación ni el build para elaborar este repositorio documental. No se comprobó la aplicación de migraciones en una instalación concreta, la disponibilidad de servicios fiscales o un despliegue público.

No se publican porcentajes de cobertura, tiempos de respuesta, usuarios concurrentes ni resultados de producción sin evidencia.

## Material visual

Se incorporaron cuatro capturas: punto de venta, inventario, cobros y caja. La portada y la [galería visual](../assets/screenshots/README.md) las presentan con descripciones. Las capturas adicionales son opcionales; el [guion de demo](DEMO.md) propone un recorrido. La incorporación de imágenes no implica una validación funcional de la aplicación.

## Mantenimiento

Al actualizar el sistema privado, revisar primero los flujos y estados afectados, después sus diagramas y finalmente las capturas. Registrar aquí la nueva fecha de revisión. Mantener separadas las funciones implementadas, las comprobadas en una demo y las propuestas futuras.
