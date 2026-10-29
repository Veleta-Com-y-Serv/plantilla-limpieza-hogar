# Limpieza y servicios del hogar: brief de diseño

Plantilla `limpieza-hogar` creada el 29/10/2026 a partir de `una-pagina` con `php artisan plantillas:nueva` y
rediseñada entera (fila 23 del brief de la tanda «ancho completo»). Este fichero se queda en el repo: es lo que lee
quien (persona o agente) la rediseñe después.

## Brief

- **Para quién**: empresas de limpieza de casas, servicios domésticos, cuidado de mayores, jardinería y
  mantenimiento de piscinas (`sectores` de template.yaml). Quien entra quiere saber qué hacen, cuánto cuesta más o
  menos, si llegan a su barrio y si se puede fiar.
- **Qué tiene que conseguir la web**: que pidan presupuesto (formulario con metros cuadrados y frecuencia) o que
  llamen o escriban por WhatsApp.
- **Tono y estilo** (`fresco`): limpio, luminoso, de confianza. Sí: la sensación de casa recién ventilada, colores
  claros con un golpe de lima. No: el aspecto de folleto con estrellitas y burbujas de jabón dibujadas, ni la caja
  centrada estrecha con tarjetas blancas.
- **Paleta de ejemplo**: primario `#0f6fc6` (azul; lleva texto blanco encima), acento `#c6f03c` (lima; lleva texto
  oscuro), fondo `#ffffff`, texto `#0b2742` (azul noche). Derivados con `color-mix` en `global.css`: `--cielo`
  (primario al 11 % sobre el fondo), `--cielo-fuerte` (22 %), `--noche` (texto oscurecido), `--sobre-acento`,
  `--linea`. Si el cliente cambia los cuatro, las bandas siguen alternando claro / cielo / pleno / noche / acento.
- **Tipografía**: títulos en sans geométrica de sistema (`Century Gothic`, Futura, Avenir Next…) a 700 con
  interletrado negativo, enormes (portada hasta 6,6 rem; secciones hasta 4,6 rem); texto en Segoe UI / system-ui.
  Antetítulos pequeños en mayúsculas espaciadas con una raya de color delante.
- **Firma visual**:
  1. Rejilla «de azulejo»: celdas separadas por juntas finas que van de borde a borde de la ventana (servicios y
     contacto), sin tarjetas.
  2. Fotos a sangre con **una sola esquina muy redonda** (portada abajo a la izquierda, cómo funciona arriba a la
     derecha, zonas arriba a la izquierda, cita grande arriba a la derecha).
  3. Subrayado de rotulador lima detrás del final del titular (`titulo_destacado`).
  4. Burbujas decorativas (aros y círculos) que asoman por el borde de algunas bandas; en móvil se ocultan los aros
     para que no crucen textos.
  5. Franja lima de promesas que corre de lado a lado bajo la portada (se para con «reducir movimiento»).
- **Ritmo de bandas** (todas a todo el ancho): portada cielo + foto → franja lima → servicios blanco (azulejos +
  franja de 6 fotos a sangre) → cifras azul → planes cielo (el destacado en bloque noche) → cómo funciona blanco con
  foto a sangre a la izquierda → zonas noche con foto a sangre a la derecha → garantías lima → opiniones blanco con
  cita enorme → preguntas cielo → presupuesto azul con formulario → contacto blanco en azulejos → pie noche con filo
  lima.
- **Apartados** (en orden): `hero`, `servicios` (items con icono y precio opcional, galeria), `cifras`, `planes`
  (`planes`: nombre, precio, periodo, texto, incluye «;», destacado), `proceso`, `zonas`, `garantias`, `opiniones`
  (`testimonios` con `servicio`), `preguntas`, `presupuesto` (`frecuencias`, `boton_formulario`, `nota`, items),
  `contacto`. `texto` para apartados nuevos.
- **Fotos** (`fotos.json`, 9): salón luminoso recién limpiado (portada, 1:1); franja vertical 3:4 de cocina, baño,
  cristales, plancha, jardín y piscina; carrito de limpieza en un pasillo (cómo funciona); calle porticada del
  casco de Alcalá (zonas). Sin texto legible, sin logotipos, sin personas reconocibles.
- **Responsive**: móvil primero; a 375 px todo en una columna con 16 px de margen del texto y las fotos de borde a
  borde; a 768 px la portada, cómo funciona y zonas pasan a 50/50 y los azulejos a 2 columnas; a 1100 px los
  azulejos y las garantías a 4 columnas, la franja de fotos a 6 y los planes en fila.
- **Qué no hacer**: volver al hero centrado de `una-pagina`, poner los servicios o los planes en tarjetas blancas
  sueltas, meter cifras o precios fijos en los componentes, o usar el lima como color de texto sobre blanco.
