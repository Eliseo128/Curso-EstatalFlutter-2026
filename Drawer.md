Aquí tienes 2 ejemplos de navegación con **Drawer** (menú lateral). El Drawer es ideal para aplicaciones que necesitan un acceso rápido a diferentes secciones sin saturar la pantalla principal.

---

### Ejemplo 1: Estilo Red Social (Uso de `UserAccountsDrawerHeader`)
Este es el método más fácil en Flutter para crear un encabezado con avatar y nombre/email.

```dart
import 'package:flutter/material.dart';

void main() => runApp(AppSocial());

class AppSocial extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(primarySwatch: Colors.indigo),
      // DEFINICIÓN DE RUTAS
      initialRoute: '/',
      routes: {
        '/': (context) => PantallaInicio(),
        '/perfil': (context) => PantallaPerfil(),
      },
    );
  }
}

// --- WIDGET PERSONALIZADO PARA EL DRAWER (Para no repetir código) ---
class MiDrawer extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        padding: EdgeInsets.zero,
        children: [
          // ENCABEZADO CON AVATAR Y DESCRIPCIÓN
          UserAccountsDrawerHeader(
            accountName: Text("Juan Pérez"),
            accountEmail: Text("juan.perez@email.com"),
            currentAccountPicture: CircleAvatar(
              backgroundImage: NetworkImage("https://www.w3schools.com/howto/img_avatar.png"),
            ),
          ),
          // OPCIÓN 1
          ListTile(
            leading: Icon(Icons.home),
            title: Text("Inicio"),
            onTap: () => Navigator.pushNamed(context, '/'),
          ),
          // OPCIÓN 2
          ListTile(
            leading: Icon(Icons.person),
            title: Text("Mi Perfil"),
            onTap: () => Navigator.pushNamed(context, '/perfil'),
          ),
        ],
      ),
    );
  }
}

// --- PANTALLAS ---
class PantallaInicio extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Inicio")),
      drawer: MiDrawer(), // Agregamos el Drawer aquí
      body: Center(child: Text("Bienvenido a la App Social")),
    );
  }
}

class PantallaPerfil extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Perfil")),
      drawer: MiDrawer(), // Agregamos el Drawer aquí también
      body: Center(child: Text("Información del Usuario")),
    );
  }
}
```

---

### Ejemplo 2: Estilo Administrativo (Drawer Personalizado)
En este ejemplo, creamos el encabezado manualmente usando un `DrawerHeader` común para tener más control sobre el diseño.

```dart
import 'package:flutter/material.dart';

void main() => runApp(AppAdmin());

class AppAdmin extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(primarySwatch: Colors.teal),
      initialRoute: '/',
      routes: {
        '/': (context) => PantallaDashboard(),
        '/config': (context) => PantallaConfiguracion(),
      },
    );
  }
}

class MenuLateral extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: Column(
        children: [
          // ENCABEZADO MANUAL
          DrawerHeader(
            decoration: BoxDecoration(color: Colors.teal),
            child: Row(
              children: [
                CircleAvatar(
                  radius: 30,
                  backgroundColor: Colors.white,
                  child: Icon(Icons.admin_panel_settings, size: 40, color: Colors.teal),
                ),
                SizedBox(width: 20),
                Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text("Admin Mode", style: TextStyle(color: Colors.white, fontSize: 18, fontWeight: FontWeight.bold)),
                    Text("Online", style: TextStyle(color: Colors.white70)),
                  ],
                )
              ],
            ),
          ),
          // OPCIONES
          ListTile(
            leading: Icon(Icons.dashboard),
            title: Text("Dashboard"),
            onTap: () => Navigator.pushNamed(context, '/'),
          ),
          ListTile(
            leading: Icon(Icons.settings),
            title: Text("Configuración"),
            onTap: () => Navigator.pushNamed(context, '/config'),
          ),
        ],
      ),
    );
  }
}

class PantallaDashboard extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Panel de Control")),
      drawer: MenuLateral(),
      body: Center(child: Icon(Icons.analytics, size: 100, color: Colors.teal[100])),
    );
  }
}

class PantallaConfiguracion extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Ajustes del Sistema")),
      drawer: MenuLateral(),
      body: Center(child: Text("Aquí puedes cambiar los ajustes")),
    );
  }
}
```

### Conceptos clave de estos ejemplos:

1.  **`drawer:`**: Es una propiedad del `Scaffold`. Si la incluyes, Flutter añade automáticamente el icono de las "tres rayitas" (hamburguesa) en el `AppBar`.
2.  **`UserAccountsDrawerHeader`**: Es un widget pre-diseñado muy útil para mostrar la información del usuario logueado.
3.  **`ListTile`**: Es el widget estándar para las filas del menú, ya que permite poner un icono al principio (`leading`) y manejar el toque (`onTap`).
4.  **`Navigator.pushNamed`**: Al usar rutas nombradas, el Drawer sabe exactamente a qué ventana enviarte.
5.  **Reutilización**: He creado clases separadas para el Drawer (`MiDrawer` y `MenuLateral`) para que puedas llamarlas en todas tus pantallas sin escribir el mismo código varias veces.
