# Agustín Delgado — Personal Site

Sitio personal de Agustín Delgado. No es un portfolio ni una demo técnica — esa evidencia ya vive en otros lugares (portfolio, GitHub, LinkedIn, CV). Este sitio responde algo distinto: quién es profesionalmente, cómo piensa, y qué tipo de problemas le interesan.

Pensado como una libreta personal de alguien que trabaja con datos, no como una landing tratando de demostrar competencia técnica.

## Arquitectura

- HTML + CSS + JavaScript vanilla. Sin build step, sin frameworks, sin dependencias de runtime.
- Único punto de entrada: `index.html`, estilos en `styles.css`, comportamiento en `script.js`.
- Página compacta (~2-3 scrolls de escritorio después del hero), sin secciones interminables.
- Fuentes vía Google Fonts (`preconnect` + `<link>`); ningún otro recurso remoto.

## Idiomas (ES/EN)

- Switch ES/EN en el header, sin recargar la página.
- Todo el texto vive en el objeto `translations` de `script.js` (`data-i18n` / `data-i18n-aria`).
- La preferencia de idioma se persiste en `localStorage`.
- Los destinos de los enlaces (Portfolio, LinkedIn, GitHub, CV, contacto) no cambian entre idiomas — solo la etiqueta visible.

## Sistemas visuales (datos como lenguaje visual, no como métrica)

Máximo tres ideas interactivas/visuales en toda la página, todas con SVG nativo (sin librerías):

1. **Hero — campo de puntos**: un campo abstracto y sutil detrás del hero que reacciona levemente al puntero (sin física, sin ruido visual). Se omite por completo con `prefers-reduced-motion`.
2. **Trayectoria**: una transición visual única (no tarjetas) que representa Operaciones → Datos → Applied AI como un cambio de carácter en la distribución de puntos.
3. **Cómo trabajo — scatter conceptual**: cinco ideas (Entender, Preguntar, Estructurar, Validar, Construir) distribuidas en un espacio conceptual. Al pasar el mouse, enfocar con teclado o tocar en móvil, se revela una frase breve y se resaltan las relaciones cercanas.

Ninguno de estos elementos representa datos medidos reales — son abstracciones conceptuales.

## Accesibilidad

- Skip link al contenido principal.
- Los nodos del scatter de "Cómo trabajo" son botones nativos: alcanzables por teclado, con `aria-pressed`, y su contenido no depende exclusivamente del hover (mouse, teclado y touch disparan la misma revelación).
- Menú móvil con `aria-expanded`, cierre con `Escape` y al hacer click afuera.
- Enlaces reales (LinkedIn, Portfolio, GitHub, CV, contacto) son `<a>` nativos, alcanzables por teclado.
- `prefers-reduced-motion` desactiva el campo de puntos del hero y el trazado animado de la trayectoria.
- Foco visible global vía `:focus-visible`. SVGs puramente decorativos llevan `aria-hidden="true"`.

## Rutas de producción

- Portfolio: `https://portfolio-me-f104.vercel.app/`
- LinkedIn: `https://www.linkedin.com/in/agustin-delgado-data98615190/`
- GitHub: `https://github.com/AgusDelgado98`
- CV: `https://portfolio-me-f104.vercel.app/cv/Agustin_Delgado_CV_EN.pdf` (fuente canónica única; mismo archivo para ES y EN)
- Contacto: `mailto:augusto.delgado00@hotmail.com`

## Videos

Los videos de la versión anterior (introducción + mini entrevista) fueron retirados del sitio: el concepto de video fue abandonado en esta versión. Los archivos originales se conservan fuera del árbol deployable, en `../video-backups/production-videos/`.

## Desarrollo local

Desde esta carpeta, con cualquier servidor estático:

```bash
python -m http.server 8080
```

Luego abrir `http://localhost:8080`.

## Despliegue

Sitio 100% estático, pensado para **Vercel** (ver `vercel.json` para headers de seguridad y cache). No requiere variables de entorno ni build command.
