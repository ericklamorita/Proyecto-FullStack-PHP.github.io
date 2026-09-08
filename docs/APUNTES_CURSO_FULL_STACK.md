# Apuntes del curso de Desarrollo Web Full Stack

**Estudiante:** Erick Mora Herrera  
**Proyecto práctico:** Tienda Don Erick  
**Tecnologías:** HTML, CSS, JavaScript, PHP y MySQL  
**Última actualización:** 8 de septiembre de 2026

Este documento reúne la teoría, los ejemplos, las dudas, las correcciones y las reglas importantes estudiadas durante el curso. Se actualizará conforme avancemos. No es una copia literal del chat: organiza lo aprendido para que pueda consultarse como una guía de estudio.

## Progreso del curso

| Capítulo | Tema | Estado |
| --- | --- | --- |
| 0.1 | Entorno local con XAMPP | Completado |
| 0.2 | Responsabilidades de cada tecnología | Completado |
| 0.3 | Flujo de trabajo y errores | Completado |
| 1.1 | Anatomía y semántica de HTML | En progreso |

---

# Capítulo 0. Preparación del entorno

## 0.1 XAMPP y `localhost`

XAMPP proporciona, entre otras herramientas, Apache y MySQL. Apache recibe las solicitudes web y permite ejecutar PHP. MySQL almacenará los datos permanentes de la tienda.

| Componente | Función principal | Si está detenido |
| --- | --- | --- |
| Apache | Recibe solicitudes HTTP y entrega respuestas | El sitio PHP en `localhost` no responde |
| PHP | Ejecuta el código del servidor | Las instrucciones PHP no pueden procesarse |
| MySQL | Almacena información permanente | Fallan las funciones que consultan datos |

### Abrir un archivo y solicitar una página

| Dirección | Qué ocurre |
| --- | --- |
| `file:///C:/xampp/htdocs/Proyecto-FullStack-PHP/index.php` | El navegador abre un archivo local. PHP no pasa por Apache. |
| `http://localhost/Proyecto-FullStack-PHP/` | El navegador envía una solicitud a Apache y PHP puede ejecutarse. |

Regla para recordar:

```text
file:///          → abre un archivo directamente
http://localhost/ → solicita una página al servidor
```

### Lectura de una solicitud en DevTools

| Dato | Ejemplo observado | Significado |
| --- | --- | --- |
| Request URL | `http://localhost/Proyecto-FullStack-PHP/` | Recurso solicitado |
| Request Method | `GET` | El navegador solicita obtener el recurso |
| Status Code | `200 OK` | Apache entregó una respuesta |
| Remote Address | `[::1]:80` | La propia computadora mediante IPv6, en el puerto 80 |
| Content-Type | `text/html` | La respuesta contiene HTML |

Un estado `200 OK` confirma que se entregó una respuesta, pero no garantiza que la aplicación esté correctamente programada. Esa respuesta podría contener un mensaje de error de PHP.

## 0.2 Separación de responsabilidades

| Tecnología | Responsabilidad | Ejemplo en la tienda |
| --- | --- | --- |
| HTML | Estructura y significado | Tarjeta, título y descripción de un producto |
| CSS | Presentación visual | Color, tamaño y distribución de un botón |
| JavaScript | Interacción en el navegador | Abrir el carrito o calcular un total provisional |
| Apache | Recepción y entrega HTTP | Recibir `GET /productos` |
| PHP | Procesamiento, seguridad y reglas | Verificar roles y calcular el total definitivo |
| MySQL | Almacenamiento permanente | Guardar inventario, usuarios y pedidos |

Resumen corto:

```text
HTML estructura
CSS presenta
JavaScript interactúa
Apache recibe
PHP decide
MySQL almacena
```

### Ejemplo del carrito

1. JavaScript abre el carrito y puede mostrar un total provisional.
2. El cliente confirma la compra y el navegador envía la información.
3. Apache recibe la solicitud y la dirige a PHP.
4. PHP consulta en MySQL los precios y las existencias reales.
5. PHP calcula el total definitivo, comprueba permisos e inventario y guarda el pedido.
6. La respuesta vuelve al navegador y se muestra la confirmación.

> El frontend ayuda al usuario, pero el backend debe comprobar la información importante.

Un usuario puede modificar JavaScript desde el navegador. Por eso nunca debemos confiar directamente en precios, permisos, existencias ni totales enviados por el frontend.

### Correcciones del laboratorio 0.2

| Operación | Responsable principal | Razón |
| --- | --- | --- |
| Abrir y cerrar visualmente el carrito | JavaScript | Reacciona al clic y cambia el estado visible |
| Recibir `GET /productos` | Apache | Es el primer componente del servidor que recibe la solicitud HTTP |
| Mostrar un total sin recargar | JavaScript | Modifica el contenido mostrado en el navegador |
| Guardar un pedido | PHP y MySQL | PHP procesa la operación y MySQL conserva los datos |
| Comprobar inventario | PHP y MySQL | PHP consulta los datos y decide si la venta puede realizarse |

## 0.3 Flujo de trabajo del desarrollador

Cada cambio del proyecto seguirá este ciclo:

```text
Entender → Editar → Guardar → Probar → Revisar → Corregir → Commit → Push
```

- `Ctrl + S` guarda el archivo local y sí afecta lo que ejecuta XAMPP.
- `commit` registra una versión en Git.
- `push` envía los commits a GitHub.
- Hacer `push` no actualiza ni repara el archivo que XAMPP ejecuta en la computadora.
- Conviene probar cambios pequeños para identificar con facilidad cuál modificación causó un error.

El orden correcto es:

```text
Editar → Guardar → Probar en localhost → Commit → Push
```

### Tipos básicos de errores

| Tipo | Ejemplo | Qué revisar |
| --- | --- | --- |
| Sintaxis | Falta un `;` en PHP | La línea indicada y la anterior |
| Ejecución | Se llama una función inexistente | Nombre, parámetros y disponibilidad |
| Lógica | El programa suma incorrectamente | Datos, condiciones y fórmula |
| HTTP | Respuesta `404` o `500` | Ruta, servidor y registro de errores |
| Base de datos | Conexión o consulta incorrecta | Credenciales, servicio y SQL |
| Visual | La página funciona, pero se ve mal | HTML, estilos y tamaño de pantalla |

### Laboratorio de error de sintaxis

Se eliminó temporalmente el punto y coma de una instrucción `echo`:

```php
<?php

echo "XAMPP y PHP están funcionando correctamente"
```

PHP mostró un `parse error` o `syntax error` porque el código incumplía sus reglas de escritura y el analizador no podía interpretarlo.

La línea señalada es donde PHP detecta el problema, pero la causa puede estar en esa línea o en la anterior.

Versión correcta:

```php
<?php

echo "XAMPP y PHP están funcionando correctamente";
```

---

# Capítulo 1. Fundamentos de HTML

## 1.1 Anatomía de un documento HTML

HTML significa **HyperText Markup Language**. Es un lenguaje de marcado: describe la estructura y el significado del contenido. Por sí solo no toma decisiones ni ejecuta ciclos como un lenguaje de programación.

### Etiqueta, elemento, atributo y contenido

```html
<a href="catalogo.html">Ver catálogo</a>
```

| Parte | Ejemplo | Función |
| --- | --- | --- |
| Etiqueta de apertura | `<a>` | Inicia el elemento |
| Atributo | `href` | Agrega información o configuración |
| Valor del atributo | `catalogo.html` | Indica el destino del enlace |
| Contenido | `Ver catálogo` | Texto visible para el usuario |
| Etiqueta de cierre | `</a>` | Finaliza el elemento |
| Elemento completo | `<a href="catalogo.html">Ver catálogo</a>` | Unión de apertura, atributos, contenido y cierre |

### Estructura general de un documento

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tienda Don Erick</title>
</head>
<body>
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
</body>
</html>
```

| Elemento | Propósito |
| --- | --- |
| `<!DOCTYPE html>` | Declara que el documento utiliza HTML5 |
| `<html lang="es">` | Contiene el documento e indica que su idioma es español |
| `<head>` | Contiene metadatos y configuración para el navegador |
| `<meta charset="UTF-8">` | Permite representar correctamente tildes, ñ y otros caracteres |
| `<meta name="viewport" ...>` | Prepara la página para distintos tamaños de pantalla |
| `<title>` | Define el texto de la pestaña del navegador |
| `<body>` | Contiene lo visible en la página |

El archivo `index.php` puede contener HTML normalmente. La extensión `.php` permite añadir código del servidor más adelante, pero no obliga a usar PHP en cada línea.

### Diferencia entre `title` y `h1`

| Elemento | Dónde aparece | Función |
| --- | --- | --- |
| `<title>` | En la pestaña del navegador | Identifica el documento para el navegador |
| `<h1>` | Dentro de la página | Presenta el encabezado principal al usuario |

## 1.2 HTML semántico

Una etiqueta semántica comunica para qué sirve el contenido. Esto ayuda a navegadores, buscadores, lectores de pantalla y desarrolladores a comprender la página.

| Etiqueta | Significado | Uso en la tienda |
| --- | --- | --- |
| `<header>` | Encabezado del sitio o de una sección | Nombre, descripción y navegación |
| `<nav>` | Conjunto importante de enlaces de navegación | Inicio, productos, retiro y contacto |
| `<main>` | Contenido principal y único de la página | Secciones centrales de la tienda |
| `<section>` | Agrupación temática | Productos destacados o retiro en tienda |
| `<article>` | Unidad independiente y reutilizable | Un producto con nombre, descripción y precio |
| `<footer>` | Información final | Datos finales, derechos o contacto |
| `<div>` | Agrupación sin significado semántico | Apoyo para el diseño cuando sea necesario |

### Diferencia entre `section` y `article`

Una `section` agrupa contenidos relacionados. Cada `article` representa una unidad que conserva sentido por sí sola.

```html
<section id="productos">
    <h2>Productos destacados</h2>

    <article id="cargador-telefono">
        <h3>Cargador de teléfono</h3>
        <p>Precio: ₡1 900</p>
    </article>

    <article id="cargador-carro">
        <h3>Cargador para carro</h3>
        <p>Precio: ₡1 000</p>
    </article>
</section>
```

La relación es:

```text
section: Productos destacados
├── article: Cargador de teléfono
└── article: Cargador para carro
```

`article` no significa únicamente artículo de periódico. También puede representar un producto, noticia, receta, comentario o publicación independiente.

### Jerarquía de encabezados

```text
h1: Tienda Don Erick
└── h2: Productos destacados
    └── h3: Cargador de teléfono
```

- `h1`: tema principal de la página.
- `h2`: título de una sección principal.
- `h3`: título de un elemento o subsección dentro de un `h2`.

Una dirección web no debe colocarse dentro de `h3` solamente para destacarla. Si representa un destino, se debe utilizar un enlace.

## 1.3 Enlaces, navegación e identificadores

El elemento `a` crea un enlace y su atributo `href` define el destino. El elemento `nav` identifica un grupo de enlaces importantes, pero no carga productos ni consulta datos.

### Enlace interno

Un enlace interno desplaza la vista hacia otro elemento del mismo documento:

```html
<nav>
    <ul>
        <li><a href="#productos">Productos</a></li>
    </ul>
</nav>

<section id="productos">
    <h2>Productos</h2>
</section>
```

La dirección del enlace apunta hacia el identificador:

```text
href="#productos" → busca → id="productos"
```

El `id` no llama al enlace. El enlace utiliza `href` para buscar el elemento identificado por `id`.

Si la página es corta, puede parecer que no sucede nada porque no existe suficiente espacio para desplazarse. La barra de direcciones debería terminar en `#productos` si el enlace funciona.

### Utilidades de `id`

Un `id` identifica un elemento único dentro del documento.

| Uso | Ejemplo | Resultado |
| --- | --- | --- |
| Enlace interno | `<a href="#productos">` | Busca el elemento con `id="productos"` |
| CSS, más adelante | `#productos { ... }` | Selecciona ese elemento para aplicarle estilos |
| JavaScript, más adelante | `document.getElementById("productos")` | Obtiene ese elemento para interactuar con él |

### Reglas para los identificadores

- Deben ser únicos dentro de la página.
- Se escribirán en minúsculas.
- No se usarán tildes ni espacios.
- Las palabras se separarán con guiones.
- Deben describir claramente el elemento.
- El valor después de `#` en `href` debe coincidir exactamente con el `id`.

```html
<!-- Recomendado -->
<a href="#cargador-telefono">Cargador de teléfono</a>
<article id="cargador-telefono">...</article>

<!-- Evitar -->
<a href="#cargador-telefono">Cargador de teléfono</a>
<article id="Cargador-de-teléfono">...</article>
```

### Tipos de destinos en `href`

| Valor de `href` | Resultado |
| --- | --- |
| `#productos` | Se desplaza dentro de la página actual |
| `productos.php` | Abre otra página del proyecto |
| `https://ejemplo.com` | Abre otro sitio web |
| `productos.php#cargador` | Abre otra página y busca una sección |

### Enlace externo y contenido visible

Un enlace vacío no muestra nada:

```html
<a href="https://ejemplo.com/producto"></a>
```

Debe incluir contenido comprensible entre la etiqueta de apertura y la de cierre:

```html
<a href="https://ejemplo.com/producto">Ver información del producto</a>
```

### Navegación principal e índice de productos

| Tipo | Ejemplos | Ubicación recomendada |
| --- | --- | --- |
| Navegación principal | Inicio, productos, retiro, contacto | Dentro de `header` |
| Índice de productos | Cargador de teléfono, cargador de carro | Cerca de la sección de productos |

## Laboratorio 1.1. Primera estructura de la tienda

**Objetivo:** construir la primera estructura semántica de Tienda Don Erick sin CSS, JavaScript, PHP ni Bootstrap.

### Trabajo realizado correctamente

- Documento HTML5 completo.
- Idioma configurado en español.
- Codificación UTF-8 y configuración para dispositivos móviles.
- Título de la pestaña y `h1` principal.
- Uso de `header`, `main`, `section`, `article` y `footer`.
- Productos separados en unidades independientes.
- Etiquetas correctamente cerradas e indentación clara.

### Correcciones y aprendizaje

| Situación | Corrección | Aprendizaje |
| --- | --- | --- |
| Producto marcado con `h2` dentro de una sección `h2` | Usar `h3` para el producto | Mantener una jerarquía clara |
| URL escrita dentro de `h3` | Usar `a` con `href` y texto visible | La etiqueta debe corresponder a la función del contenido |
| Producto convertido en `section` | Conservar `article` | El producto es una unidad independiente |
| Enlace externo vacío | Escribir texto entre `<a>` y `</a>` | Un enlace necesita contenido visible |
| `id` con mayúsculas y tildes | Usar minúsculas, guiones y sin tildes | Una convención consistente evita errores |

### Requisitos pendientes

- Mantener el documento HTML5 completo y correctamente indentado.
- Usar `h1` para la tienda, `h2` para las secciones y `h3` para cada producto.
- Agregar navegación principal con cuatro enlaces: inicio, productos, retiro y contacto.
- Crear los `id` correspondientes y comprobar que los enlaces internos funcionan.
- Conservar cada producto como `article`.
- Agregar texto visible a los enlaces externos.
- Crear una sección de bienvenida.
- Crear una sección de retiro en tienda.
- Crear una sección o información de contacto.
- Probar mediante `http://localhost/Proyecto-FullStack-PHP/` antes de realizar `commit` y `push`.

## Lista rápida de comprobación

- [ ] ¿La página se abre desde `http://localhost` y no desde `file:///`?
- [ ] ¿Todas las etiquetas están correctamente cerradas y anidadas?
- [ ] ¿Solo existe un `h1` principal?
- [ ] ¿Cada sección tiene un encabezado apropiado?
- [ ] ¿Cada producto está representado mediante `article`?
- [ ] ¿Los valores `href` con `#` coinciden exactamente con un `id`?
- [ ] ¿Los enlaces contienen texto visible?
- [ ] ¿La versión funciona antes de realizar `commit` y `push`?

## Próximo paso

Completar y revisar la segunda versión de `index.php` del Laboratorio 1.1. Después se cerrará la lección de anatomía HTML y se continuará con el siguiente tema del capítulo.

---

## Regla de mantenimiento de estos apuntes

Cuando se estudie un concepto nuevo, este documento se actualizará con:

1. Definición clara.
2. Explicación de para qué sirve.
3. Sintaxis o estructura.
4. Ejemplo distinto al laboratorio.
5. Aplicación en Tienda Don Erick.
6. Tabla comparativa cuando ayude a distinguir conceptos.
7. Errores frecuentes y sus correcciones.
8. Regla corta para recordar.
9. Estado del laboratorio y siguiente paso.
