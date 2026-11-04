# Agustín Delgado — Personal Site

Sitio personal de Agustín Delgado. No es un portfolio ni una demo técnica — esa evidencia ya vive en otros lugares (portfolio, GitHub, LinkedIn, CV). Este sitio responde algo distinto: quién es profesionalmente, cómo piensa, y qué tipo de problemas le interesan.

Diseño editorial (verde profundo, grafito, marfil y acentos dorados) organizado en tres vistas: Inicio, Sobre mí e Intereses y pensamiento.

## Arquitectura

- HTML + CSS + JavaScript vanilla. Sin build step, sin frameworks, sin dependencias de runtime.
- Único punto de entrada: `index.html`, estilos en `styles.css`, comportamiento en `script.js`.
- Tres vistas (`#inicio`, `#sobre-mi`, `#intereses`) dentro de la misma página: un router liviano en `script.js` muestra/oculta las secciones `.view` según el hash de la URL (sin recarga, con soporte de atrás/adelante del navegador) y mueve el foco al heading de la vista para usuarios de teclado/lector de pantalla.
- Fuentes vía Google Fonts (`preconnect` + `<link>`); ningún otro recurso remoto.

## Idiomas (ES/EN)

- Switch ES/EN en el header y en el footer, sin recargar la página.
- Todo el texto vive en el objeto `translations` de `script.js` (`data-i18n` / `data-i18n-html` / `data-i18n-aria` / `data-i18n-alt`).
- La preferencia de idioma se persiste en `localStorage`.
- Los destinos de los enlaces (Portfolio, LinkedIn, GitHub, CV, contacto) no cambian entre idiomas — solo la etiqueta visible.

## Fotografía

- `assets/agustin-photo.jpg` (hero, Inicio) y `assets/agustin-photo-about.jpg` (Sobre mí) parten de la misma foto real, sin alterar rasgos faciales.
- Tratamiento aplicado: recorte fotográfico auténtico, corrección leve de color/contraste y un degradé (vignette) generado en CSS/Pillow que funde el fondo original (desordenado) hacia el verde de marca — sin reconstrucción de rostro por IA.

## Sistemas visuales (datos como lenguaje visual, no como métrica)

Todos con SVG nativo (sin librerías):

1. **Hero — campo de puntos**: un campo abstracto y sutil detrás del hero que reacciona levemente al puntero (sin física, sin ruido visual). Se omite por completo con `prefers-reduced-motion`.
2. **Mi recorrido** (Inicio): una transición visual única (no tarjetas) que representa Operaciones → Analítica de datos → Ciencia de Datos e IA como un cambio de carácter en la distribución de puntos.
3. **Intereses y pensamiento**: cinco ideas (Problemas reales, Experimentación, Modelado, IA con propósito, Impacto) en una lista accesible con panel de detalle y una constelación decorativa de fondo. Al pasar el mouse, enfocar con teclado o tocar en móvil, se revela una frase breve.

Ninguno de estos elementos representa datos medidos reales — son abstracciones conceptuales.

## Accesibilidad

- Skip link al contenido principal.
- Los nodos de "Intereses y pensamiento" son botones nativos: alcanzables por teclado, con `aria-pressed`, y su contenido no depende exclusivamente del hover (mouse, teclado y touch disparan la misma revelación).
- Menú móvil con `aria-expanded`, cierre con `Escape` y al hacer click afuera.
- Al cambiar de vista, el foco se mueve al `<h1>` de la vista (con `tabindex="-1"`) y el nav marca `aria-current="page"` en el enlace activo.
- Enlaces reales (LinkedIn, Portfolio, GitHub, CV, contacto) son `<a>` nativos, alcanzables por teclado.
- `prefers-reduced-motion` desactiva el campo de puntos del hero y el trazado animado de "Mi recorrido".
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
