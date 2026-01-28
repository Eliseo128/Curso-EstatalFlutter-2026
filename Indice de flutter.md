¡Perfecto! Una vez que tienen la base de Dart (del temario anterior), el paso natural es **Flutter**.

Para estudiantes de preparatoria, la clave de Flutter es la **gratificación visual inmediata**. A diferencia de la consola de comandos de Dart, aquí verán colores, botones y animaciones en su celular.

Este temario está diseñado bajo la filosofía de *"Aprender construyendo"* (Project-Based Learning).

---

# 📱 Curso: Desarrollo de Apps Móviles con Flutter

**Nivel:** Principiante a Intermedio
**Requisito:** Conocimientos básicos de Dart (Variables, Funciones, Clases).

### 🚀 Módulo 0: El entorno y la "Magia"

*Objetivo: Que vean su primera app corriendo en su celular o emulador en menos de 1 hora.*

1. **¿Qué es Flutter?** El concepto de "Escribe una vez, ejecuta en todos lados" (iOS, Android, Web).
2. **Arquitectura:** ¿Cómo pinta Flutter los píxeles? (Skia).
3. **La Estructura de Carpetas:** Entendiendo `lib`, `pubspec.yaml` y `android/ios`.
4. **Hot Reload & Hot Restart:** Por qué Flutter es tan rápido para desarrollar.
5. **Hola Mundo Visual:** Modificar el código base para cambiar colores y textos.

### 🧱 Módulo 1: Todo es un Widget (UI Básica)

*Objetivo: Entender la metáfora de los "Bloques de Lego".*

1. **Widgets Material Design:** `Scaffold`, `AppBar`, `Body`.
2. **Contenedores:** El uso de `Container` (márgenes, bordes, colores).
3. **Texto y Estilos:** `Text`, `TextStyle` (fuentes, tamaños, negritas).
4. **El Árbol de Widgets:** Padres e hijos (`child` vs `children`).

### 📐 Módulo 2: Layouts (Diseño y Distribución)

*Objetivo: Aprender a acomodar elementos en la pantalla sin que "se rompa".*

1. **Filas y Columnas:** `Row` y `Column` (Eje principal vs transversal).
2. **Alineación:** `MainAxisAlignment` y `CrossAxisAlignment`.
3. **Espaciado:** `SizedBox` (espacio vacío) y `Padding`.
4. **Diseño Responsivo Básico:** `Expanded` y `Flexible` (para evitar el error de "overflow" de franjas amarillas y negras).
5. **Stack:** Poner elementos uno encima de otro (ej. texto sobre imagen).

### 🎨 Módulo 3: Assets e Imágenes

*Objetivo: Hacer que la app se vea profesional.*

1. **Imágenes:**
* Desde Internet: `Image.network`.
* Locales: Configuración en `pubspec.yaml` y uso de `Image.asset`.


2. **Iconos:** Uso de la librería `Icons`.
3. **Fuentes Personalizadas:** Importar Google Fonts.
4. **Botones:** `ElevatedButton`, `TextButton`, `IconButton` y cómo estilizarlos.

### ⚡ Módulo 4: State Management Básico (Interactivity)

*Objetivo: Que la app "haga cosas" cuando el usuario toca la pantalla.*

1. **Stateless vs Stateful:** La diferencia entre una foto (estático) y un video (dinámico).
2. **SetState:** El comando mágico para repintar la pantalla.
3. **Inputs:** `TextField` para recibir texto del usuario.
4. **Controladores:** `TextEditingController` para leer lo que escribe el usuario.
5. **Proyecto Práctico:** "Contador de Clics" o "Calculadora de Propinas".

### 🗺️ Módulo 5: Navegación y Rutas

*Objetivo: Pasar de una pantalla a otra.*

1. **Navegación Básica:** `Navigator.push` y `Navigator.pop`.
2. **Rutas Nombradas:** Organizar las pantallas en un "mapa".
3. **Pasar Argumentos:** Enviar datos de la Pantalla A a la Pantalla B.
4. **Drawer y Menús:** Crear un menú lateral desplegable.

### 📜 Módulo 6: Listas y Grids (Colecciones Visuales)

*Objetivo: Mostrar mucha información de forma eficiente (como Instagram o WhatsApp).*

1. **ListView:** Listas con scroll.
2. **ListTile:** El widget estándar para elementos de lista (título, subtítulo, icono).
3. **ListView.builder:** Renderizar listas infinitas o muy largas de manera optimizada.
4. **GridView:** Galerías de imágenes o catálogos.

### 📦 Módulo 7: Pub.dev y Librerías (Nivel Intermedio)

*Objetivo: No reinventar la rueda, usar código de la comunidad.*

1. **Pub.dev:** Cómo buscar e instalar paquetes.
2. **Paquetes Populares:**
* `google_fonts` (Tipografía).
* `font_awesome_flutter` (Iconos extra).
* `toast` o `snackbar` (Mensajes emergentes).
* `url_launcher` (Abrir navegador web o llamar por teléfono).



---

### 🌐 Módulo 8: Conexión a Internet (API REST)

*Objetivo: Conectar la app con el mundo real (datos en vivo).*

1. **Concepto de JSON:** Repaso rápido.
2. **Paquete HTTP:** Realizar peticiones `GET`.
3. **FutureBuilder:** El widget perfecto para esperar datos de internet (Cargando -> Error -> Datos).
4. **Modelos:** Convertir JSON a Objetos Dart (Factory constructors).
5. **Proyecto:** App de Clima, App de Noticias o Pokedex.

### 🧠 Módulo 9: Introducción a Gestores de Estado (Provider)

*Objetivo: Solucionar el "Spaghetti code" de usar mucho `setState`.*

1. **El problema de pasar datos:** "Prop Drilling" (pasar datos de abuelo a nieto).
2. **Provider:** Concepto de "Single Source of Truth" (Una sola fuente de verdad).
3. **ChangeNotifier:** Notificar a múltiples widgets que algo cambió.
4. **Consumer:** Escuchar cambios y redibujar solo lo necesario.

---

### 🎓 Proyecto Final del Curso

Los estudiantes deben elegir una de estas opciones para desarrollar en las últimas 2 semanas:

1. **Clon de Red Social (Simplificado):** Feed de fotos (usando una API pública como Lorem Picsum) y perfil de usuario.
2. **App de Tareas (To-Do) Avanzada:** Con categorías, colores y recordatorios visuales.
3. **App de Películas:** Consultando la API de *The Movie Database* (TMDB) para ver pósters, títulos y descripciones.

---

### 💡 Sugerencias Pedagógicas para este nivel

* **Evita el emulador lento:** Si es posible, enséñales a conectar **su propio celular Android** por USB. Ver la app en su mano aumenta la motivación un 200%. Si tienen iPhone y usan Windows, usen Chrome (Flutter Web) para depurar.
* **Diseño > Lógica (al principio):** A los chicos de preparatoria les importa mucho la estética. Dedica tiempo a `BoxDecoration`, bordes redondeados, sombras (`BoxShadow`) y gradientes.
* **Snippets:** Enséñales a usar atajos de teclado en VS Code (ej. `stless` crea un widget rápido, `Ctrl + .` para envolver widgets).

¿Te gustaría que desarrolle **el detalle del Módulo 4 (Interactivity)** con ejemplos de código, ya que suele ser el primer "muro" de dificultad para los alumnos?
