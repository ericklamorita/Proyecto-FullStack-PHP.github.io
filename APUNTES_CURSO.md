# Apuntes del curso Full Stack — Erick

Este documento reúne de forma acumulativa los conceptos, ejemplos, correcciones y reglas aprendidas durante el desarrollo de **Proyecto Full Stack PHP**.

> Regla de actualización: cada tema nuevo se agregará en su capítulo correspondiente. HTML, CSS, JavaScript, PHP y MySQL tendrán secciones separadas y ordenadas.

## Índice

1. [Capítulo 0 — Entorno y funcionamiento de una aplicación web](#capítulo-0--entorno-y-funcionamiento-de-una-aplicación-web)
2. [Capítulo 1 — Fundamentos de HTML](#capítulo-1--fundamentos-de-html)
3. [Práctica actual](#práctica-actual)
4. [Temas futuros](#temas-futuros)

---

# Capítulo 0 — Entorno y funcionamiento de una aplicación web

## 0.1 Herramientas utilizadas

| Herramienta | Función principal |
|---|---|
| VS Code | Escribir y organizar el código |
| XAMPP | Proporcionar Apache, PHP y MySQL en la computadora |
| Apache | Recibir solicitudes HTTP y entregar respuestas |
| PHP | Ejecutar la lógica del servidor |
| MySQL | Guardar información permanentemente |
| Navegador | Solicitar páginas y mostrar el resultado |
| DevTools | Inspeccionar solicitudes, respuestas y errores |
| Git | Registrar versiones locales del proyecto |
| GitHub | Guardar y compartir el repositorio remoto |

## 0.2 Abrir un archivo no es lo mismo que solicitarlo al servidor

### Archivo abierto directamente

```text
file:///C:/xampp/htdocs/Proyecto-FullStack-PHP/index.php
```

El navegador abre el archivo desde Windows. En este caso, Apache no participa y el código PHP no se ejecuta correctamente.

### Página solicitada a Apache

```text
http://localhost/Proyecto-FullStack-PHP/
```

El navegador envía una solicitud a Apache. Apache reconoce el archivo PHP, permite que PHP lo procese y devuelve al navegador el resultado generado.

| Dirección | Resultado |
|---|---|
| `file:///` | Abre un archivo local directamente |
| `http://localhost/` | Solicita una página al servidor Apache |

### Regla importante

> Los proyectos con PHP siempre deben probarse mediante `http://localhost`, no abriendo el archivo directamente.

## 0.3 Datos observados en DevTools

En `F12 → Network` se observó:

| Dato | Valor | Significado |
|---|---|---|
| Request URL | `http://localhost/Proyecto-FullStack-PHP/` | Dirección solicitada |
| Request Method | `GET` | Solicitud para obtener un recurso |
| Status Code | `200 OK` | Apache entregó una respuesta |
| Remote Address | `[::1]:80` | La propia computadora mediante IPv6 y el puerto 80 |
| Referrer Policy | `strict-origin-when-cross-origin` | Política de seguridad del navegador |

Un estado `200 OK` indica que el servidor respondió, pero no garantiza que el contenido de la aplicación sea correcto. Una configuración de PHP puede devolver un mensaje de error dentro de una respuesta con estado 200.

## 0.4 Responsabilidad de cada tecnología

| Tecnología | Responsabilidad |
|---|---|
| HTML | Estructura y significado del contenido |
| CSS | Diseño y presentación visual |
| JavaScript | Interacción y cambios en el navegador |
| Apache | Recibir inicialmente las solicitudes HTTP |
| PHP | Procesar datos, aplicar reglas y tomar decisiones seguras |
| MySQL | Almacenar y consultar datos permanentes |

### Regla para memorizar

```text
HTML estructura
CSS presenta
JavaScript interactúa
Apache recibe
PHP decide
MySQL almacena
```

## 0.5 Ejemplo del flujo de una compra

1. JavaScript puede actualizar visualmente el carrito.
2. JavaScript muestra un total provisional.
3. El usuario presiona “Realizar pedido”.
4. El navegador envía los datos.
5. Apache recibe la solicitud.
6. PHP procesa la información.
7. PHP consulta en MySQL los precios y el inventario verdaderos.
8. PHP calcula el total definitivo.
9. MySQL guarda el pedido.
10. PHP genera una respuesta y Apache la entrega al navegador.

> El frontend puede ayudar al usuario, pero el backend debe comprobar toda información importante.

No debemos confiar en precios, permisos, existencias ni totales enviados únicamente desde JavaScript, porque el usuario puede modificar el código que se ejecuta en su navegador.

## 0.6 Flujo general de una solicitud

```text
Navegador → Apache → PHP → MySQL
                         ↓
Navegador ← Apache ← respuesta generada
```

Apache recibe la solicitud, pero normalmente no extrae por sí mismo los productos. PHP consulta MySQL y genera la respuesta.

## 0.7 Tipos básicos de errores

| Tipo | Ejemplo |
|---|---|
| Sintaxis | Falta un `;` en PHP |
| Ejecución | Se intenta utilizar una función inexistente |
| Lógica | El programa ejecuta, pero calcula un resultado incorrecto |
| HTTP | Se obtiene un estado como `404` o `500` |
| Base de datos | Falla la conexión o una consulta SQL |
| Visual | La página funciona, pero se muestra incorrectamente |

### `syntax error` y `parse error`

- **Syntax error:** el código incumple las reglas de escritura del lenguaje.
- **Parse error:** el analizador no logra interpretar el programa debido a un error de sintaxis.

La línea mostrada en el error es donde PHP detectó el problema. La causa real también puede encontrarse en la línea anterior.

### Comprobación de sintaxis de PHP

Desde la terminal del proyecto:

```powershell
C:\xampp\php\php.exe -l index.php
```

Resultado esperado:

```text
No syntax errors detected in index.php
```

## 0.8 Flujo de trabajo con Git

```text
Editar → Guardar → Probar en localhost → Commit → Push
```

- `Ctrl + S` guarda el archivo local.
- XAMPP ejecuta el archivo local.
- `commit` registra una versión en Git.
- `push` envía los commits a GitHub.
- Hacer `push` no cambia lo que XAMPP muestra en la computadora.

Los errores intencionales de un laboratorio deben corregirse antes de hacer `commit` y `push`.

---

# Capítulo 1 — Fundamentos de HTML

## 1.1 ¿Qué es HTML?

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

## 1.2 Atributos

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

## 1.3 Estructura básica de un documento

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

## 1.4 Jerarquía de encabezados

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

## 1.5 HTML semántico

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

## 1.6 Diferencia entre `section`, `article` y `div`

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

## 1.7 Navegación con `nav`

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

## 1.8 Relación entre `href` e `id`

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

## 1.9 Tipos de valores de `href`

| `href` | Resultado |
|---|---|
| `#productos` | Se desplaza hasta un elemento de la página actual |
| `productos.php` | Abre otra página del proyecto |
| `https://ejemplo.com` | Abre otro sitio web |
| `productos.php#cargador` | Abre otra página y busca una sección específica |

## 1.10 Enlaces externos

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

## 1.11 Otros usos de `id`

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

## 1.12 Navegación principal e índice de productos

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

---

# Práctica actual

## Laboratorio 1.1 — Primera estructura de la tienda

Archivo de trabajo:

```text
C:\xampp\htdocs\Proyecto-FullStack-PHP\index.php
```

La página debe probarse mediante:

```text
http://localhost/Proyecto-FullStack-PHP/
```

## Estado de la revisión actual

La versión presentada ya contiene una estructura HTML válida, tres productos semánticos y enlaces externos visibles. Para cerrar el laboratorio todavía falta transformar el menú en una navegación de secciones generales, normalizar los identificadores, agregar una cuarta opción y crear las secciones de bienvenida y retiro físico.

## Requisitos pendientes de la segunda versión

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

## Errores corregidos durante la práctica

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

# Temas futuros

Estas secciones se completarán progresivamente durante el curso:

## HTML

- Formularios.
- Tablas.
- Imágenes.
- Accesibilidad.
- Validación básica.
- Organización en varias páginas.

## CSS

- Selectores.
- Modelo de caja.
- Colores y tipografía.
- Flexbox.
- Grid.
- Diseño adaptable.

## JavaScript

- Variables y tipos de datos.
- Condiciones y ciclos.
- Funciones.
- DOM.
- Eventos.
- Solicitudes con `fetch`.

## PHP

Cuando comience PHP, los apuntes se organizarán como un capítulo independiente:

- Sintaxis básica.
- Variables y tipos.
- Condiciones y ciclos.
- Funciones.
- Formularios con GET y POST.
- Validaciones.
- Sesiones.
- Seguridad.
- Organización del backend.
- Manejo de errores.

## MySQL

- Bases de datos y tablas.
- Tipos de datos.
- Claves primarias y foráneas.
- Consultas SQL.
- Relaciones.
- CRUD.
- Conexión segura mediante PDO.
- Consultas preparadas.
