# Salud a Domicilio

Sitio web multipágina para un servicio independiente de **enfermería a domicilio
y traslados en ambulancia**. Está pensado como **maqueta educativa para un taller
de HTML y CSS**: usa solo HTML y CSS, tiene comentarios en español y no necesita
frameworks, instalación ni JavaScript.

---

## Cómo ver el sitio

1. Abrí la carpeta del proyecto.
2. Hacé doble clic en `index.html` (se abre en el navegador).
3. Para verlo como si estuviera publicado, abrí una terminal en esta carpeta y ejecutá:

   ```bash
   python3 -m http.server 8000
   ```

   Después entrá a <http://localhost:8000>.

> Las tipografías de Google necesitan internet. El resto del sitio funciona sin
> conexión porque las fotos y el logo están guardados en `assets/`.

---

## Archivos del proyecto

```
enfermeria/
├── index.html                  → Inicio: portada, servicios, pasos y sobre el servicio
├── servicios.html              → Enfermería a domicilio y traslados en ambulancia
├── nosotros.html               → Historia, valores, números y compromiso
├── preguntas-frecuentes.html   → Preguntas agrupadas por tema
├── contacto.html               → Teléfono, WhatsApp, correo, zonas y avisos
├── styles.css                  → Todos los estilos y el responsive
├── assets/                     → Fotos y logo
│   ├── hero.jpg
│   ├── nosotros.jpg
│   ├── enfermeria.jpg
│   ├── traslados.jpg
│   ├── ambulancia.jpg
│   └── logo.svg
└── README.md                   → esta guía
```

**Hay cinco páginas separadas.** El encabezado, el pie y los botones flotantes
se repiten en todas: si cambiás el teléfono, tenés que actualizarlo en los cinco
archivos.

---

## Datos que hay que reemplazar

Todos los datos son **ficticios** y están marcados en el HTML con comentarios
`<!-- REEMPLAZAR: ... -->`. La lista completa:

| Dato | Dónde está | Valor actual |
|---|---|---|
| Nombre del servicio | Encabezado, pie y textos | Salud a Domicilio |
| Teléfono visible | Navbar, botones, tarjetas y pie | `11 5555-5555` |
| Teléfono para llamar (`tel:`) | Todos los enlaces de llamada | `+5491155555555` |
| WhatsApp (`wa.me`) | Botones y botones flotantes | `5491155555555` |
| Correo | Página de contacto y pie | `hola@saludadomicilio.com.ar` |
| Profesional y matrícula | `nosotros.html`, firma | Enf. Martín Ríos · Matrícula 00000 |
| Números de experiencia | `nosotros.html`, sección de estadísticas | 10+ años, 500+ familias, etc. |
| Zonas de atención | `contacto.html` y preguntas frecuentes | CABA y GBA Norte |
| Horarios | Varias páginas | Lunes a domingo, 8 a 20 h |
| Números de emergencia | Barra superior, pie y avisos | 107 (SAME) y 911 |

### Cómo reemplazar el teléfono y el WhatsApp

El teléfono aparece de tres formas distintas. Conviene buscar y reemplazar cada
una en **los cinco archivos HTML**:

1. **Texto visible:** `11 5555-5555`
2. **Enlaces de llamada:** `tel:+5491155555555`
3. **Enlaces de WhatsApp:** `https://wa.me/5491155555555?text=...`

El número de WhatsApp va **sin signos ni espacios**, con código de país
(`54` + `9` + código de área + número). El texto después de `?text=` es el
mensaje que aparece ya escrito en el chat; podés cambiarlo o borrarlo.

Una forma rápida de hacerlo desde la terminal, dentro de la carpeta:

```bash
# Reemplazá los tres valores por los reales y ejecutá:
sed -i 's/11 5555-5555/11 4444-4444/g; s/+5491155555555/+5491144444444/g; s/5491155555555/5491144444444/g' *.html
```

Revisá después con `grep -R "5555" *.html` que no haya quedado ningún dato de
ejemplo.

### Cómo reemplazar el correo

Buscá `hola@saludadomicilio.com.ar` en `contacto.html` (tarjeta y enlace
`mailto:`) y en el pie de las cinco páginas.

---

## Comentarios con pistas

A lo largo del HTML y del CSS hay comentarios que empiezan con **`PISTA:`**.
No se ven en el navegador: sirven para orientar al momento de editar el código.

- En HTML: `<!-- PISTA: ... -->`
- En CSS: `/* PISTA: ... */`

Las pistas indican qué se puede cambiar en cada bloque (textos, fotos, colores,
botones, cantidad de tarjetas, breakpoints) y qué otros archivos conviene
actualizar cuando el cambio se repite. Los datos ficticios siguen marcados
aparte con `REEMPLAZAR:`.

---

## Cómo personalizar el diseño

### Colores

Todos los colores están al principio de `styles.css`, dentro de `:root`:

```css
:root {
  --teal: #1B76B4;        /* color principal (azul) */
  --teal-dark: #0C3B5E;   /* secciones oscuras y títulos */
  --teal-soft: #D9EAF7;   /* detalles suaves */
  --mint: #EDF5FC;        /* fondos alternos */
  --cream: #FBF9F4;       /* fondo general */
  --sand: #F4EEE3;        /* fondo cálido alternativo */
  --amber: #F0B429;       /* acentos y detalles */
  --whatsapp: #0F7D43;    /* botones de WhatsApp */
  --ink: #152421;         /* texto principal */
  --muted: #536763;       /* texto secundario */
}
```

Cambiar esos valores alcanza para transformar todo el sitio. También podés
ajustar `--radius` (bordes redondeados), `--shadow` (sombras) y `--container`
(ancho máximo del contenido).

### Tipografías

Se cargan desde Google Fonts en el `<head>` de cada página:

- **Manrope** para títulos y botones.
- **Inter** para párrafos y navegación.

Si querés usar otras, cambiá el `<link>` en los cinco HTML y las familias en
`styles.css` (`font-family`). Siempre conviene dejar una fuente de respaldo como
`system-ui` o `sans-serif`.

### Logo

El logo es `assets/logo.svg`: una casa con una cruz. Es un SVG editable con
cualquier editor de texto; los colores están en los atributos `fill` y `stroke`.
Si lo reemplazás por un archivo con otro nombre, actualizá las referencias en el
encabezado, el pie y el `<link rel="icon">`.

### Fotos

Reemplazá los archivos de `assets/` manteniendo el mismo nombre. El CSS las
recorta con `object-fit: cover`:

| Archivo | Uso | Proporción que conviene |
|---|---|---|
| `hero.jpg` | Portada de Inicio | Vertical, 4:5 (ej. 1600 × 2000) |
| `nosotros.jpg` | Inicio y Nosotros | Horizontal, 4:3 |
| `enfermeria.jpg` | Tarjeta y página de Servicios | Horizontal, 16:9 |
| `traslados.jpg` | Tarjeta de Servicios | Horizontal, 16:9 |
| `ambulancia.jpg` | Sección de traslados | Horizontal, 4:3 |

Mantené los atributos `width` y `height` del `<img>`: ayudan a que la página no
“salte” mientras cargan las imágenes. Actualizá también el `alt` si la foto
muestra otra cosa.

### Menú hamburguesa

Funciona con HTML y CSS, sin JavaScript: un `<input type="checkbox">` oculto y
un `<label>` con las tres líneas. Cuando el checkbox se marca, el CSS muestra el
menú y convierte las líneas en una X.

**Limitación:** al tocar un enlace, la página cambia (o hace scroll) pero el
menú queda abierto hasta que se vuelve a tocar la X. Navegar a otra página sí lo
reinicia. Es una buena consigna para resolver más adelante con unas pocas líneas
de JavaScript.

### Preguntas frecuentes

Las preguntas se muestran siempre abiertas, como tarjetas con título y
respuesta. No hay acordeones ni JavaScript: es la versión más simple y directa
para leer o imprimir.

### Llamada final y botones flotantes

La banda de llamada a la acción (`.cta-band`) y los botones flotantes
(`.floating-contact`) se repiten en las cinco páginas. Si agregás una página
nueva, copiá también esos bloques para mantener la coherencia.

---

## Estructura del CSS

`styles.css` está dividido en secciones numeradas y comentadas:

1. Variables y estilos generales
2. Utilidades (contenedor, botones, listas, avisos)
3. Encabezado y menú
4. Botones flotantes de contacto
5. Portada (hero)
6. Contacto rápido
7. Tarjetas de servicios
8. Pasos y bloques en dos columnas
9. Testimonios y preguntas frecuentes
10. Página de servicios
11. Página nosotros
12. Página de contacto
13. Llamada final a la acción
14. Pie de página
15. Adaptación a tablets y celulares

Todo el layout usa **flexbox** (`display: flex`) y medidas relativas
(`clamp`, `%`, `rem`). No se usa `display: grid` para que el ejemplo se mantenga
dentro de los temas básicos del taller.

Los cortes responsive están en `1080px` (menú hamburguesa), `900px`, `700px` y
`480px` (botones flotantes compactos).

---

## Accesibilidad incluida

- HTML semántico (`header`, `nav`, `main`, `section`, `footer`).
- Enlace "Saltar al contenido" para navegar con teclado.
- Foco visible en todos los enlaces y botones.
- Textos alternativos en las imágenes decorativas e informativas.
- Etiqueta accesible en el botón del menú y en los botones flotantes.
- Contraste cuidado y tamaños de texto adaptables.
- Respeto por la preferencia `prefers-reduced-motion`.
- Avisos de emergencia claros (107 / 911) en las páginas principales.

Al agregar contenido, mantené estos criterios: imágenes con `alt`, títulos en
orden (`h1`, `h2`, `h3`) y enlaces con textos claros.

---

## Desafíos para el taller

1. **Cambiar la identidad:** probar otra paleta en `:root`, otro par de
   tipografías y un logo propio.
2. **Sumar una página:** por ejemplo "Obras sociales" u "Opiniones", con su
   enlace en el menú y en el pie de las cinco páginas.
3. **Reemplazar las fotos:** usar imágenes reales del servicio, ajustando los
   `alt` y las proporciones.
4. **Mejorar el menú:** hacer que se cierre al elegir un enlace, con unas pocas
   líneas de JavaScript o el truco de `:target`.
5. **Sumar un formulario:** un formulario de contacto con `mailto:` o con un
   servicio externo (hoy el sitio usa solo teléfono, WhatsApp y correo).
6. **Convertir las preguntas en acordeones:** usar `<details>` y `<summary>`
   para mostrar solo la pregunta y desplegar la respuesta al hacer clic.
7. **Crear una galería:** una grilla de fotos con `display: grid`, para comparar
   con el resto del sitio hecho en flexbox.
8. **Agregar modo oscuro:** con variables de CSS y `prefers-color-scheme`.
9. **Unificar los datos de contacto:** reemplazar los teléfonos repetidos por un
   componente o plantilla, y comentar qué cambiaría al pasar a un generador de
   sitios estáticos.
10. **Publicar el sitio:** subirlo a GitHub Pages, Netlify o Vercel.

---

## Créditos de las fotos

Las fotos son de [Pexels](https://www.pexels.com) y se usan bajo la
[Licencia de Pexels](https://www.pexels.com/license/). Son imágenes de ejemplo:
conviene reemplazarlas por fotos reales del servicio.

| Archivo | Foto | Autor/a |
|---|---|---|
| `hero.jpg` | [Woman measuring the blood pressure of an elderly man](https://www.pexels.com/photo/7345476/) | Antoni Shkraba |
| `nosotros.jpg` | [Caregiver taking care of a patient](https://www.pexels.com/photo/7345459/) | Antoni Shkraba |
| `enfermeria.jpg` | [Caregiver taking care of a patient on bed](https://www.pexels.com/photo/18459210/) | Jsme MILA |
| `traslados.jpg` | [Man pulling out a stretcher](https://www.pexels.com/photo/6519935/) | RDNE Stock project |
| `ambulancia.jpg` | [Paramedics next to an ambulance](https://www.pexels.com/photo/6519887/) | RDNE Stock project |

El logo es propio (SVG) y las tipografías pertenecen a Google Fonts.

---

## Sitio de ejemplo

Este proyecto es una **maqueta educativa**. El nombre del profesional, la
matrícula, los años de experiencia, la cantidad de familias, las zonas, los
horarios y los datos de contacto son **ficticios**. Antes de
publicarlo:

- reemplazá todos los datos marcados con `<!-- REEMPLAZAR: ... -->`;
- verificá que el profesional y la matrícula sean reales;
- revisá que las afirmaciones sobre servicios y zonas sean correctas;
- confirmá que las imágenes puedan usarse;
- y no prometas atención de urgencias: el sitio deriva al 107 y al 911.
