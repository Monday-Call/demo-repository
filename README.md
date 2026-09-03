# Portal de Obras — RHR

Portal unificado de las apps de seguimiento de obra publicadas originalmente como repos
separados en [github.com/ruben92arq](https://github.com/ruben92arq). `index.html` es el
punto de entrada: lista las 6 obras/apps y muestra un resumen financiero en vivo, leído
directamente desde el Firestore de cada una.

## Estructura

```
index.html                     Portal: resumen financiero + tarjetas de las 6 obras
obras/horus/                   Obra Horus (Decosol) — firebase: obra-horus
obras/buceo/                   Obra Buceo (Pindo) — firebase: obra-buceo-pindo
obras/marinas-de-carrasco/     Marinas de Carrasco — firebase: marinas-de-carrasco
obras/rhr-gestion/             RHR Gestión — clientes/presupuestos/gastos, solo local
```

Cada app se copió tal cual del repo original (mismo HTML/JS/service worker) y sigue
conectada a su propio proyecto de Firebase por debajo; el portal no comparte datos entre
ellas, solo las reúne y lee sus totales para el resumen. Los repos `Comoras` y
`RHR-gestión-` de Rubén están vacíos (sin código) y aparecen en el portal marcados como
tales — este último quedó reemplazado por `RHR Gestión`, que sí tiene la app completa.

No hay autenticación: las apps ya usaban reglas abiertas de Firestore (`allow read, write:
if true`) para poder sincronizar entre dispositivos sin login, y el portal respeta eso
tal cual.

## Publicar en GitHub Pages

Este repo incluye el workflow `Proof HTML`, que valida los archivos HTML en cada push.
Para servir el sitio, habilitá GitHub Pages una vez en **Settings → Pages → Build and
deployment → Source → Deploy from a branch → `main` / `/(root)`**. Con eso, cada push a
`main` publica el portal en `https://<org>.github.io/<repo>/`.
