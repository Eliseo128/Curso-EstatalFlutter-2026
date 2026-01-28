A nivel principiante en Flutter, **StatelessWidget + Row + Column** es la base para construir prácticamente cualquier interfaz.

A continuación tienes **3 ejemplos visualmente atractivos, funcionales y didácticos** que tus alumnos pueden ejecutar inmediatamente y entender cómo se organiza la UI en Flutter.

---

## 🧩 Ejemplo 1 — Tarjeta de Perfil (Column + Row)

**Objetivo didáctico:**
Aprender a combinar `Column` (vertical) y `Row` (horizontal) para estructurar información tipo tarjeta.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MiApp());
}

class MiApp extends StatelessWidget {
  const MiApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: PerfilScreen(),
    );
  }
}

class PerfilScreen extends StatelessWidget {
  const PerfilScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Perfil de Usuario')),
      body: Center(
        child: Container(
          padding: const EdgeInsets.all(16),
          margin: const EdgeInsets.all(20),
          decoration: BoxDecoration(
            color: Colors.blue.shade50,
            borderRadius: BorderRadius.circular(12),
          ),
          child: Row(
            children: [
              const CircleAvatar(
                radius: 40,
                backgroundImage: NetworkImage(
                  'https://i.pravatar.cc/150?img=3',
                ),
              ),
              const SizedBox(width: 20),
              Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: const [
                  Text('Eliseo Nava',
                      style:
                          TextStyle(fontSize: 20, fontWeight: FontWeight.bold)),
                  Text('Desarrollador Flutter'),
                  Text('eliseo@email.com'),
                ],
              )
            ],
          ),
        ),
      ),
    );
  }
}
```

### 🔎 ¿Qué se aprende aquí?

* `Row` organiza la imagen y la información **horizontalmente**.
* `Column` organiza los textos **verticalmente**.
* Uso de `Container`, `padding`, `margin` y `BoxDecoration`.

---

## 🧩 Ejemplo 2 — Menú de Opciones (Column con varias Rows)

**Objetivo didáctico:**
Simular un menú tipo aplicación real usando filas repetidas.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MiApp());
}

class MiApp extends StatelessWidget {
  const MiApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: MenuScreen(),
    );
  }
}

class MenuScreen extends StatelessWidget {
  const MenuScreen({super.key});

  Widget opcion(IconData icono, String texto) {
    return Container(
      margin: const EdgeInsets.symmetric(vertical: 10),
      padding: const EdgeInsets.all(12),
      decoration: BoxDecoration(
        color: Colors.grey.shade200,
        borderRadius: BorderRadius.circular(10),
      ),
      child: Row(
        children: [
          Icon(icono, size: 30),
          const SizedBox(width: 20),
          Text(texto, style: const TextStyle(fontSize: 18)),
        ],
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Menú Principal')),
      body: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          children: [
            opcion(Icons.person, 'Perfil'),
            opcion(Icons.shopping_cart, 'Carrito'),
            opcion(Icons.settings, 'Configuración'),
            opcion(Icons.logout, 'Cerrar sesión'),
          ],
        ),
      ),
    );
  }
}
```

### 🔎 ¿Qué se aprende aquí?

* Reutilización de código creando un **método que regresa un Widget**.
* `Column` contiene varias `Row`.
* Diseño tipo menú real de aplicación.

---

## 🧩 Ejemplo 3 — Tarjetas de Productos (Row dentro de Column)

**Objetivo didáctico:**
Simular productos tipo tienda usando diseño más visual.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MiApp());
}

class MiApp extends StatelessWidget {
  const MiApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: ProductosScreen(),
    );
  }
}

class ProductosScreen extends StatelessWidget {
  const ProductosScreen({super.key});

  Widget producto(String nombre, String precio, String imagen) {
    return Container(
      margin: const EdgeInsets.symmetric(vertical: 10),
      padding: const EdgeInsets.all(10),
      decoration: BoxDecoration(
        border: Border.all(),
        borderRadius: BorderRadius.circular(10),
      ),
      child: Row(
        children: [
          Image.network(imagen, width: 80),
          const SizedBox(width: 20),
          Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Text(nombre,
                  style: const TextStyle(
                      fontSize: 18, fontWeight: FontWeight.bold)),
              Text(precio, style: const TextStyle(fontSize: 16)),
            ],
          )
        ],
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Productos')),
      body: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          children: [
            producto('Laptop', '\$15,000',
                'https://picsum.photos/100?1'),
            producto('Celular', '\$8,000',
                'https://picsum.photos/100?2'),
            producto('Audífonos', '\$1,200',
                'https://picsum.photos/100?3'),
          ],
        ),
      ),
    );
  }
}
```

### 🔎 ¿Qué se aprende aquí?

* Diseño tipo **e-commerce**.
* Combinación real de `Row + Column`.
* Reutilización de widgets para generar múltiples tarjetas.

---

## 🧠 Concepto clave que deben comprender tus alumnos

> **Column = ordena vertical**
> **Row = ordena horizontal**

Y Flutter funciona como **bloques Lego**: un widget dentro de otro.

---

Si quieres, el siguiente paso ideal para tus alumnos es:
👉 **Convertir uno de estos ejemplos a StatefulWidget y agregar interacción (botones, contador, etc.)**.
