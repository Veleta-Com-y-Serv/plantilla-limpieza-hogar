# Plantilla «Limpieza y servicios del hogar» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **fresco**.
Una sola página para empresas de limpieza del hogar, cristales, plancha, cuidado de mayores, jardinería y piscinas.
Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…); `src/styles/global.css` saca de ahí los derivados (`--cielo`, `--cielo-fuerte`, `--noche`, `--sobre-acento`, `--linea`) con `color-mix`. El primario lleva texto blanco encima: conviene un azul medio u oscuro. El acento (lima) lleva texto oscuro.
- **Tipografías y aspecto general**: `src/styles/global.css` (bandas `.banda--clara|cielo|azul|noche|lima`, rejilla `.azulejos`, franja de fotos `.franja`, bandas partidas `.partida`, botones píldora `.btn`/`.btn-sec`, cabecera `.cabecera--fresca` y pie `.pie--fresco`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las de relleno están en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Las fotos nuevas del cliente van en `public/fotos/`.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en burbuja + nombre.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Todas aguantan listas y campos vacíos.
- `hero` → `hero.astro`: portada partida 50/50 (banda azul cielo con titular + foto a sangre). `titulo_destacado` = final del titular con subrayado lima. `items` (solo `titulo`) = promesas de la franja lima que corre debajo.
- `servicios` → `servicios.astro`: rejilla de azulejo (`items`: titulo, texto, icono, precio opcional) y franja de fotos a sangre (`galeria`, hasta 12).
- `cifras` → `cifras.astro`: banda azul con cifras en lima (`items`: titulo = cifra, texto). Sin cifras no se pinta.
- `planes` → `planes.astro`: `planes` (nombre, precio, periodo, texto, incluye con «;», destacado), `nota` y `boton` (texto del botón; por defecto «Pedir este plan»). El botón va a `#presupuesto` si hay presupuesto activo; si no, a `#contacto`.
- `proceso` → `proceso.astro`: banda partida con foto a la izquierda (`imagen`) y pasos numerados (`items`: titulo, texto, icono).
- `zonas` → `zonas.astro`: banda noche con píldoras (`items`: titulo) y foto a la derecha (`imagen`).
- `garantias` → `garantias.astro`: banda lima con columnas (`items`: titulo, texto, icono).
- `opiniones` → `opiniones.astro`: la primera opinión como cita enorme y el resto en columna (`testimonios`: texto, autor, servicio). Sin opiniones no se pinta.
- `preguntas` → `preguntas.astro`: acordeón `details/summary` (`preguntas`: pregunta, respuesta) con botón de WhatsApp si hay número. Sin preguntas no se pinta.
- `presupuesto` → `presupuesto.astro`: banda azul con `items` (titulo, texto, icono), `nota`, `boton_formulario` y el formulario con servicio (sale de los `items` de servicios), metros cuadrados y frecuencia (`frecuencias`: cadena con «;»).
- `contacto` → `contacto.astro`: rejilla de azulejo con teléfono, WhatsApp, correo, dirección y horario de `site.yaml → contacto`. Si no hay presupuesto activo, añade el formulario de contacto.
- `texto` → `texto.astro`: diseño genérico para apartados nuevos (`tipo: texto`): con `imagen`, banda partida; sin ella, título a la izquierda y párrafos a la derecha.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre como cadena (`"79 €"`, `"desde 16 €/hora"`, `"Consultar"`).
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Lo que incluye un plan va en una cadena con «;». Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`.
6. **Apartado nuevo**: un id propio en `secciones` con `tipo:` = el diseño de otra sección (`servicios`, `planes`, `garantias`…) o `texto`. `src/pages/index.astro` lo recoge solo; no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt) y salen solos de `site.yaml`. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto en móvil (las fotos y fondos sí tocan el borde), botones de 44 px de alto como mínimo y sin scroll horizontal. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

Fotos de partida en `public/fotos/` (las genera el paso de fotos a partir de `fotos.json`, sin derechos de terceros); los SVG de `public/placeholders/` siguen de respaldo.
