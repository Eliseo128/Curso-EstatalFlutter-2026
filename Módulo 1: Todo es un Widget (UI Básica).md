¡Bienvenidos al fascinante mundo de **Flutter**! En este módulo dejamos atrás la consola negra y fría para empezar a construir interfaces que puedes ver y tocar.

La regla de oro en Flutter es: **"Todo es un Widget"**. Imagina que los Widgets son piezas de **LEGO**. Una pieza puede ser un botón, otra un color de fondo, y otra el texto. Al unirlas, formas una aplicación.

---

### 1. Widgets Material Design: `Scaffold`, `AppBar` y `Body`
Estos son los bloques de construcción básicos para que una app se vea "profesional" y con el estilo de Google (Material Design).
*   **Scaffold:** Es el "lienzo" o la estructura de la página (el esqueleto).
*   **AppBar:** La barra superior donde suele ir el título.
*   **Body:** Todo el contenido que va debajo de la barra.

#### Ejemplo 1: Estructura de una Red Social
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: const Text("Mi Perfil"),
        backgroundColor: Colors.blue, // Color de la barra
      ),
      body: const Center(
        child: Text("¡Bienvenido a tu muro!"),
      ),
    ),
  ));
}
```
**Explicación:** 
1. `runApp` inicia la app.
2. `MaterialApp` le dice a Flutter que use el diseño de Android/Google.
3. `Scaffold` organiza la pantalla: le pusimos un `AppBar` azul con un título y un `body` que tiene un texto centrado.

#### Ejemplo 2: Tienda de Mascotas
```dart
import 'package:flutter/material.dart';

void main() => runApp(const MiTienda());

class MiTienda extends StatelessWidget {
  const MiTienda({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: const Text("Adopta un amigo 🐶"),
          backgroundColor: Colors.orange,
        ),
        body: const Center(
          child: Text("Lista de perritos disponibles"),
        ),
      ),
    );
  }
}
```
**Explicación:** Aquí usamos una **Clase (StatelessWidget)** para organizar mejor el código. El `Scaffold` ahora tiene un color naranja amigable. El `Center` es un widget que ayuda a que su hijo (`child`) no se quede pegado a las esquinas.

---

### 2. Contenedores: `Container` (márgenes, bordes, colores)
El `Container` es como una caja mágica. Sirve para envolver otros widgets y darles tamaño, color de fondo, bordes o separarlos de otros.

#### Ejemplo 1: Una tarjeta de aviso
```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
  home: Scaffold(
    body: Center(
      child: Container(
        color: Colors.yellow, // Color de fondo
        padding: const EdgeInsets.all(20), // Espacio interno (relleno)
        child: const Text("¡Atención: Aviso importante!"),
      ),
    ),
  ),
));
```
**Explicación:** El `padding` es muy importante; es el espacio que hay entre el texto y el borde de la caja amarilla. Sin padding, el texto se vería muy apretado.

#### Ejemplo 2: Caja con bordes redondeados
```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
  home: Scaffold(
    body: Center(
      child: Container(
        width: 200,
        height: 100,
        decoration: BoxDecoration(
          color: Colors.purple,
          borderRadius: BorderRadius.circular(20), // Bordes curvos
          border: Border.all(color: Colors.black, width: 3), // Borde negro
        ),
        child: const Center(
          child: Text("Caja con Estilo", style: TextStyle(color: Colors.white)),
        ),
      ),
    ),
  ),
));
```
**Explicación:** Cuando usamos `decoration`, el color debe ir dentro de ella. `BorderRadius` hace que las esquinas no sean picudas, dándole un toque moderno a la app.

---

### 3. Texto y Estilos: `Text` y `TextStyle`
El widget `Text` muestra palabras, pero `TextStyle` es el "maquillaje" que le aplicamos para cambiar su apariencia.

#### Ejemplo 1: Título llamativo
```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
  home: Scaffold(
    body: Center(
      child: Text(
        "¡Nivel 1 Completado!",
        style: TextStyle(
          fontSize: 30,             // Tamaño de letra
          fontWeight: FontWeight.bold, // Negrita
          color: Colors.green,       // Color verde
        ),
      ),
    ),
  ),
));
```
**Explicación:** `fontSize` usa números grandes para títulos (30+) y pequeños para párrafos (14-16). `FontWeight.bold` hace que resalte más.

#### Ejemplo 2: Texto con subtítulo y estilo itálico
```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
  home: Scaffold(
    body: Center(
      child: Text(
        "Diseñado por: Estudiante de Prepa",
        style: TextStyle(
          fontSize: 18,
          fontStyle: FontStyle.italic, // Letra cursiva
          letterSpacing: 2.0,           // Espacio entre letras
          backgroundColor: Colors.black12,
        ),
      ),
    ),
  ),
));
```
**Explicación:** `letterSpacing` separa un poco las letras para que se vea más elegante, y `fontStyle.italic` inclina el texto.

---

### 4. El Árbol de Widgets: Padres e Hijos (`child` vs `children`)
Aquí es donde aprendemos a meter piezas dentro de otras.
*   **child:** Se usa cuando el widget solo puede tener **un** hijo (ej. `Center`, `Container`).
*   **children:** Se usa cuando el widget puede tener una **lista** de hijos (ej. `Column`, `Row`).

#### Ejemplo 1: Una columna de textos (Vertical)
```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
  home: Scaffold(
    body: Column( // Este widget permite muchos hijos
      children: [
        Text("Primer paso"),
        Text("Segundo paso"),
        Text("Tercer paso"),
      ],
    ),
  ),
));
```
**Explicación:** La `Column` organiza los elementos uno debajo del otro. Nota que usamos corchetes `[]` porque es una lista de widgets.

#### Ejemplo 2: Combinando todo (El árbol complejo)
```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
  home: Scaffold(
    appBar: AppBar(title: Text("Mi App")),
    body: Center( // Padre 1 (Un solo hijo)
      child: Column( // Hijo de Center (Muchos hijos)
        mainAxisAlignment: MainAxisAlignment.center, // Centra verticalmente
        children: [
          Icon(Icons.star, color: Colors.amber), // Una pieza nueva: Icono
          Text("Calificación"),
          Container(
            color: Colors.blue,
            child: Text("5 Estrellas", style: TextStyle(color: Colors.white)),
          ),
        ],
      ),
    ),
  ),
));
```
**Explicación del Árbol:**
1. **Scaffold** es el padre de todos.
2. Su hijo es **Center**.
3. El hijo de Center es una **Column**.
4. La Column tiene 3 hijos: un **Icon**, un **Text** y un **Container**.
5. El Container tiene su propio hijo: otro **Text**.

¡Así es como se construye cualquier app en el mundo real! Es una jerarquía de padres e hijos.
