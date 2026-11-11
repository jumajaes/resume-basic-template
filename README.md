# resume-basic-template

📝 Plantilla interactiva para crear tu Hoja de Vida básica y ordenada. Completa tus datos, añade secciones a tu gusto, guarda localmente y descarga al instante en PDF o HTML funcional. ¡Fácil, rápido y profesional!

## Qué trae

- **Una sola hoja, siempre.** El ajuste automático mide el contenido y escala la letra
  (entre 55 % y 145 %) para que **nada se salga de la página**. Si aun así no cabe, la
  barra lo avisa con `⚠ No cabe en 1 hoja` en vez de recortar el contenido en silencio.
- **Tres tamaños de hoja:** A4 (210 × 297 mm), **Oficio (216 × 356 mm)** y Carta (216 × 279 mm).
  El tamaño elegido se aplica también al imprimir, así que el PDF sale del tamaño correcto.
- **Distribución vertical sin huecos.** El espacio sobrante se reparte entre las secciones
  en lugar de dejar un vacío enorme al final o abrir huecos gigantes.
- **Edición en vivo:** al escribir, añadir o quitar secciones el ajuste se recalcula solo.
- **Ajustes que se recuerdan:** tamaño de hoja, tamaños de letra, color de acento y colores
  de fondo se guardan en el navegador (`Restablecer` vuelve a los valores por defecto).
- **Guardar cambios (.html):** descarga un HTML autónomo con tus datos, la foto incrustada
  y el mismo motor de ajuste (sigue siendo editable y se puede imprimir a PDF).
- Foto (tamaño, radio, zoom y posición), color de acento, fondo de columnas, secciones
  personalizadas, habilidades, intereses, experiencia, educación, cursos y referencias.

## Cómo usarlo

1. Abre `index.html` en el navegador (doble clic, sin instalar nada).
2. Escribe sobre cualquier texto de la hoja: todo es editable en el sitio.
3. Cambia la foto con **Cambiar** y ajusta el marco con los controles de la barra.
4. Revisa el indicador **1 hoja · NN %** de la barra: es el ajuste que se está aplicando.
   Si desactivas **Auto**, el tamaño de letra lo eliges tú con los selectores.
5. Descarga el HTML con **Guardar cambios (.html)** y, desde ahí, genera el PDF con
   **Imprimir / PDF** (destino *Guardar como PDF*, sin encabezados ni pies).

## Notas técnicas

- Un solo archivo `index.html`, sin dependencias de compilación: Tailwind, Font Awesome y
  las fuentes se cargan por CDN.
- El tamaño real de la hoja se aplica con `--page-w` / `--page-h` y una regla `@page`
  inyectada por JS (las variables CSS no funcionan dentro de `@page`).
- La escala del ajuste se aplica con `--fit-scale` sobre el tamaño base de letra de cada
  columna.
- Las secciones de una columna nunca se comprimen (`flex-shrink: 0`): si el contenido no
  cabe, se reduce la letra, no se recorta el texto.
