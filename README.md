# Dedicatoria Especial para Mamá 💖

Página web interactiva para crear una dedicatoria personalizada en el Día de las Madres. El usuario ingresa su nombre y el de su mamá, y la página genera un mensaje emotivo con una animación de fondo de corazones flotantes.

---

## Estructura del código

### 1. Documento HTML (`Dia de las madres.html`)

El archivo está compuesto por tres secciones principales: **`<head>`** (metadatos y estilos), **`<body>`** (contenido visible) y **`<script>`** (lógica interactiva).

---

### 2. `<head>` — Configuración y estilos CSS

#### Metadatos
- `charset="UTF-8"` — permite usar caracteres especiales como tildes y ñ.
- `viewport` — hace que la página se adapte correctamente a dispositivos móviles.
- `<title>` — título que aparece en la pestaña del navegador.

#### Estilos CSS destacados

| Selector | Descripción |
|---|---|
| `html, body` | Fondo degradado rosa claro (`#fff5f5` → `#f8e8e8`), sin márgenes, altura total, desbordamiento oculto. |
| `canvas` | Posicionado detrás de todo el contenido (`z-index: -1`) para servir como fondo animado. |
| `.container` | Tarjeta central con bordes redondeados, sombra suave y animación `fadeIn` al cargar. |
| `.heart` | Emoji de corazón con animación `pulse` que lo hace latir (escala del 100% al 115%). |
| `input[type="text"]` | Campos de texto con borde rosa y efecto de brillo al enfocarse. |
| `button` | Botón degradado rosa con efecto de elevación al pasar el cursor (`translateY(-2px)`). |
| `.message` | Caja del mensaje, inicialmente invisible (`opacity: 0`). Al recibir la clase `.show`, aparece con transición suave. |
| `.signature` | Firma del mensaje en cursiva, alineada a la derecha, en color fucsia. |

#### Animaciones CSS
- **`pulse`** — El corazón del encabezado escala entre 1× y 1.15× de forma continua (2 segundos).
- **`fadeIn`** — El contenedor aparece desde ligeramente reducido y transparente al cargar la página.
- **`floating`** — El corazón del encabezado sube y baja suavemente 10px cada 3 segundos.

#### Diseño responsive
Con `@media (max-width: 768px)` se ajustan márgenes, tamaño del título y del texto del mensaje para pantallas pequeñas.

---

### 3. `<body>` — Contenido visible

```
<canvas id="bg">          → Lienzo para la animación de fondo
<div class="container">   → Tarjeta principal centrada
  <div class="header">    → Corazón flotante + título + subtítulo
  <div class="input-group"> → Dos campos de texto (nombre propio y nombre de mamá)
  <button>                → Botón que dispara la función mostrarMensaje()
  <div id="mensaje">      → Área donde aparece la dedicatoria generada
```

---

### 4. `<script>` — Lógica JavaScript

#### Función `mostrarMensaje()`
1. Lee los valores de los campos `#nombre` (nombre del hijo/a) y `#mama` (nombre de la mamá).
2. Si alguno está vacío, muestra una alerta y limpia el mensaje anterior.
3. Si ambos están completos, selecciona **aleatoriamente** uno de **3 mensajes predefinidos** que incluyen el nombre de la mamá interpolado dentro del texto.
4. Añade una firma personalizada con el nombre del hijo/a al final.
5. Muestra el mensaje con la clase CSS `.show` (que activa la transición de opacidad).
6. Hace scroll suave hasta el mensaje con `scrollIntoView({ behavior: 'smooth' })`.

#### Animación de fondo con Canvas API

Se crea una clase `Particle` que representa un corazón flotante con las siguientes propiedades:

| Propiedad | Descripción |
|---|---|
| `x`, `y` | Posición inicial aleatoria en el canvas. |
| `size` | Tamaño aleatorio entre 10px y 30px. |
| `speedX`, `speedY` | Velocidad de movimiento suave (±0.25 px/frame). |
| `opacity` | Transparencia aleatoria entre 0.1 y 0.5. |
| `rotation` / `rotationSpeed` | Ángulo y velocidad de rotación aleatoria. |

- **`update()`** — Mueve la partícula cada frame y la hace reaparecer en el lado opuesto cuando sale del canvas (efecto de bucle infinito).
- **`draw()`** — Dibuja el emoji ❤️ en el canvas usando `ctx.fillText`, rotado y con la opacidad correspondiente.
- **`init()`** — Crea 30 partículas iniciales.
- **`animate()`** — Limpia el canvas cada frame y redibuja todas las partículas usando `requestAnimationFrame` para un loop fluido.

El canvas se redimensiona automáticamente cuando el usuario cambia el tamaño de la ventana (`resize` event listener).

---

## Tecnologías utilizadas

- **HTML5** — estructura semántica de la página.
- **CSS3** — animaciones (`@keyframes`), diseño responsivo (`@media`), transiciones y degradados.
- **JavaScript (Vanilla)** — manipulación del DOM, generación aleatoria de mensajes y animación con Canvas 2D API.

---

## Cómo usar

1. Abrir el archivo `Dia de las madres.html` en cualquier navegador moderno.
2. Escribir tu nombre en el primer campo.
3. Escribir el nombre de tu mamá en el segundo campo.
4. Hacer clic en **"Crear mi dedicatoria"** para generar el mensaje personalizado.