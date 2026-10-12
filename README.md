# ONLYOFFICE Docs — cambios de Washington Academy

Washington Academy usa **ONLYOFFICE Docs Community Edition 9.3.1 (build 10)**, © Ascensio System SIA,
distribuido bajo la licencia **GNU AGPL v3** (ver `LICENSE`). Sitio del proyecto original:
https://github.com/ONLYOFFICE/DocumentServer — servidor: https://github.com/ONLYOFFICE/server

Este repositorio publica, como pide la AGPL, la única modificación que hacemos al componente `server`
(docservice): `wa-sin-limite.patch`.

- `Common/sources/constants.js`: `LICENSE_CONNECTIONS` de 20 a 9999 (conexiones simultáneas).
- `Common/sources/commondefines.js` y `license.js`: versión, número de build y fecha para que coincidan con 9.3.1.10.

Base usada: el código del componente `server` de ONLYOFFICE correspondiente a 9.3.1.10. Los archivos que ya no están en el
repositorio público de ONLYOFFICE se tomaron de una copia pública de su historial (commit `34adaee`) y se verificaron
idénticos, archivo por archivo, a la versión oficial 9.3.1.10.

Todo el resto del producto (editores, convertidor, interfaz) se usa sin cambios. El crédito de ONLYOFFICE se conserva.

---

Washington Academy's only modification to ONLYOFFICE Docs Community 9.3.1.10 (AGPL-3.0): raise the
simultaneous-connection constant from 20 to 9999. Patch: `wa-sin-limite.patch`.
