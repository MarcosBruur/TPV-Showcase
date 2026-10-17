# Seguridad y privacidad

[Volver a la presentación](../README.md)

## Controles presentes

La API exige autenticación y permisos por operación. La administración de catálogo y usuarios se diferencia de la operación de caja. La consulta fiscal de un cajero se restringe a las ventas que cobró; la administración tiene un alcance más amplio.

La sesión usa access token y refresh token. El refresh se transporta en cookie HttpOnly, con rotación y blacklist; el access token permanece en localStorage. Esta descripción no equivale a una auditoría de seguridad.

La configuración exige una clave de aplicación externa al código. Existen límites de solicitudes y validaciones de contraseña. Las cargas de imágenes incluyen validación y conversión a WebP.

Los PDF fiscales se descargan por una vista autenticada. Los certificados, las claves y las credenciales temporales fiscales pertenecen al entorno privado.

## Material apto para este repositorio

Documentación escrita para el showcase, diagramas de estructura y capturas preparadas con datos ficticios. No se copian archivos del proyecto privado para construir la presentación.

La lista de archivos admitidos por .gitignore reduce incorporaciones accidentales de código y archivos operativos. Es una ayuda local: Git permite forzar inclusiones y sigue rastreando archivos que ya estaban versionados.

## Preparación de capturas

Usar una instalación de demostración y datos ficticios desde el origen. Revisar nombres, usuarios, correos, teléfonos, documentos, importes comerciales sensibles y notificaciones del navegador antes de exportar.

No incorporar certificados, claves, tokens, paneles de entorno, consolas de red con cabeceras o registros internos. Evitar comprobantes fiscales reales: QR, códigos y enlaces pueden contener información aun cuando parte de la pantalla esté tapada.

El material fiscal de demostración debe identificarse visualmente como tal. No se debe emitir una factura real para obtener una captura.

## Estado de revisión

El showcase documenta controles observados y límites conocidos. No declara una certificación, auditoría completa o ausencia de vulnerabilidades. Consultar [estado y validación](ESTADO.md).
