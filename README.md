# resume-basic-template

📝 Plantilla interactiva para crear tu Hoja de Vida básica y ordenada. El diseño es **fijo**:
las secciones son las estándar de un CV, la hoja tiene un tamaño único y la letra se ajusta
sola para que **todo quede en una sola página**. Solo hay dos botones: guardar y imprimir.

## Cómo funciona

- **Una sola hoja, siempre.** La letra base es fija (13 px la columna izquierda, 14 px la
  derecha, 11 px los títulos) y un ajuste automático la escala entre 45 % y 145 % hasta que
  el contenido cabe en la hoja. Nada se recorta: si aun así no cabe, el indicador de la
  barra avisa `⚠ No cabe en 1 hoja`.
- **La hoja no crece.** El alto de la hoja, de la rejilla y de las columnas es fijo; el
  sobrante se reparte entre las secciones (nunca huecos gigantes).
- **Secciones fijas, ordenadas por importancia:**
  - Izquierda: foto y nombre · Contacto · Perfil profesional · Habilidades · Intereses
  - Derecha: Experiencia profesional · Educación · Cursos y certificaciones · Referencias
- **Se pueden añadir elementos dentro de cada sección** (habilidades, intereses,
  experiencias, educaciones, cursos y referencias), pero **no secciones nuevas**.
- **Hoja fija en Oficio (215,9 × 330,2 mm)**, más alta que A4 para que quepa más contenido
  sin encoger la letra. Para cambiarla, una línea en `index.html`:
  `const PAGE_W = '215.9mm'; const PAGE_H = '330.2mm';` (A4: `210mm` × `297mm`).

## Cómo llenarla

**A mano:** abre `index.html` en el navegador y escribe sobre cualquier texto (todo es
editable en el sitio).

**Con una IA (o cualquier script):** los datos se pueden pasar en JSON.

- Por URL: `index.html?datos=<JSON>` o `index.html?datos=https://.../mi-cv.json`
  (la IA puede generar ese archivo y la hoja lo descarga al abrirse).
- En la página: `Ctrl` + `Shift` + `D` abre el editor de JSON, con **Copiar JSON**
  (para llevarte los datos actuales) y **Aplicar datos**.

### Esquema de los datos

```json
{
  "nombre": "JUAN (J)",
  "apellido": "JARAMILLO",
  "profesion": "💻 SOFTWARE ENGINEER FULL-STACK",
  "foto": "https://.../mi-foto.jpg",
  "contacto": [{ "etiqueta": "📧 CORREO", "valor": "correo@ejemplo.com" }],
  "perfil": "Texto del perfil profesional.",
  "habilidades": ["🧠 Habilidad", "🤖 Otra habilidad"],
  "intereses": ["📚 Estudiar"],
  "experiencia": [{
    "cargo": "Full Stack Engineer",
    "empresa": "TSGroup S.A.S.",
    "fecha": "Abr 2024 - Presente",
    "descripcion": "Qué hiciste."
  }],
  "educacion": [{
    "titulo": "Programación de Sistemas de Información",
    "institucion": "Politécnico Colombiano 'Jaime Isaza Cadavid'",
    "anio": "2022 - 2026"
  }],
  "cursos": ["📊 Análisis de Datos de Google"],
  "referencias": [{ "nombre": "Nombre", "cargo": "Cargo", "telefono": "Tel: +57 000 000 0000" }]
}
```

Todos los campos son opcionales: los que no vengan se dejan como están.

## Guardar e imprimir

- **Guardar cambios (.html):** descarga un HTML autónomo con tus datos (la foto incrustada)
  y el mismo motor de ajuste. Sigue siendo editable y se puede volver a imprimir.
- **Imprimir / PDF:** el destino *Guardar como PDF* genera el PDF con el tamaño de la hoja
  y sin encabezados ni pies de página.

## Notas técnicas

- Un solo archivo `index.html`, sin compilación: Tailwind, Font Awesome y las fuentes se
  cargan por CDN.
- El tamaño real de la hoja se aplica con `--page-w` / `--page-h` y una regla `@page`
  inyectada por JS (las variables CSS no funcionan dentro de `@page`).
- La escala del ajuste se aplica con `--fit-scale` sobre el tamaño base fijo de cada columna.
- Las secciones de una columna nunca se comprimen (`flex-shrink: 0`): si el contenido no
  cabe, se reduce la letra, no se recorta el texto.
- El ajuste se recalcula solo al escribir, añadir o quitar elementos (`MutationObserver`).
