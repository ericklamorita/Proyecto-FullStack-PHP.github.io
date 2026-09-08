# HTML

[← Volver al índice general](../APUNTES_CURSO.md)

## Lección 1.1 — Anatomía y estructura semántica

### 1.1.1 ¿Qué es HTML?

HTML significa **HyperText Markup Language** o lenguaje de marcado de hipertexto.

HTML describe la estructura y el significado del contenido. No es un lenguaje de programación porque, por sí solo, no contiene decisiones, ciclos ni lógica de programación.

Ejemplo:

```html
<h1>Biblioteca Central</h1>
```

| Parte | Código |
|---|---|
| Etiqueta de apertura | `<h1>` |
| Contenido | `Biblioteca Central` |
| Etiqueta de cierre | `</h1>` |
| Elemento completo | `<h1>Biblioteca Central</h1>` |

### 1.1.2 Atributos

Los atributos agregan información a un elemento.

```html
<a href="catalogo.html">Ver catálogo</a>
```

| Parte | Valor |
|---|---|
| Elemento | `a` |
| Atributo | `href` |
| Valor del atributo | `catalogo.html` |
| Texto visible | `Ver catálogo` |

Los valores de los atributos normalmente se escriben entre comillas.

### 1.1.3 Estructura básica de un documento

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Título de la pestaña</title>
</head>
<body>
    <header>
        <h1>Título principal</h1>
    </header>

    <main>
        <section>
            <h2>Título de una sección</h2>
        </section>
    </main>

    <footer>
        <p>Información final</p>
    </footer>
</body>
</html>
```

| Elemento | Función |
|---|---|
| `<!DOCTYPE html>` | Indica que el documento utiliza HTML5 |
| `<html lang="es">` | Elemento raíz e idioma del contenido |
| `<head>` | Información para el navegador |
| `<meta charset="UTF-8">` | Permite caracteres como tildes y ñ |
| `<meta name="viewport">` | Adapta la página a diferentes pantallas |
| `<title>` | Texto de la pestaña del navegador |
| `<body>` | Contenido visible de la página |
| `<header>` | Encabezado del sitio o de una sección |
| `<main>` | Contenido principal y único de la página |
| `<footer>` | Información final del sitio o de una sección |

### Diferencia entre `title` y `h1`

| Elemento | Dónde aparece |
|---|---|
| `<title>` | En la pestaña del navegador |
| `<h1>` | Dentro de la página |

### 1.1.4 Jerarquía de encabezados

Los encabezados deben representar la organización del contenido:

```text
h1: Título principal del sitio
└── h2: Título de una sección
    └── h3: Título de un producto o contenido dentro de la sección
```

Ejemplo correcto:

```html
<h1>Tienda Don Erick</h1>

<section>
    <h2>Productos destacados</h2>

    <article>
        <h3>Cargador de teléfono</h3>
    </article>
</section>
```

Si la sección ya tiene un `h2`, el nombre del producto normalmente debe ser un `h3`.

### 1.1.5 HTML semántico

Una etiqueta semántica describe la función de su contenido.

| Etiqueta | Significado |
|---|---|
| `<header>` | Encabezado |
| `<nav>` | Conjunto importante de enlaces de navegación |
| `<main>` | Contenido principal |
| `<section>` | Agrupación temática |
| `<article>` | Unidad independiente de contenido |
| `<footer>` | Pie del sitio o de una sección |
| `<div>` | Agrupación sin significado semántico específico |

La semántica ayuda a navegadores, buscadores, lectores de pantalla y programadores a comprender la página.

### 1.1.6 Diferencia entre `section`, `article` y `div`

| Elemento | Cuándo utilizarlo |
|---|---|
| `<section>` | Para agrupar contenidos relacionados bajo un tema |
| `<article>` | Para una unidad que puede entenderse de manera independiente |
| `<div>` | Para agrupar elementos cuando no existe una etiqueta semántica adecuada |

En una tienda:

```text
section: Productos destacados
├── article: Cargador de teléfono
├── article: Cargador para carro
└── article: Batería portátil
```

Cada producto puede utilizar `article` porque posee su propio nombre, descripción, precio, imagen y enlace.

```html
<section>
    <h2>Productos destacados</h2>

    <article>
        <h3>Cargador de teléfono</h3>
        <p>Precio: ₡1 900</p>
    </article>
</section>
```

`article` no significa únicamente un artículo de periódico. También puede representar productos, noticias, publicaciones, comentarios o recetas.

### 1.1.7 Navegación con `nav`

`nav` identifica un conjunto importante de enlaces. No carga productos, no consulta la base de datos y no ejecuta PHP.

```html
<nav>
    <ul>
        <li><a href="#inicio">Inicio</a></li>
        <li><a href="#productos">Productos</a></li>
        <li><a href="#retiro">Retiro en tienda</a></li>
        <li><a href="#contacto">Contacto</a></li>
    </ul>
</nav>
```

- `nav` representa la navegación.
- `ul` crea una lista sin numeración.
- `li` representa una opción de la lista.
- `a` crea el enlace.
- `href` indica el destino.

La navegación principal suele contener secciones generales. Un índice secundario puede contener enlaces hacia productos específicos.

### 1.1.8 Relación entre `href` e `id`

El enlace indica el destino y el `id` identifica el elemento de destino.

```html
<a href="#productos">Ir a productos</a>
```

```html
<section id="productos">
    <h2>Productos</h2>
</section>
```

La dirección de búsqueda es:

```text
href="#productos" → busca → id="productos"
```

El `id` no llama al enlace. Es el enlace el que busca el elemento cuyo identificador coincide.

### Reglas para escribir un `id`

- Debe ser único en la página.
- No debe contener espacios.
- Debe coincidir exactamente con el valor después de `#`.
- Es preferible escribirlo en minúsculas.
- Es preferible evitar tildes.
- Las palabras pueden separarse con guiones.

Ejemplo recomendado:

```html
<a href="#cargador-telefono">Cargador de teléfono</a>

<article id="cargador-telefono">
    <h3>Cargador de teléfono</h3>
</article>
```

Este ejemplo no funciona porque los valores son diferentes:

```html
<a href="#cargador-telefono">Cargador</a>
<article id="Cargador-de-teléfono">
```

### ¿Por qué a veces no se observa movimiento?

Si la página es muy corta y todo el contenido ya está visible, el navegador no tiene suficiente espacio para desplazarse. El enlace puede estar funcionando aunque el movimiento no sea evidente.

Una señal es que la dirección cambia a algo parecido a:

```text
http://localhost/Proyecto-FullStack-PHP/#productos
```

### 1.1.9 Tipos de valores de `href`

| `href` | Resultado |
|---|---|
| `#productos` | Se desplaza hasta un elemento de la página actual |
| `productos.php` | Abre otra página del proyecto |
| `https://ejemplo.com` | Abre otro sitio web |
| `productos.php#cargador` | Abre otra página y busca una sección específica |

### 1.1.10 Enlaces externos

Una dirección web no debe colocarse dentro de un encabezado solamente para mostrarla.

Incorrecto:

```html
<h3>https://ejemplo.com/producto</h3>
```

Correcto:

```html
<a href="https://ejemplo.com/producto">Ver información del producto</a>
```

Un enlace vacío no muestra nada:

```html
<a href="https://ejemplo.com/producto"></a>
```

El patrón general es:

```html
<a href="DIRECCIÓN">Texto visible para el usuario</a>
```

### 1.1.11 Otros usos de `id`

Además de los enlaces internos, un `id` podrá utilizarse más adelante desde CSS y JavaScript.

### CSS

```css
#cargador-telefono {
    color: blue;
}
```

### JavaScript

```javascript
document.getElementById("cargador-telefono");
```

Por ahora, lo importante es utilizarlo como identificador único y como destino de los enlaces internos.

### 1.1.12 Navegación principal e índice de productos

Aunque ambos se escriben con enlaces, cumplen propósitos distintos.

| Tipo | Contenido habitual | Ejemplo |
|---|---|---|
| Navegación principal | Secciones generales del sitio | Inicio, Productos, Retiro, Contacto |
| Índice de productos | Elementos específicos de un catálogo | Cargador, batería, audífonos |

La navegación principal ayuda al usuario a comprender las partes grandes de la página. Los enlaces hacia productos individuales pueden mantenerse como un índice secundario dentro de la sección de productos.

Ejemplo de otro contexto:

```html
<nav>
    <ul>
        <li><a href="#inicio">Inicio</a></li>
        <li><a href="#libros">Libros</a></li>
        <li><a href="#prestamos">Préstamos</a></li>
        <li><a href="#contacto">Contacto</a></li>
    </ul>
</nav>
```

Cada enlace necesita un destino con el mismo nombre:

```html
<section id="inicio">...</section>
<section id="libros">...</section>
<section id="prestamos">...</section>
<footer id="contacto">...</footer>
```

Un `id` también puede colocarse en `article` cuando se necesita enlazar directamente a un producto, pero eso no convierte automáticamente esos enlaces en una navegación principal.

### Convención de escritura adoptada

Para todos los identificadores del proyecto se utilizará:

```text
minúsculas + sin tildes + palabras-separadas-por-guiones
```

| Evitar | Preferir |
|---|---|
| `Cargador-de-teléfono` | `cargador-telefono` |
| `Cargador-para-carro` | `cargador-carro` |
| `Bateria-portatil` | `bateria-portatil` |

Esta convención reduce errores al relacionar HTML, CSS y JavaScript.

### 1.1.13 Un solo título principal y coincidencia exacta de destinos

Normalmente cada página debe tener un `h1` que identifique su tema principal. Los títulos de las secciones internas continúan con `h2`.

```html
<h1>Tienda Don Erick</h1>

<section id="inicio">
    <h2>Bienvenidos a Tienda Don Erick</h2>
</section>
```

Agregar otro `h1` a la bienvenida hace que ambos títulos parezcan tener el mismo nivel jerárquico. En este proyecto se mantendrá un solo `h1` por página para conservar una estructura sencilla y clara.

Los destinos internos distinguen mayúsculas, minúsculas, guiones y formas diferentes de escribir una palabra. Por eso esta pareja no coincide:

```html
<a href="#Retiro-en-tienda">Retiro</a>
<section id="retiroEnTienda">
```

Debe utilizarse exactamente el mismo identificador:

```html
<a href="#retiro">Retiro</a>
<section id="retiro">
```

### Lista de comprobación para un enlace interno

1. El `href` comienza con `#`.
2. El texto posterior a `#` existe como un `id`.
3. Ambos valores son exactamente iguales.
4. El `id` no se repite.
5. Se utiliza la convención de minúsculas, sin tildes y con guiones.

---

### Ubicación y ejecución

### Resultado final

**Estado: aprobado.** La versión final contiene un documento HTML5 completo, estructura semántica, jerarquía correcta de encabezados, navegación interna, tres productos independientes, retiro en tienda y contacto.

| Criterio | Resultado |
|---|---:|
| Documento HTML completo | 3/3 |
| Etiquetas semánticas | 3/3 |
| Jerarquía de encabezados | 2/2 |
| Anidamiento e indentación | 1/1 |
| Contenido solicitado | 1/1 |
| **Calificación** | **10/10** |

Corrección menor recomendada antes del commit del código:

```html
<!-- Evitar la tilde dentro del identificador -->
<article id="cargador-telefono">
```

Los cuatro pares de navegación quedaron definidos así:

| Enlace | Destino |
|---|---|
| `href="#inicio"` | `id="inicio"` |
| `href="#productos"` | `id="productos"` |
| `href="#retiro"` | `id="retiro"` |
| `href="#contacto"` | `id="contacto"` |

## Laboratorio 1.1 — Primera estructura de la tienda

Archivo de trabajo:

```text
C:\xampp\htdocs\Proyecto-FullStack-PHP\index.php
```

La página debe probarse mediante:

```text
http://localhost/Proyecto-FullStack-PHP/
```

### Estado de la revisión

La versión presentada ya contiene una estructura HTML válida, tres productos semánticos y enlaces externos visibles. Para cerrar el laboratorio todavía falta transformar el menú en una navegación de secciones generales, normalizar los identificadores, agregar una cuarta opción y crear las secciones de bienvenida y retiro físico.

### Requisitos evaluados

- [x] Mantener el documento HTML5 completo.
- [x] Utilizar un solo `h1` principal.
- [x] Utilizar `h2` para las secciones.
- [x] Utilizar `h3` para los nombres de productos.
- [x] Mantener cada producto dentro de un `article`.
- [x] Convertir las direcciones externas en enlaces con texto visible.
- [ ] Agregar una navegación con cuatro secciones generales.
- [ ] Agregar los `id` que correspondan a los enlaces internos.
- [ ] Crear una sección de bienvenida.
- [ ] Crear una sección sobre retiro en tienda física.
- [x] Mantener el laboratorio sin CSS, JavaScript, PHP ni Bootstrap.
- [ ] Probar todos los enlaces desde `localhost`.
- [ ] Revisar antes de hacer `commit` y `push`.

### Errores corregidos

| Situación | Corrección |
|---|---|
| Productos escritos como `h2` dentro de una sección con `h2` | Usar `h3` para cada producto |
| Dirección web colocada como encabezado | Utilizar un enlace `a` con `href` |
| Enlace externo sin texto visible | Escribir contenido entre `<a>` y `</a>` |
| Producto representado como otra `section` | Mantenerlo como `article` |
| Identificadores con mayúsculas y tildes | Usar minúsculas, sin tildes y con guiones |
| Creer que `id` llama al enlace | Recordar que `href="#nombre"` busca `id="nombre"` |
| Menú principal dirigido solo a productos | Usar secciones generales para la navegación principal |
---

## Lección 1.2 — Imágenes, rutas y atributos importantes

### 1.2.1 El elemento `img`

Una imagen se incorpora con el elemento `img`:

```html
<img src="imagenes/paisaje.jpg" alt="Montañas verdes bajo un cielo azul">
```

`img` es un elemento vacío: no contiene texto interno y no utiliza una etiqueta de cierre `</img>`.

| Parte | Función |
|---|---|
| `img` | Indica que se mostrará una imagen |
| `src` | Especifica dónde se encuentra el archivo |
| `alt` | Describe la imagen cuando no puede verse |

### 1.2.2 Importancia de `alt`

El atributo `alt` no debe limitarse a repetir “imagen”. Debe comunicar la información relevante que aporta la imagen.

| Imagen | `alt` adecuado |
|---|---|
| Producto | `alt="Cargador de pared blanco con puerto USB"` |
| Logotipo | `alt="Tienda Don Erick"` |
| Decoración sin significado | `alt=""` |

El texto alternativo ayuda a personas que utilizan lectores de pantalla y también aparece conceptualmente cuando la imagen no puede cargarse.

### 1.2.3 Rutas relativas

Una ruta relativa parte desde la ubicación del archivo HTML o PHP actual.

Supongamos esta estructura:

```text
Proyecto-FullStack-PHP/
├── index.php
└── assets/
    └── images/
        └── cargador.jpg
```

Desde `index.php`, la ruta es:

```html
<img src="assets/images/cargador.jpg" alt="Cargador de pared">
```

| Ruta | Significado |
|---|---|
| `foto.jpg` | El archivo está en la misma carpeta |
| `images/foto.jpg` | Está dentro de una subcarpeta |
| `assets/images/foto.jpg` | Está dentro de dos subcarpetas |
| `../foto.jpg` | Se sube una carpeta para buscar el archivo |
| `https://sitio.com/foto.jpg` | La imagen se obtiene desde otro sitio web |

En HTML se utiliza `/`, incluso cuando el proyecto está en Windows. No se deben escribir rutas locales como:

```text
C:\Users\Erick\Pictures\foto.jpg
```

Esa dirección solo existe en la computadora de Erick y dejaría de funcionar al publicar la página.

### 1.2.4 Nombres de archivos

Para evitar errores se utilizará esta convención:

```text
minúsculas + sin tildes + sin espacios + guiones
```

| Evitar | Preferir |
|---|---|
| `Cargador Teléfono.JPG` | `cargador-telefono.jpg` |
| `Batería portátil.png` | `bateria-portatil.png` |

La extensión escrita en `src` debe coincidir con el archivo real. `.jpg`, `.png` y `.webp` no son intercambiables.

### 1.2.5 Formatos comunes

| Formato | Uso habitual |
|---|---|
| JPEG/JPG | Fotografías con muchos colores |
| PNG | Imágenes que necesitan transparencia |
| WebP | Imágenes web con buena compresión |
| SVG | Logotipos, iconos y gráficos vectoriales |

### 1.2.6 `figure` y `figcaption`

Cuando una imagen necesita un texto explicativo asociado, puede agruparse así:

```html
<figure>
    <img src="assets/images/montana.jpg" alt="Sendero rodeado de montañas">
    <figcaption>Ruta principal del parque nacional.</figcaption>
</figure>
```

- `figure` agrupa contenido visual independiente.
- `figcaption` proporciona una leyenda visible.
- `alt` sigue siendo necesario porque cumple una función de accesibilidad diferente.

### 1.2.7 Errores frecuentes

| Error | Consecuencia |
|---|---|
| Ruta o extensión incorrecta | La imagen no aparece y puede producirse un `404` |
| Usar `\` en la ruta | El enlace no sigue la convención web |
| Escribir una ruta de Windows | Solo funciona en una computadora específica |
| Omitir `alt` | Se reduce la accesibilidad |
| Utilizar una URL de otra tienda | La imagen depende de un servidor ajeno |
| Cambiar el nombre del archivo sin cambiar `src` | La ruta deja de coincidir |

### Laboratorio 1.2 — Imágenes locales de productos

Objetivo: agregar una imagen local a cada producto sin utilizar CSS.

1. Crear dentro del proyecto las carpetas `assets/images`.
2. Conseguir tres imágenes propias o autorizadas para la práctica.
3. Renombrarlas usando minúsculas, sin tildes ni espacios.
4. Colocar cada archivo dentro de `assets/images`.
5. Agregar un elemento `img` dentro de cada `article`, después del `h3`.
6. Escribir un `alt` específico para cada producto.
7. Probar la página desde `http://localhost/Proyecto-FullStack-PHP/`.
8. Revisar en Network si alguna imagen devuelve `404`.

Restricciones del laboratorio:

- No utilizar CSS todavía.
- No escribir rutas absolutas de Windows.
- No copiar el ejemplo como solución completa.
- No hacer `push` hasta que las tres imágenes aparezcan correctamente.

