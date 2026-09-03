# Proyecto Full Stack PHP

Proyecto educativo para aprender desarrollo **frontend y backend desde los fundamentos**, construyendo progresivamente una tienda híbrida que pueda operar en línea y apoyar la administración de un futuro local físico.

> Estado actual: planificación y preparación del entorno.  
> El código y las carpetas de la aplicación serán creados por Erick durante las clases.

## 1. Objetivos

Este proyecto busca cumplir tres objetivos:

1. Reforzar los conocimientos necesarios para la universidad.
2. Desarrollar habilidades prácticas para optar por un trabajo en programación.
3. Construir una base adaptable a un emprendimiento real.

La aplicación no estará limitada a una clase específica de producto. Se utilizará un modelo flexible con productos, categorías, inventario, clientes, pedidos, ventas y proveedores.

## 2. Alcance de la tienda híbrida

### Tienda en línea

- Catálogo público de productos.
- Búsqueda y filtros por categorías.
- Registro e inicio de sesión.
- Carrito de compras.
- Creación y seguimiento de pedidos.
- Selección entre envío y retiro en tienda.
- Pago por SINPE Móvil.
- Historial del cliente.

### Administración de la tienda física

- Registro de ventas presenciales.
- Administración de productos y categorías.
- Control de inventario compartido.
- Administración de proveedores.
- Consulta y actualización de pedidos.
- Confirmación de pagos.
- Alertas de existencias.
- Reportes de ventas.

Las ventas físicas y en línea utilizarán el mismo inventario.

## 3. Tecnologías planeadas

- HTML5.
- CSS3.
- JavaScript.
- PHP.
- MySQL.
- PDO.
- Firebase Authentication.
- Git y GitHub.
- n8n para automatizaciones.
- WhatsApp Business Cloud en una etapa posterior.

Después de completar y comprender el backend en PHP, se estudiará cómo reconstruir partes del sistema con Node.js.

## 4. Autenticación con Firebase

Se creará un proyecto nuevo en Firebase. Inicialmente se implementará:

- Registro con correo y contraseña.
- Inicio y cierre de sesión.
- Identificación del usuario autenticado.
- Verificación del token de Firebase desde el backend.
- Relación entre el UID de Firebase y la información almacenada en MySQL.
- Inicio de sesión con Google en una etapa posterior.

Las credenciales privadas, cuentas de servicio y contraseñas de bases de datos no deben almacenarse en GitHub.

## 5. Estados de los pedidos

El flujo inicial contemplará los siguientes estados:

1. `pendiente_pago`
2. `comprobante_recibido`
3. `pago_por_verificar`
4. `pagado`
5. `preparando`
6. `listo_para_retirar`
7. `entregado`
8. `cancelado`

Una imagen del comprobante no confirmará automáticamente el pago. La validación final se mantendrá manual hasta contar con un mecanismo bancario autorizado y confiable.

## 6. Automatizaciones planeadas con n8n

- Detectar el correo oficial enviado por el banco después de un SINPE.
- Relacionar el correo con el pedido correspondiente.
- Avisar al administrador de pedidos nuevos.
- Alertar cuando un producto tenga pocas existencias.
- Enviar al cliente la confirmación de su pedido.
- Notificar cuando un pedido esté listo para retirar.
- Enviar un resumen diario de ventas.
- Recordar pedidos pendientes de pago.
- Generar tareas de seguimiento.
- Enviar facturas o comprobantes.

Las automatizaciones se estudiarán después de comprender PHP, MySQL, formularios, estados, seguridad y webhooks.

## 7. Ruta de aprendizaje

### Etapa 0 — Diagnóstico y entorno

- Diagnóstico de conocimientos.
- Preparación de herramientas.
- Funcionamiento general de una aplicación web.
- Introducción a Git y GitHub.

### Etapa 1 — Fundamentos frontend

- HTML semántico.
- Formularios.
- CSS y diseño adaptable.
- JavaScript básico.
- DOM y eventos.

### Etapa 2 — Fundamentos backend

- Sintaxis de PHP.
- Formularios con GET y POST.
- Validaciones.
- Sesiones.
- Organización de archivos.
- Manejo de errores.

### Etapa 3 — Base de datos

- Modelado relacional.
- SQL.
- Claves primarias y foráneas.
- Conexión con PDO.
- Consultas preparadas.
- CRUD.

### Etapa 4 — Tienda en línea

- Productos y categorías.
- Catálogo y búsqueda.
- Carrito.
- Clientes.
- Pedidos.
- Historial de compras.

### Etapa 5 — Operación híbrida

- Inventario compartido.
- Ventas físicas.
- Pedidos en línea.
- Envíos y retiros.
- Proveedores.
- Panel administrativo.
- Reportes.

### Etapa 6 — Firebase y seguridad

- Firebase Authentication.
- Verificación de identidad desde PHP.
- Roles y permisos.
- Protección de formularios.
- Validación del lado del servidor.
- Manejo seguro de configuración.

### Etapa 7 — n8n

- Conceptos de automatización.
- Eventos, condiciones y acciones.
- Webhooks.
- Correos bancarios.
- WhatsApp Business.
- Alertas, recordatorios y reportes.

### Etapa 8 — Node.js

- Fundamentos de Node.js.
- APIs REST.
- Comparación con PHP.
- Reconstrucción gradual de funciones del backend.

## 8. Metodología de estudio

Cada capítulo podrá incluir:

1. Objetivos de aprendizaje.
2. Explicación teórica paso a paso.
3. Ejemplos pequeños y comentados.
4. Documentación oficial y páginas confiables.
5. Videos de YouTube seleccionados según el tema.
6. Laboratorio guiado.
7. Ejercicio independiente.
8. Revisión del código realizado por Erick.
9. Preguntas de repaso.
10. Evaluación corta.
11. Aplicación progresiva al proyecto.

## 9. Acuerdo de trabajo

- Erick creará las carpetas y escribirá el código de la aplicación.
- El asistente no entregará directamente la solución de los ejercicios.
- Los ejemplos guía utilizarán problemas pequeños o diferentes al ejercicio principal.
- Primero se ofrecerán explicaciones, pistas, pseudocódigo y preguntas orientadoras.
- El código completo solo se proporcionará cuando Erick lo solicite expresamente.
- Los errores se explicarán indicando la causa y cómo investigarlos.
- Cada avance importante se registrará con Git.
- Ningún cambio será enviado al repositorio sin autorización.
- No se almacenarán contraseñas, tokens ni credenciales privadas en GitHub.
- La ortografía no afectará las evaluaciones técnicas.

## 10. Repositorios de referencia

- Proyecto del profesor: [brav88/BookingPHP](https://github.com/brav88/BookingPHP)
- Proyecto anterior de Erick: repositorio privado `ericklamorita/ChatEstudio`
- Proyecto actual: repositorio privado `ericklamorita/Proyecto-FullStack-PHP`

Los proyectos anteriores se utilizarán como material de análisis. El proyecto actual se desarrollará desde cero.

## 11. Progreso

- [x] Definir objetivos.
- [x] Crear el repositorio.
- [x] Conectar el repositorio para revisión.
- [x] Definir el alcance general.
- [x] Seleccionar Firebase y n8n.
- [ ] Realizar el diagnóstico inicial.
- [ ] Preparar el entorno local.
- [ ] Comenzar el primer capítulo.
