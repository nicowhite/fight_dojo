# Fight Dojo

Biblioteca personal de juegos de pelea (Street Fighter 6, Tekken 8, Mortal Kombat 1): combos, tips, tutoriales y lore por personaje.

## Dónde vive

- La app es un **artefacto de claude.ai**: https://claude.ai/code/artifact/6edb0abc-c55c-4d5b-9bc1-c419b0ebfd8f
- `index.html` en este repo es el código fuente de esa página (un solo archivo con CSS, HTML y JS).
- El **contenido** (entradas) NO está en el repo: vive en la base de datos del artefacto, colección `entries`
  (capability `db`, regla: read `view`, write `admin`). Republicar el HTML no borra las entradas.

## Cómo trabajar

1. Leer el artefacto con la herramienta Artifact (`action: read`, con la URL de arriba) antes de cambiar nada,
   por si la versión publicada es más nueva que este repo; si lo es, traer esos cambios a `index.html`.
2. Editar `index.html`.
3. Publicar con Artifact en **la misma URL** (`url` de arriba), nunca como artefacto nuevo.
4. Hacer commit y push del cambio a este repo.

Para cargar o corregir entradas en volumen, usar ArtifactData sobre la colección `entries`, no el HTML.

## Sincronizar con GitHub ("sincronizá con GitHub")

`entries.json` es la copia pública del contenido: la usan GitHub Pages (https://nicowhite.github.io/fight_dojo/)
y los visitantes del artefacto sin sesión de Claude (función `loadStatic` en `index.html`).
1. Exportar la colección `entries` con ArtifactData (`list`, `limit: 1000`) y escribir `entries.json` como un
   arreglo JSON (UTF-8 sin BOM) donde cada objeto es el documento más su `id`.
2. Republicar el artefacto pasando `entries.json` en `files` (los retratos ya publicados se conservan).
3. Commit y push a `main`; GitHub Pages publica desde `main`.

## Notas

- Los rosters de cada juego están en la constante `GAMES` dentro de `index.html`.
- Fuera de claude.ai (por ejemplo GitHub Pages) `window.claude` no existe: la página lee `entries.json` en modo
  solo lectura, que puede estar atrasado respecto de la base de datos hasta la próxima sincronización.
- Los retratos oficiales están en `portraits/<juego>-<slug>.png`; un personaje sin archivo usa la cara pixelada.
- Textos de la interfaz en español rioplatense.
