¡Excelente elección! Usar **StatelessWidget** es la mejor práctica en Flutter. Esto nos permite separar el diseño de la ejecución y hace que nuestro código sea más ordenado y profesional. 

Aquí tienes los ejemplos actualizados, cada uno con su estructura de clase completa.

---

### 1. Widgets Material Design: `Scaffold`, `AppBar` y `Body`
El `StatelessWidget` es una pieza de la interfaz que no cambia por sí sola. Es el molde perfecto para pantallas de información.

#### Ejemplo 1: Estructura de un Perfil
```dart
import 'package:flutter/material.dart';

void main() => runApp(const MaterialApp(home: PantallaPerfil()));

class PantallaPerfil extends StatelessWidget {
  const PantallaPerfil({super.key}); // Constructor de la clase

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Mi Perfil"),
        backgroundColor: Colors.indigo,
      ),
      body: const Center(
        child: Text("Nombre del Usuario: Rex_99"),
      ),
    );
  }
}
```
**Explicación:** 
1. `main` lanza `MaterialApp`, pero ahora le decimos que el inicio (`home`) es nuestra clase `PantallaPerfil`.
2. `Scaffold` organiza la pantalla. El `AppBar` es la parte superior y el `body` es el espacio principal.
3. El `const` se usa porque este diseño no cambiará mientras la app corre, lo que la hace más rápida.

#### Ejemplo 2: Pantalla de Bienvenida de una Tienda
```dart
import 'package:flutter/material.dart';

void main() => runApp(const MaterialApp(home: BienvenidaTienda()));

class BienvenidaTienda extends StatelessWidget {
  const BienvenidaTienda({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Tienda de Mascotas 🐾"),
        backgroundColor: Colors.teal,
      ),
      body: const Center(
        child: Text("¡Hola! ¿Qué mascota buscas hoy?"),
      ),
    );
  }
}
```
**Explicación:** Al usar una clase `StatelessWidget`, el código es más fácil de leer. Aquí cambiamos el color de la barra a `teal` (azul verdoso) para darle una personalidad diferente a la tienda.

---

### 2. Contenedores: `Container` (márgenes, bordes, colores)
El `Container` es el widget más versátil para dar forma y color a nuestras cajas.

#### Ejemplo 1: Caja de Notificación
```dart
import 'package:flutter/material.dart';

void main() => runApp(const MaterialApp(home: NotificacionView()));

class NotificacionView extends StatelessWidget {
  const NotificacionView({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Container(
          padding: const EdgeInsets.all(30.0), // Espacio interno
          color: Colors.amber,
          child: const Text("Tienes una tarea pendiente"),
        ),
      ),
    );
  }
}
```
**Explicación:** El `Container` envuelve al texto. `EdgeInsets.all(30.0)` crea un "colchón" de espacio alrededor del texto para que no toque los bordes amarillos de la caja.

#### Ejemplo 2: Tarjeta Decorada (Bordes Redondeados)
```dart
import 'package:flutter/material.dart';

void main() => runApp(const MaterialApp(home: TarjetaDecorada()));

class TarjetaDecorada extends StatelessWidget {
  const TarjetaDecorada({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Container(
          width: 250,
          height: 150,
          decoration: BoxDecoration(
            color: Colors.deepPurple,
            borderRadius: BorderRadius.circular(25), // Esquinas curvas
            border: Border.all(color: Colors.black, width: 2), // Borde
          ),
          child: const Center(
            child: Text("Tarjeta VIP", style: TextStyle(color: Colors.white)),
          ),
        ),
      ),
    );
  }
}
```
**Explicación:** Cuando queremos bordes redondeados, usamos `BoxDecoration`. **Dato importante:** Si usas `decoration`, el color debe ir *adentro* de la decoración, no fuera, o la app marcará error.

---

### 3. Texto y Estilos: `Text` y `TextStyle`
El estilo define la jerarquía visual: lo más importante debe ser más grande y llamativo.

#### Ejemplo 1: Título de Juego
```dart
import 'package:flutter/material.dart';

void main() => runApp(const MaterialApp(home: PantallaVictoria()));

class PantallaVictoria extends StatelessWidget {
  const PantallaVictoria({super.key});

  @override
  Widget build(BuildContext context) {
    return const Scaffold(
      body: Center(
        child: Text(
          "¡VICTORIA!",
          style: TextStyle(
            fontSize: 45,                // Muy grande
            fontWeight: FontWeight.w900, // Extra negrita
            color: Colors.orange,        // Color llamativo
            letterSpacing: 5.0,           // Espacio entre letras
          ),
        ),
      ),
    );
  }
}
```
**Explicación:** `FontWeight.w900` es la negrita más gruesa disponible. `letterSpacing` hace que la palabra se vea más imponente, ideal para un anuncio de victoria.

#### Ejemplo 2: Estilo de Subtítulo Elegante
```dart
import 'package:flutter/material.dart';

void main() => runApp(const MaterialApp(home: CreditosApp()));

class CreditosApp extends StatelessWidget {
  const CreditosApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const Scaffold(
      body: Center(
        child: Text(
          "Versión 1.0.2 - Creado por Programadores",
          style: TextStyle(
            fontSize: 16,
            fontStyle: FontStyle.italic, // Cursiva
            color: Colors.grey,          // Color discreto
          ),
        ),
      ),
    );
  }
}
```
**Explicación:** Usamos un tamaño de fuente pequeño (16) y un color gris para que el texto parezca información secundaria, demostrando cómo el estilo guía la mirada.

---

### 4. El Árbol de Widgets: Padres e Hijos (`child` vs `children`)
Aquí organizamos múltiples piezas de LEGO para formar algo más grande.

#### Ejemplo 1: Lista de Instrucciones (Columna)
```dart
import 'package:flutter/material.dart';

void main() => runApp(const MaterialApp(home: ListaInstrucciones()));

class ListaInstrucciones extends StatelessWidget {
  const ListaInstrucciones({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("Pasos a seguir")),
      body: const Column( // Column acepta muchos hijos
        children: [
          Text("1. Abre la cuenta"),
          Text("2. Ingresa tus datos"),
          Text("3. ¡Listo para usar!"),
        ],
      ),
    );
  }
}
```
**Explicación:** `Column` usa `children` porque puede tener una lista infinita de widgets uno debajo de otro.

#### Ejemplo 2: Mini Tarjeta de Resumen (El Árbol Completo)
```dart
import 'package:flutter/material.dart';

void main() => runApp(const MaterialApp(home: ResumenApp()));

class ResumenApp extends StatelessWidget {
  const ResumenApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center( // Padre 1
        child: Column( // Hijo de Center, Padre de los siguientes
          mainAxisAlignment: MainAxisAlignment.center, // Centra el contenido de la columna
          children: [
            const Icon(Icons.star, size: 50, color: Colors.blue), // Un icono
            const Text("Puntuación Final", style: TextStyle(fontSize: 24)),
            Container( // Un hijo que a su vez es padre de un texto
              color: Colors.blue[100],
              padding: const EdgeInsets.all(10),
              child: const Text("9.8 / 10", style: TextStyle(fontWeight: FontWeight.bold)),
            ),
          ],
        ),
      ),
    );
  }
}
```
**Explicación del Árbol:**
1.  **Scaffold** contiene a **Center**.
2.  **Center** tiene un único hijo (`child`): **Column**.
3.  **Column** tiene tres hijos (`children`): un **Icon**, un **Text** y un **Container**.
4.  **Container** tiene un único hijo (`child`): otro **Text**.
¡Este es el poder de los Widgets! Puedes anidarlos tanto como necesites para crear diseños complejos.
