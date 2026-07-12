# RESKIN — clonar VOLTA para otro gym

VOLTA es el **flagship canónico de gym**. Para un gym real que responda, se clona esta carpeta y se reskinea. La "fontanería" (estructura, animaciones, SEO, PageSpeed) se reusa; solo cambia la "piel".

> Regla de oro: la piel la manda el **logo real** del cliente (paleta) y sus **fotos reales** (Instagram). Nunca stock genérico en el entregable real.

## 1. Datos — `src/data/site.json` (el 90% del reskin)
- `url` → dominio nuevo del cliente.
- `contacto` → **WhatsApp** (whatsapp, whatsappUrl, whatsappDisplay), **Instagram**, dirección (L1/L2/Full), `horario` + `horarioDias`, `mapQuery`, **`lat`/`lon`** (coords reales del gym → salen en el mapa y el JSON-LD).
- `marca` → nombre, tagline, comunidad.
- `hero` → eyebrow, titulo1/titulo2/tituloAcento (el titular grande), párrafo, CTAs, stats.
- `statsBand`, `disciplinas`, `sobre`, `planes`, `horario`, `resenas`, `ambiente`, `ubicacion`, `faq`, `cta`, `nav`.
- **Reseñas**: reemplazar por las reales de Google del gym.

## 2. Fotos — `public/img/` (la palanca #1)
Swapear por fotos reales del Instagram del gym (mismo nombre de archivo, para no tocar el JSON):
- `hero.webp` (dramática, oscura, sujeto a la derecha), `sobre.webp` (interior 4:5).
- `d-gluteo.webp`, `d-fuerza.webp`, `d-cycling.webp`, `d-cryo.webp` (disciplinas, cuadradas).
- `g-1.webp`…`g-5.webp` (galería; g-1 es la grande del bento).
- `og.jpg` (1200×630, para redes).
- Tratarlas oscuras y parejas para que no lean a stock. Formato webp, livianas (hero < 60KB ideal para el LCP).

## 3. Marca / color — `src/styles/global.css` (bloque `@theme`)
Si el logo del cliente manda otra paleta, cambiar SOLO los valores (los nombres de token se quedan):
- `--color-negro` (fondo), `--color-negro2` (paneles), `--color-ambar` (acento principal), `--color-ambar2` (hover), `--color-descarga` (2º acento de la firma), `--color-crema` (texto), `--color-tenue` (texto 2º).
- La **firma "línea de voltaje"** es de VOLTA. Para otra marca, adaptar el gradiente (`.v-line`, `.v-divider`, `.v-tick`, `.v-under`) o cambiar el sello por otro propio del negocio.

## 4. Tipografía (opcional) — `src/styles/fonts.css` + `Layout.astro`
- Fuentes self-host en `public/fonts/` (Archivo variable + …). Si se cambian: subir el woff2, actualizar `@font-face` y los tokens `--font-*` en `global.css`, y el `<link rel="preload">` en `Layout.astro`.

## 5. Logo / favicon
- Wordmark de texto en `Nav.astro`, `Footer.astro`, `404.astro` (si el cliente tiene logo-imagen, reemplazar el wordmark por su `<img>`).
- `public/favicon.svg` (el rayo de VOLTA → el del cliente).
- `public/apple-touch-icon.png` (regenerar; hoy es placeholder).

## 6. SEO / metadatos
- `src/layouts/Layout.astro`: `title`/`description` por defecto, `og:site_name`, `og:image:alt`, y el **JSON-LD** (name, `openingHours`, geo lat/lon, address).
- `public/robots.txt`, `public/sitemap.xml`, `public/llms.txt` → **dominio + contenido** del gym nuevo.

## 7. Deploy (Vercel)
- Vercel detecta Astro solo (`astro build` → `dist`).
- Al tener el dominio real, actualizar `url` en `site.json` + `sitemap.xml` + `robots.txt` + `llms.txt`.

## 8. Activación del cliente real (SOLO al vender)
Los demos van limpios. Al cerrar venta, sumar (ver memoria `activacion-cliente-real`):
- **Política de Tratamiento de Datos** (Ley 1581 Habeas Data) SOLO si hay formulario que recoja datos.
- **Aviso de cookies** solo si se mete Analytics.
- **Google Search Console** (siempre; gratis, sin cookies) — enviar el sitemap.
- **Google Analytics** opcional (upsell de mantenimiento; baja algo el PageSpeed).

## No caer en las "huellas de IA" (al variar la piel)
Ver memoria `anti-ia-tells-landings`: no reponer eyebrows con rayita en cada sección, no resaltar una palabra en color en TODOS los títulos, no volver a la banda de métricas con divisores, no meter emojis en botones/features. Romper el ritmo, variar los headers, sello de marca propio.
