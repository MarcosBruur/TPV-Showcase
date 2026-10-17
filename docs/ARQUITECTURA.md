# Arquitectura

[Volver a la presentación](../README.md)

## Organización

TPV se organiza como una SPA Vue y un backend Django con módulos por dominio. El backend es un monolito modular: los módulos comparten aplicación, ORM y base de datos. No hay evidencia revisada de microservicios, colas de trabajo o caché distribuida como infraestructura del sistema.

## Responsabilidades

| Componente | Responsabilidad |
| --- | --- |
| Vistas Vue | Pantallas de operación y administración |
| Componentes compartidos | Navegación, listados, paginación, autocompletado y modales |
| Pinia | Sesión, rol, modalidad, carrito y turno actual |
| Servicios del navegador | Solicitudes HTTP, renovación de sesión, notificaciones y XLSX |
| Router | Navegación y guardias por rol y modalidad |
| authentication | Sesión JWT, perfil de operador y gestión de usuarios |
| pos | Catálogo, clientes comerciales, ventas, inventario, caja y egresos |
| config | Datos del comercio, identidad visual y parámetros operativos/fiscales |
| facturacion | Emisión, consulta, persistencia fiscal y generación de PDF |
| ORM y migraciones | Entidades, relaciones y restricciones de integridad |

Los permisos del router facilitan la navegación; la autorización efectiva depende de la API. Las validaciones y transacciones del negocio se distribuyen entre serializers, views y utilidades de dominio.

## Estructura del proyecto privado

Este árbol es una descripción documental de las carpetas originales. No son carpetas que deban copiarse al showcase.

```text
TPV/
├── backend/
│   ├── backend/          Configuración Django, URLs y entradas ASGI/WSGI
│   ├── authentication/   Sesión y usuarios
│   ├── pos/              Ventas, productos, caja y egresos
│   ├── config/           Comercio y parámetros de operación
│   ├── facturacion/      API fiscal, modelos, PDF y clientes WSAA/WSFE
│   ├── templates/        Entrada HTML de la SPA
│   └── static/assets/    Salida compilada del frontend
└── frontend/
    ├── src/
    │   ├── views/        Pantallas
    │   ├── components/   Elementos compartidos
    │   ├── stores/       Estado Pinia
    │   ├── services/     HTTP y utilidades
    │   ├── router/       Rutas y guardias
    │   ├── config/       Tema y notificaciones
    │   └── assets/       Estilos
    └── public/           Recursos estáticos
```

## Comunicación y entrega

En desarrollo, Vite sirve la interfaz y redirige las solicitudes de API hacia Django. El build del frontend se escribe en la carpeta de recursos estáticos del backend. Django declara una entrada de plantilla para las rutas de la SPA.

Esto describe la organización del proyecto, no una topología productiva verificada. Proxy HTTPS, hosting, almacenamiento externo y respaldo deben definirse y verificarse en cada instalación.

## Persistencia y archivos

SQLite almacena la información de negocio mediante el ORM. El proyecto configura transacciones IMMEDIATE y un tiempo de espera para mitigar contención. Los archivos incluyen imágenes comerciales y PDF; los PDF fiscales se descargan por una vista autenticada y tienen un tratamiento distinto de los medios públicos.

Las comunicaciones fiscales salen desde el backend. Certificados, claves privadas y tickets de acceso pertenecen al entorno privado y no forman parte de esta documentación.
