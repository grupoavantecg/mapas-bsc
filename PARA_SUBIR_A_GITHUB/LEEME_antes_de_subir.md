# Subida a GitHub · versión aligerada

Los 10 MAPAs pasaron de ~772 KB a ~100 KB cada uno. El repo baja de ~8 MB a 1.5 MB y los builds de Pages deberían volver a durar segundos.

**Qué cambió:** la librería MSAL (367 KB) y el logo (152 KB en base64) estaban duplicados dentro de cada archivo. Ahora viven una sola vez en `vendor/` y `assets/`, y los 10 HTML los referencian. MSAL sigue siendo self-hosted en tu propio repo, no depende de un CDN externo.

## Antes de subir: destraba la cola

1. Ve a **Actions** y abre el run **#32** que está en "Queued".
2. Botón **Cancel workflow** arriba a la derecha.
3. Espera a que quede en gris. Si no aparece el botón, entra al run y usa el menú `...`.

Sin esto, el build nuevo se vuelve a formar detrás del atorado.

## Subir

1. En el repo: **Add file → Upload files**.
2. Arrastra **todo el contenido de esta carpeta**, incluidas las subcarpetas `assets/` y `vendor/`. Si arrastras la carpeta completa desde el explorador, GitHub conserva la estructura.
3. Verifica en la lista previa al commit que aparezcan `assets/logo.png` y `vendor/msal-2.38.4.js` con sus rutas.
4. **Commit changes**. Y ahora sí: **no toques nada más** hasta que el build termine.

El archivo `.nojekyll` ya está incluido por si no quedó en el repo.

## Verificar

Cuando el run aparezca en verde, abre cualquier MAPA. Si el logo se ve y el botón "Iniciar sesión con Microsoft" abre la ventana de login, las rutas quedaron bien.

Si el logo no carga o el login no responde, es que las subcarpetas no se subieron con su estructura. Revisa que en el repo existan `assets/logo.png` y `vendor/msal-2.38.4.js`, no sueltos en la raíz.

## Ojo

Los archivos de `MAPAs/` en la carpeta del proyecto siguen siendo los pesados con todo embebido. Esta carpeta es exclusivamente lo que va a GitHub. Para futuras regeneraciones, el aligerado se rehace desde los originales.
