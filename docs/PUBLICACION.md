# Publicación y mantenimiento del showcase

[Volver a la presentación](../README.md)

Repositorio de destino: [MarcosBruur/TPV-Showcase](https://github.com/MarcosBruur/TPV-Showcase).

## Estructura pública

```text
TPV-Showcase/
├── README.md
├── DERECHOS.md
├── .gitignore
├── .gitattributes
├── docs/
│   ├── ARQUITECTURA.md
│   ├── MODELO-DE-DOMINIO.md
│   ├── FLUJOS.md
│   ├── DECISIONES.md
│   ├── API.md
│   ├── SEGURIDAD.md
│   ├── ESTADO.md
│   ├── DEMO.md
│   └── PUBLICACION.md
└── assets/
    └── screenshots/
        └── README.md
```

Los diagramas Mermaid viven dentro del Markdown y se visualizan en GitHub. No se necesita instalar dependencias, ejecutar un servidor ni configurar GitHub Pages.

## Revisión y envío

Desde la carpeta local TPV-Showcase, revisar los cambios y comprobar que el remoto origin corresponda al repositorio indicado:

```powershell
git status --short
git remote -v
git diff --stat
git diff -- README.md DERECHOS.md
```

Si origin no existe, agregarlo una única vez:

```powershell
git remote add origin https://github.com/MarcosBruur/TPV-Showcase.git
```

Agregar únicamente la documentación y los recursos preparados, revisar lo que entrará al commit y enviarlo a la rama actual:

```powershell
git add README.md DERECHOS.md .gitignore .gitattributes docs assets/screenshots
git diff --cached --stat
git diff --cached
git commit -m "docs: presentar arquitectura y funcionalidades de TPV"
git push -u origin HEAD
```

Estos son pasos de publicación; su presencia en la documentación no significa que ya se hayan ejecutado. Si el remoto rechaza un envío por cambios previos, revisar y reconciliar el historial sin forzar el push.

## Presentación del repositorio

Descripción sugerida para About:

> Showcase de TPV: ventas, inventario, caja y facturación electrónica. Arquitectura Vue + Django, flujos de negocio y documentación técnica. Código fuente privado.

Temas sugeridos: vue, django, django-rest-framework, point-of-sale, inventory-management, software-architecture, portfolio, showcase.

No agregar un enlace de demo si no hay un despliegue preparado para acceso público. La revisión de esta documentación no confirma el estado de visibilidad del repositorio remoto.

## Actualizaciones

Agregar capturas siguiendo la guía de assets/screenshots/README.md, actualizar la portada y registrar la fecha de revisión en ESTADO.md. Mantener la documentación alineada con el código privado y conservar explícitos los límites.

No trasladar el historial Git del proyecto privado, su carpeta .git, código fuente, builds, archivos de entorno ni datos operativos a este repositorio.
