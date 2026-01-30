Aquí tienes los 3 ejemplos actualizados. En cada uno verás cómo configurar el **`ThemeData`** (colores y estilos globales) dentro del widget de inicio y la estructura de 3 pantallas utilizando rutas nombradas.

---

### Ejemplo 1: Flujo de Registro (Tema Azul)
Este ejemplo utiliza un color primario azul y un flujo secuencial: **Bienvenida -> Datos -> Finalizar**.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MiAppRegistro());

class MiAppRegistro extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Registro App',
      // CONFIGURACIÓN DE TEMA
      theme: ThemeData(
        primarySwatch: Colors.blue,
        elevatedButtonTheme: ElevatedButtonThemeData(
          style: ElevatedButton.styleFrom(backgroundColor: Colors.blueAccent),
        ),
      ),
      // RUTAS NOMBRADAS
      initialRoute: '/',
      routes: {
        '/': (context) => PantallaBienvenida(),
        '/datos': (context) => PantallaDatos(),
        '/final': (context) => PantallaFinal(),
      },
    );
  }
}

class PantallaBienvenida extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Paso 1: Bienvenida")),
      body: Center(
        child: ElevatedButton(
          onPressed: () => Navigator.pushNamed(context, '/datos'),
          child: Text("Empezar Registro"),
        ),
      ),
    );
  }
}

class PantallaDatos extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Paso 2: Tus Datos")),
      body: Center(
        child: ElevatedButton(
          onPressed: () => Navigator.pushNamed(context, '/final'),
          child: Text("Guardar y Continuar"),
        ),
      ),
    );
  }
}

class PantallaFinal extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Paso 3: ¡Listo!")),
      body: Center(
        child: OutlinedButton(
          onPressed: () => Navigator.popUntil(context, ModalRoute.withName('/')),
          child: Text("Volver al Inicio"),
        ),
      ),
    );
  }
}
```

---

### Ejemplo 2: App de Perfil (Tema Verde)
Este ejemplo usa un tema verde y un esquema de **Menú -> Perfil / Configuración**.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MiAppPerfil());

class MiAppPerfil extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.green,
        scaffoldBackgroundColor: Colors.green[50], // Fondo suave
      ),
      initialRoute: '/',
      routes: {
        '/': (context) => PantallaPrincipal(),
        '/perfil': (context) => PantallaDetallePerfil(),
        '/ajustes': (context) => PantallaAjustes(),
      },
    );
  }
}

class PantallaPrincipal extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Mi App")),
      body: ListView(
        children: [
          ListTile(
            leading: Icon(Icons.person, color: Colors.green),
            title: Text("Ver mi Perfil"),
            onTap: () => Navigator.pushNamed(context, '/perfil'),
          ),
          ListTile(
            leading: Icon(Icons.settings, color: Colors.green),
            title: Text("Configuración"),
            onTap: () => Navigator.pushNamed(context, '/ajustes'),
          ),
        ],
      ),
    );
  }
}

class PantallaDetallePerfil extends StatelessWidget {
  @override
  Widget build(BuildContext context) => Scaffold(
    appBar: AppBar(title: Text("Perfil")),
    body: Center(child: Text("👤 Información del Usuario")),
  );
}

class PantallaAjustes extends StatelessWidget {
  @override
  Widget build(BuildContext context) => Scaffold(
    appBar: AppBar(title: Text("Ajustes")),
    body: Center(child: Text("⚙️ Opciones del sistema")),
  );
}
```

---

### Ejemplo 3: Tienda Virtual (Tema Naranja/DeepOrange)
Simula un flujo de compra: **Tienda -> Carrito -> Confirmación**, con un estilo visual cálido.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MiAppTienda());

class MiAppTienda extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.deepOrange,
        useMaterial3: true, // Estilo moderno de Flutter
      ),
      initialRoute: '/tienda',
      routes: {
        '/tienda': (context) => PantallaTienda(),
        '/carrito': (context) => PantallaCarrito(),
        '/confirmacion': (context) => PantallaConfirmacion(),
      },
    );
  }
}

class PantallaTienda extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Naranja Store")),
      body: Center(
        child: IconButton(
          icon: Icon(Icons.add_shopping_cart, size: 50, color: Colors.deepOrange),
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
        child: ElevatedButton.icon(
          icon: Icon(Icons.payment),
          label: Text("Pagar Ahora"),
          onPressed: () => Navigator.pushNamed(context, '/confirmacion'),
        ),
      ),
    );
  }
}

class PantallaConfirmacion extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.deepOrange[100],
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Icon(Icons.check_circle_outline, size: 100, color: Colors.deepOrange),
            Text("¡Gracias por tu compra!", style: TextStyle(fontSize: 20)),
            SizedBox(height: 30),
            TextButton(
              onPressed: () => Navigator.pushNamedAndRemoveUntil(context, '/tienda', (r) => false),
              child: Text("Volver a comprar"),
            ),
          ],
        ),
      ),
    );
  }
}
```

### ¿Qué aprendemos de estos ejemplos?
1.  **`primarySwatch`**: Es un conjunto de colores basado en un color principal. Al cambiarlo, Flutter ajusta automáticamente el AppBar, los botones y otros widgets.
2.  **`Navigator.pushNamed`**: Se usa para avanzar.
3.  **`Navigator.popUntil` o `pushNamedAndRemoveUntil`**: Son útiles en la tercera pantalla para limpiar el historial y evitar que el usuario regrese a pantallas intermedias (como el carrito de compra ya pagado).
4.  **`debugShowCheckedModeBanner: false`**: Se añade para quitar la etiqueta roja de "Debug" en la esquina superior derecha.
