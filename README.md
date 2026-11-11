# resume-basic-template

📝 Plantilla interactiva para crear tu Hoja de Vida básica y ordenada. El diseño es **fijo**:
las secciones son las estándar de un CV (todas obligatorias), la hoja es una **Carta** y la
letra tiene un tamaño fijo que solo se reduce si el contenido no cabe. En la barra hay dos
botones: guardar e imprimir.

## Cómo funciona

- **Una sola hoja, siempre, y la letra se acomoda sola.** La letra base es de 13 px
  (columna izquierda), 14 px (derecha) y 11 px (títulos), pero el ajuste la **escala
  dinámicamente entre 30 % y 125 %** hasta que el contenido llena exactamente la hoja:
  crece si sobra espacio, baja si el contenido es largo. Así la hoja queda siempre llena y
  nada se desborda.
- **La hoja no crece.** El alto de la hoja, de la rejilla y de las columnas es fijo, y
  **cada sección tiene un alto máximo**: si aun así una sección se pasa de largo, se
  recorta dentro de ella, sin empujar a las demás.
- **Secciones fijas, de arriba hacia abajo, ordenadas por importancia:**
  - Izquierda: foto y nombre · Contacto · Perfil profesional · Habilidades · Intereses
  - Derecha: Experiencia profesional · Educación · Cursos y certificaciones · Referencias
  Todas están siempre: son los datos mínimos de una hoja de vida. Si no se llenan, quedan
  vacías.
- **Se pueden añadir elementos dentro de cada sección** (habilidades, intereses,
  experiencias, educaciones, cursos y referencias), pero **no secciones nuevas**.
- **Hoja fija en Carta (215,9 × 279,4 mm).** Para cambiarla, una línea en `index.html`:
  `const PAGE_W = '215.9mm'; const PAGE_H = '279.4mm';` (A4: `210mm` × `297mm`).

## Cómo llenarla

**A mano:** abre `index.html` en el navegador y escribe sobre cualquier texto (todo es
editable en el sitio).

**Con una IA (o cualquier script):** los datos se pueden pasar en JSON.

- Por URL: `index.html?datos=<JSON>` o `index.html?datos=https://.../mi-cv.json`
  (la IA puede generar ese archivo y la hoja lo carga al abrirse).
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

Todos los campos son opcionales: los que no vengan se quedan vacíos.

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
- La reducción de la letra se aplica con `--fit-scale` sobre el tamaño base fijo de cada
  columna.
- Las secciones de una columna nunca se comprimen (`flex-shrink: 0`) y tienen `overflow:
  hidden`: si el contenido no cabe, se recorta dentro de la sección, no se recorta la hoja.
- El ajuste se recalcula solo al escribir, añadir o quitar elementos (`MutationObserver`).
