Aquí tienes 3 ejemplos prácticos utilizando **Rutas Nombradas** en Flutter. Cada ejemplo tiene una estructura de 3 pantallas y un enfoque distinto de navegación.

### Conceptos clave antes de empezar:
1.  **`initialRoute`**: Define cuál es la pantalla que se abre al iniciar la app (normalmente `/`).
2.  **`routes`**: Un "mapa" (diccionario) donde relacionas un nombre (String) con una pantalla (Widget).
3.  **`Navigator.pushNamed(context, '/nombre')`**: Para ir a una pantalla por su nombre.

---

### Ejemplo 1: Flujo Lineal (Paso a Paso)
Este ejemplo simula un proceso de registro o un tutorial donde vas de la pantalla 1 -> 2 -> 3 de forma secuencial.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => PantallaUno(),
    '/segunda': (context) => PantallaDos(),
    '/tercera': (context) => PantallaTres(),
  },
));

class PantallaUno extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Paso 1: Inicio")),
      body: Center(
        child: ElevatedButton(
          child: Text("Ir al Paso 2"),
          onPressed: () => Navigator.pushNamed(context, '/segunda'),
        ),
      ),
    );
  }
}

class PantallaDos extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Paso 2: Configuración")),
      body: Center(
        child: ElevatedButton(
          child: Text("Ir al Paso 3"),
          onPressed: () => Navigator.pushNamed(context, '/tercera'),
        ),
      ),
    );
  }
}

class PantallaTres extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Paso 3: Finalizar")),
      body: Center(
        child: ElevatedButton(
          child: Text("Volver al Inicio"),
          onPressed: () => Navigator.popUntil(context, ModalRoute.withName('/')),
        ),
      ),
    );
  }
}
```

---

### Ejemplo 2: Menú Principal (Hub Central)
En este caso, la pantalla de inicio funciona como un menú desde el cual puedes saltar a dos secciones diferentes (Perfil o Ajustes).

```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => MenuPrincipal(),
    '/perfil': (context) => PantallaPerfil(),
    '/ajustes': (context) => PantallaAjustes(),
  },
));

class MenuPrincipal extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Menú Principal")),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          ListTile(
            leading: Icon(Icons.person),
            title: Text("Ver Perfil"),
            onTap: () => Navigator.pushNamed(context, '/perfil'),
          ),
          ListTile(
            leading: Icon(Icons.settings),
            title: Text("Ir a Ajustes"),
            onTap: () => Navigator.pushNamed(context, '/ajustes'),
          ),
        ],
      ),
    );
  }
}

class PantallaPerfil extends StatelessWidget {
  @override
  Widget build(BuildContext context) => Scaffold(
    appBar: AppBar(title: Text("Mi Perfil")),
    body: Center(child: Text("Datos del usuario")),
  );
}

class PantallaAjustes extends StatelessWidget {
  @override
  Widget build(BuildContext context) => Scaffold(
    appBar: AppBar(title: Text("Configuración")),
    body: Center(child: Text("Opciones de la App")),
  );
}
```

---

### Ejemplo 3: Ciclo de Tienda (Navegación Circular)
Simula un flujo de compra: Catálogo -> Carrito -> Confirmación. Desde la confirmación, el usuario puede regresar directamente al catálogo.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
  initialRoute: '/catalogo',
  routes: {
    '/catalogo': (context) => PantallaCatalogo(),
    '/carrito': (context) => PantallaCarrito(),
    '/exito': (context) => PantallaExito(),
  },
));

class PantallaCatalogo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Tienda")),
      body: Center(
        child: ElevatedButton(
          child: Text("Añadir al carrito"),
          onPressed: () => Navigator.pushNamed(context, '/carrito'),
        ),
      ),
    );
  }
}

class PantallaCarrito extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Tu Carrito")),
      body: Center(
        child: ElevatedButton(
          style: ElevatedButton.styleFrom(backgroundColor: Colors.green),
          child: Text("Finalizar Compra"),
          onPressed: () => Navigator.pushNamed(context, '/exito'),
        ),
      ),
    );
  }
}

class PantallaExito extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Icon(Icons.check_circle, size: 100, color: Colors.green),
            Text("¡Compra realizada!"),
            SizedBox(height: 20),
            ElevatedButton(
              child: Text("Volver a la tienda"),
              onPressed: () => Navigator.pushNamedAndRemoveUntil(context, '/catalogo', (route) => false),
              // pushNamedAndRemoveUntil limpia el historial para que no pueda volver atrás al carrito
            ),
          ],
        ),
      ),
    );
  }
}
```

### Resumen de las diferencias:
1.  **Ejemplo 1 (Lineal):** Usa `Navigator.pushNamed` para avanzar y `Navigator.pop` (automático en el AppBar) para retroceder uno a uno.
2.  **Ejemplo 2 (Hub):** Muestra cómo una sola pantalla puede dirigir a múltiples rutas independientes.
3.  **Ejemplo 3 (Limpieza de pila):** Introduce `pushNamedAndRemoveUntil`, que es útil cuando quieres "resetear" la app (como después de un Logout o una compra) para que el usuario no pueda regresar a la pantalla anterior con el botón físico de atrás.
