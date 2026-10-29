# Plantilla NoExpertise · Limpieza y servicios del hogar

Web fresca de una sola página para empresas de limpieza y servicios del hogar: limpieza de casas, cristales,
fin de obra, plancha, acompañamiento a mayores, jardinería y piscinas. Bandas a todo el ancho en azul cielo,
blanco, azul pleno, lima y noche; rejillas «de azulejo» de borde a borde y fotos a sangre.

- Sectores: limpieza, servicios-domesticos, cuidado-mayores, jardineria, piscinas. Estilo: fresco. Plan mínimo: gratis.
- Secciones: hero, servicios, cifras, planes, proceso, zonas, garantias, opiniones, preguntas, presupuesto, contacto (y `texto` para apartados nuevos).
- Ejemplo: «Brisa Hogar», empresa ficticia de Alcalá de Henares (teléfonos ficticios).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; fotos en `fotos.json`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`.

## Campos propios

| Sección | Campo | Qué es |
|---|---|---|
| `hero` | `titulo_destacado` | Final del titular, con subrayado lima |
| `hero` | `items[].titulo` | Promesas cortas de la franja lima bajo la portada |
| `servicios` | `items[].precio` | Precio opcional de cada servicio («desde 16 €/hora», «Consultar») |
| `servicios` | `galeria[]` | Franja de fotos a sangre bajo los servicios (hasta 12) |
| `planes` | `planes[]` | nombre, precio, periodo, texto, incluye (cadena con «;»), destacado |
| `planes` | `nota`, `boton` | Letra pequeña y texto del botón de cada plan |
| `opiniones` | `testimonios[].servicio` | Servicio y barrio de quien opina |
| `presupuesto` | `frecuencias` | Opciones de «¿Cada cuánto?» separadas por «;» |
| `presupuesto` | `boton_formulario`, `nota` | Texto del botón y nota bajo los puntos |

El formulario de presupuesto pide nombre, teléfono, servicio (de los servicios), metros cuadrados, frecuencia,
barrio o localidad y un mensaje opcional, y abre el correo del negocio (`mailto`).

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) hechas para esta plantilla, sin licencias de terceros.
