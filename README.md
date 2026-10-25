# ONLYOFFICE Docs — cambios de Washington Academy

Washington Academy usa **ONLYOFFICE Docs Community Edition 9.3.1 (build 10)**, © Ascensio System SIA,
distribuido bajo la licencia **GNU AGPL v3** (ver `LICENSE`). Sitio del proyecto original:
https://github.com/ONLYOFFICE/DocumentServer — servidor: https://github.com/ONLYOFFICE/server

Este repositorio publica, como pide la AGPL, las modificaciones que hacemos:

1. `wa-sin-limite.patch` — componente `server` (docservice), desde 2026-10-12.
2. `wa-movil-edicion.patch` — componente `web-apps` (editores de celular), desde 2026-10-16.
3. `wa-movil-menu-celda.patch` — componente `web-apps` (menú de celda en la hoja de cálculo de celular), desde 2026-10-25.
   Se aplica encima de `wa-movil-edicion.patch`.

- `Common/sources/constants.js`: `LICENSE_CONNECTIONS` de 20 a 9999 (conexiones simultáneas).
- `Common/sources/commondefines.js` y `license.js`: versión, número de build y fecha para que coincidan con 9.3.1.10.

Base usada: el código del componente `server` de ONLYOFFICE correspondiente a 9.3.1.10. Los archivos que ya no están en el
repositorio público de ONLYOFFICE se tomaron de una copia pública de su historial (commit `34adaee`) y se verificaron
idénticos, archivo por archivo, a la versión oficial 9.3.1.10.

### `wa-movil-edicion.patch` (web-apps, tag `v9.3.1.10`)

La versión Community abre los editores de celular solo para ver. El código abierto de `web-apps` ya trae las pantallas de
edición de celular; lo que falta es el archivo que las conecta (`src/lib/patch.jsx`). Este parche lo completa para Excel,
Word y PowerPoint con la implementación AGPL publicada por el proyecto Euro-Office
(https://github.com/Euro-Office/web-apps, archivos `apps/*/mobile/src/lib/{patch,editor}.jsx` y
`apps/common/mobile/lib/editor.jsx`), sin otros cambios. Se compila con `vendor/framework7-react`
(`PRODUCT_VERSION=9.3.1 BUILD_NUMBER=10 npm run deploy-cell|deploy-word|deploy-slide`); solo cambia `mobile/dist/js/app.js`
de cada editor.

### `wa-movil-menu-celda.patch` (web-apps, encima de `wa-movil-edicion.patch`)

En la hoja de cálculo de celular, el menú que sale al tocar una celda seleccionada (Cortar, Copiar, Pegar, Celda…) no
aparecía. Tres cambios:

- `apps/spreadsheeteditor/mobile/src/lib/patch.jsx`: se activa `EditorUIController.ContextMenu` (venía comentado).
- `apps/common/mobile/lib/controller/ContextMenu.jsx`: el menú se abre en el callback de `setState`; con React 19 la lista
  de opciones todavía estaba vacía y el menú no abría al primer toque.
- `apps/spreadsheeteditor/mobile/src/lib/editor.jsx`: "Anular combinación" solo en celdas combinadas y "Combinar" solo si
  no lo están (una celda sola reporta `Disabled`, no `None`).

Se compila igual (`npm ci` con Node 20 en `vendor/framework7-react`, `PRODUCT_VERSION=9.3.1 BUILD_NUMBER=10 npm run
deploy-cell`); solo cambia `spreadsheeteditor/mobile/dist/js/app.js`.

Todo el resto del producto (editores, convertidor, interfaz) se usa sin cambios. El crédito de ONLYOFFICE se conserva.

---

Washington Academy's modifications to ONLYOFFICE Docs Community 9.3.1.10 (AGPL-3.0): raise the
simultaneous-connection constant from 20 to 9999 (`wa-sin-limite.patch`, server) and wire up the open-source mobile
editing UI using Euro-Office's AGPL implementation (`wa-movil-edicion.patch`, web-apps), plus the cell context menu
(Cut/Copy/Paste) in the mobile spreadsheet editor (`wa-movil-menu-celda.patch`, web-apps).
