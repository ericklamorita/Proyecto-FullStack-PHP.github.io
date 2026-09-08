# Entorno y funcionamiento de una aplicación web

[← Volver al índice general](../APUNTES_CURSO.md)

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
