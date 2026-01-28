# Widget AppBar en Flutter - Guía Completa

## 📚 Propiedades Básicas del AppBar

### **Propiedades Principales:**

### 1. **`title`** (Widget - requerido)
```dart
title: Text('Mi Aplicación')
```
**Explicación:** Es el widget principal que se muestra en el centro de la AppBar. Normalmente es un Text, pero puede ser cualquier widget.

### 2. **`backgroundColor`** (Color)
```dart
backgroundColor: Colors.blue,
```
**Explicación:** Define el color de fondo de la AppBar. Usa `Colors` de la biblioteca `material.dart`.

### 3. **`elevation`** (double)
```dart
elevation: 4.0,
```
**Explicación:** Controla la sombra bajo la AppBar (efecto de elevación). Mayor valor = sombra más pronunciada.

### 4. **`actions`** (List<Widget>)
```dart
actions: [
  IconButton(icon: Icon(Icons.search), onPressed: () {}),
  IconButton(icon: Icon(Icons.more_vert), onPressed: () {}),
]
```
**Explicación:** Widgets que aparecen en el lado derecho de la AppBar (normalmente IconButtons).

### 5. **`leading`** (Widget)
```dart
leading: IconButton(
  icon: Icon(Icons.menu),
  onPressed: () {},
)
```
**Explicación:** Widget que aparece en el lado izquierdo. En Android suele ser el botón de navegación.

### 6. **`centerTitle`** (bool)
```dart
centerTitle: true,
```
**Explicación:** Controla si el título está centrado (true) o alineado a la izquierda (false).

### 7. **`toolbarHeight`** (double)
```dart
toolbarHeight: 80.0,
```
**Explicación:** Define la altura de la AppBar en píxeles lógicos.

### 8. **`shadowColor`** (Color)
```dart
shadowColor: Colors.black.withOpacity(0.5),
```
**Explicación:** Color de la sombra cuando tiene elevation.

### 9. **`shape`** (ShapeBorder)
```dart
shape: RoundedRectangleBorder(
  borderRadius: BorderRadius.vertical(
    bottom: Radius.circular(20),
  ),
)
```
**Explicación:** Define la forma de la AppBar (bordes redondeados, etc.).

### 10. **`flexibleSpace`** (Widget)
```dart
flexibleSpace: Container(
  decoration: BoxDecoration(
    gradient: LinearGradient(
      colors: [Colors.blue, Colors.purple],
    ),
  ),
)
```
**Explicación:** Widget que se expande detrás de la toolbar y el bottom.

### 11. **`bottom`** (PreferredSizeWidget)
```dart
bottom: TabBar(
  tabs: [
    Tab(text: 'Tab 1'),
    Tab(text: 'Tab 2'),
  ],
)
```
**Explicación:** Widget que aparece debajo de la toolbar (TabBar, SearchBar, etc.).

---

## 📱 Código Base main.dart

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Ejemplos AppBar',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        useMaterial3: true, // Habilitar Material 3
      ),
      home: const HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        // Propiedades básicas aquí
        title: const Text('Ejemplo Básico'),
        backgroundColor: Colors.blue,
        elevation: 4.0,
      ),
      body: const Center(
        child: Text('Contenido de la página'),
      ),
    );
  }
}
```

---

## 🎯 3 Ejemplos Prácticos de AppBar

### **Ejemplo 1: AppBar con Actions y Menú Desplegable**

```dart
import 'package:flutter/material.dart';

void main() => runApp(const AppBarExample1());

class AppBarExample1 extends StatelessWidget {
  const AppBarExample1({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Red Social'),
          backgroundColor: Colors.deepPurple,
          centerTitle: true,
          elevation: 8.0,
          shadowColor: Colors.purple.withOpacity(0.3),
          
          // Icono izquierdo personalizado
          leading: IconButton(
            icon: const Icon(Icons.person),
            onPressed: () {
              ScaffoldMessenger.of(context).showSnackBar(
                const SnackBar(content: Text('Perfil de usuario')),
              );
            },
          ),
          
          // Acciones en el lado derecho
          actions: [
            // Notificaciones con badge
            Stack(
              children: [
                IconButton(
                  icon: const Icon(Icons.notifications),
                  onPressed: () {
                    ScaffoldMessenger.of(context).showSnackBar(
                      const SnackBar(content: Text('Notificaciones')),
                    );
                  },
                ),
                Positioned(
                  right: 8,
                  top: 8,
                  child: Container(
                    padding: const EdgeInsets.all(2),
                    decoration: BoxDecoration(
                      color: Colors.red,
                      borderRadius: BorderRadius.circular(10),
                    ),
                    constraints: const BoxConstraints(
                      minWidth: 16,
                      minHeight: 16,
                    ),
                    child: const Text(
                      '3',
                      style: TextStyle(
                        color: Colors.white,
                        fontSize: 10,
                      ),
                      textAlign: TextAlign.center,
                    ),
                  ),
                ),
              ],
            ),
            
            // Menú desplegable
            PopupMenuButton<String>(
              icon: const Icon(Icons.more_vert),
              onSelected: (value) {
                ScaffoldMessenger.of(context).showSnackBar(
                  SnackBar(content: Text('Seleccionado: $value')),
                );
              },
              itemBuilder: (BuildContext context) {
                return [
                  const PopupMenuItem(
                    value: 'Configuración',
                    child: Row(
                      children: [
                        Icon(Icons.settings, size: 20),
                        SizedBox(width: 8),
                        Text('Configuración'),
                      ],
                    ),
                  ),
                  const PopupMenuItem(
                    value: 'Ayuda',
                    child: Row(
                      children: [
                        Icon(Icons.help, size: 20),
                        SizedBox(width: 8),
                        Text('Ayuda'),
                      ],
                    ),
                  ),
                  const PopupMenuItem(
                    value: 'Cerrar sesión',
                    child: Row(
                      children: [
                        Icon(Icons.logout, size: 20),
                        SizedBox(width: 8),
                        Text('Cerrar sesión'),
                      ],
                    ),
                  ),
                ];
              },
            ),
          ],
        ),
        
        // Contenido de la página
        body: ListView.builder(
          itemCount: 20,
          itemBuilder: (context, index) {
            return ListTile(
              leading: CircleAvatar(
                backgroundColor: Colors.deepPurple[100],
                child: Text('${index + 1}'),
              ),
              title: Text('Amigo ${index + 1}'),
              subtitle: Text('Última conexión: hace ${index + 1} horas'),
              trailing: const Icon(Icons.chevron_right),
            );
          },
        ),
        
        // Botón flotante
        floatingActionButton: FloatingActionButton(
          onPressed: () {},
          backgroundColor: Colors.deepPurple,
          child: const Icon(Icons.add),
        ),
      ),
    );
  }
}
```

### **Ejemplo 2: AppBar con Tabs y Search**

```dart
import 'package:flutter/material.dart';

void main() => runApp(const AppBarExample2());

class AppBarExample2 extends StatelessWidget {
  const AppBarExample2({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: DefaultTabController(
        length: 3,
        child: Scaffold(
          appBar: AppBar(
            title: const Text('Tienda Online'),
            backgroundColor: Colors.green,
            
            // AppBar con borde redondeado inferior
            shape: const RoundedRectangleBorder(
              borderRadius: BorderRadius.vertical(
                bottom: Radius.circular(25),
              ),
            ),
            
            // Fondo con gradiente
            flexibleSpace: Container(
              decoration: const BoxDecoration(
                gradient: LinearGradient(
                  colors: [
                    Colors.green,
                    Colors.lightGreen,
                  ],
                  begin: Alignment.topLeft,
                  end: Alignment.bottomRight,
                ),
              ),
            ),
            
            // Barra de búsqueda en el bottom
            bottom: PreferredSize(
              preferredSize: const Size.fromHeight(100),
              child: Padding(
                padding: const EdgeInsets.all(16.0),
                child: Column(
                  children: [
                    // Barra de búsqueda
                    TextField(
                      decoration: InputDecoration(
                        hintText: 'Buscar productos...',
                        prefixIcon: const Icon(Icons.search),
                        filled: true,
                        fillColor: Colors.white,
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(30),
                          borderSide: BorderSide.none,
                        ),
                        contentPadding: const EdgeInsets.symmetric(
                          vertical: 0,
                          horizontal: 20,
                        ),
                      ),
                    ),
                    
                    const SizedBox(height: 10),
                    
                    // Tabs
                    TabBar(
                      indicatorColor: Colors.white,
                      indicatorWeight: 3,
                      labelColor: Colors.white,
                      unselectedLabelColor: Colors.white70,
                      tabs: const [
                        Tab(text: 'Todos'),
                        Tab(text: 'Ofertas'),
                        Tab(text: 'Favoritos'),
                      ],
                    ),
                  ],
                ),
              ),
            ),
            
            // Acciones
            actions: [
              IconButton(
                icon: const Icon(Icons.shopping_cart),
                onPressed: () {
                  ScaffoldMessenger.of(context).showSnackBar(
                    const SnackBar(content: Text('Carrito de compras')),
                  );
                },
              ),
            ],
          ),
          
          // Cuerpo con contenido de tabs
          body: const TabBarView(
            children: [
              // Tab 1: Todos los productos
              Center(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Icon(Icons.store, size: 100, color: Colors.green),
                    SizedBox(height: 20),
                    Text(
                      'Todos los productos',
                      style: TextStyle(fontSize: 20),
                    ),
                  ],
                ),
              ),
              
              // Tab 2: Ofertas
              Center(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Icon(Icons.local_offer, size: 100, color: Colors.orange),
                    SizedBox(height: 20),
                    Text(
                      'Productos en oferta',
                      style: TextStyle(fontSize: 20),
                    ),
                  ],
                ),
              ),
              
              // Tab 3: Favoritos
              Center(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Icon(Icons.favorite, size: 100, color: Colors.red),
                    SizedBox(height: 20),
                    Text(
                      'Productos favoritos',
                      style: TextStyle(fontSize: 20),
                    ),
                  ],
                ),
              ),
            ],
          ),
          
          // Drawer lateral
          drawer: Drawer(
            child: ListView(
              padding: EdgeInsets.zero,
              children: [
                DrawerHeader(
                  decoration: const BoxDecoration(
                    color: Colors.green,
                  ),
                  child: Column(
                    crossAxisAlignment: CrossAxisAlignment.start,
                    mainAxisAlignment: MainAxisAlignment.end,
                    children: [
                      const CircleAvatar(
                        radius: 30,
                        backgroundImage: NetworkImage(
                          'https://i.pravatar.cc/150?img=1',
                        ),
                      ),
                      const SizedBox(height: 10),
                      const Text(
                        'Juan Pérez',
                        style: TextStyle(
                          color: Colors.white,
                          fontSize: 18,
                        ),
                      ),
                      Text(
                        'usuario@email.com',
                        style: TextStyle(
                          color: Colors.white.withOpacity(0.8),
                        ),
                      ),
                    ],
                  ),
                ),
                ListTile(
                  leading: const Icon(Icons.home),
                  title: const Text('Inicio'),
                  onTap: () {},
                ),
                ListTile(
                  leading: const Icon(Icons.person),
                  title: const Text('Perfil'),
                  onTap: () {},
                ),
                ListTile(
                  leading: const Icon(Icons.settings),
                  title: const Text('Configuración'),
                  onTap: () {},
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

### **Ejemplo 3: AppBar Transparente con Imagen de Fondo**

```dart
import 'package:flutter/material.dart';

void main() => runApp(const AppBarExample3());

class AppBarExample3 extends StatelessWidget {
  const AppBarExample3({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        // ExtendBodyBehindAppBar permite que el cuerpo esté detrás del AppBar
        extendBodyBehindAppBar: true,
        
        appBar: AppBar(
          // AppBar transparente
          backgroundColor: Colors.transparent,
          elevation: 0,
          
          // Icono con color blanco para contraste
          iconTheme: const IconThemeData(color: Colors.white),
          
          // Título con sombra para mejor legibilidad
          title: const Text(
            'Galería de Fotos',
            style: TextStyle(
              color: Colors.white,
              fontWeight: FontWeight.bold,
              shadows: [
                Shadow(
                  blurRadius: 10.0,
                  color: Colors.black,
                  offset: Offset(2.0, 2.0),
                ),
              ],
            ),
          ),
          
          centerTitle: true,
          
          // Acciones con botones personalizados
          actions: [
            Container(
              margin: const EdgeInsets.only(right: 16),
              decoration: BoxDecoration(
                color: Colors.white.withOpacity(0.2),
                borderRadius: BorderRadius.circular(20),
              ),
              child: IconButton(
                icon: const Icon(Icons.share, color: Colors.white),
                onPressed: () {
                  ScaffoldMessenger.of(context).showSnackBar(
                    const SnackBar(
                      content: Text('Compartir galería'),
                      backgroundColor: Colors.black87,
                    ),
                  );
                },
              ),
            ),
          ],
        ),
        
        // Cuerpo con imagen de fondo y contenido
        body: Stack(
          children: [
            // Imagen de fondo
            Container(
              decoration: const BoxDecoration(
                image: DecorationImage(
                  image: NetworkImage(
                    'https://images.unsplash.com/photo-1506905925346-21bda4d32df4?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
                  ),
                  fit: BoxFit.cover,
                ),
              ),
            ),
            
            // Overlay oscuro para mejor legibilidad
            Container(
              decoration: BoxDecoration(
                gradient: LinearGradient(
                  begin: Alignment.topCenter,
                  end: Alignment.bottomCenter,
                  colors: [
                    Colors.black.withOpacity(0.3),
                    Colors.black.withOpacity(0.7),
                  ],
                ),
              ),
            ),
            
            // Contenido principal
            SingleChildScrollView(
              padding: const EdgeInsets.only(top: 100),
              child: Column(
                children: [
                  // Tarjeta de información
                  Container(
                    margin: const EdgeInsets.all(20),
                    padding: const EdgeInsets.all(20),
                    decoration: BoxDecoration(
                      color: Colors.white.withOpacity(0.9),
                      borderRadius: BorderRadius.circular(20),
                      boxShadow: [
                        BoxShadow(
                          color: Colors.black.withOpacity(0.2),
                          blurRadius: 10,
                          offset: const Offset(0, 5),
                        ),
                      ],
                    ),
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: [
                        const Text(
                          'Montañas del Norte',
                          style: TextStyle(
                            fontSize: 24,
                            fontWeight: FontWeight.bold,
                          ),
                        ),
                        const SizedBox(height: 10),
                        const Text(
                          'Fotografía tomada durante el amanecer en las montañas del norte. '
                          'La composición juega con la luz natural y los colores del cielo.',
                          style: TextStyle(
                            fontSize: 16,
                            height: 1.5,
                          ),
                        ),
                        const SizedBox(height: 20),
                        
                        // Estadísticas
                        Row(
                          mainAxisAlignment: MainAxisAlignment.spaceAround,
                          children: [
                            _buildStat(Icons.favorite, '1.2K', Colors.red),
                            _buildStat(Icons.visibility, '5.4K', Colors.blue),
                            _buildStat(Icons.comment, '243', Colors.green),
                            _buildStat(Icons.download, '876', Colors.purple),
                          ],
                        ),
                      ],
                    ),
                  ),
                  
                  // Miniaturas de fotos
                  const SizedBox(height: 20),
                  const Padding(
                    padding: EdgeInsets.symmetric(horizontal: 20),
                    child: Text(
                      'Fotos relacionadas',
                      style: TextStyle(
                        color: Colors.white,
                        fontSize: 20,
                        fontWeight: FontWeight.bold,
                      ),
                    ),
                  ),
                  
                  SizedBox(
                    height: 150,
                    child: ListView.builder(
                      scrollDirection: Axis.horizontal,
                      padding: const EdgeInsets.all(20),
                      itemCount: 10,
                      itemBuilder: (context, index) {
                        return Container(
                          width: 120,
                          margin: const EdgeInsets.only(right: 10),
                          decoration: BoxDecoration(
                            borderRadius: BorderRadius.circular(15),
                            image: DecorationImage(
                              image: NetworkImage(
                                'https://images.unsplash.com/photo-${150000 + index}?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60',
                              ),
                              fit: BoxFit.cover,
                            ),
                            boxShadow: [
                              BoxShadow(
                                color: Colors.black.withOpacity(0.3),
                                blurRadius: 5,
                                offset: const Offset(0, 3),
                              ),
                            ],
                          ),
                          child: Container(
                            decoration: BoxDecoration(
                              borderRadius: BorderRadius.circular(15),
                              gradient: LinearGradient(
                                begin: Alignment.bottomCenter,
                                end: Alignment.topCenter,
                                colors: [
                                  Colors.black.withOpacity(0.7),
                                  Colors.transparent,
                                ],
                              ),
                            ),
                            child: Align(
                              alignment: Alignment.bottomCenter,
                              child: Padding(
                                padding: const EdgeInsets.all(8.0),
                                child: Text(
                                  'Foto ${index + 1}',
                                  style: const TextStyle(
                                    color: Colors.white,
                                    fontWeight: FontWeight.bold,
                                  ),
                                ),
                              ),
                            ),
                          ),
                        );
                      },
                    ),
                  ),
                ],
              ),
            ),
          ],
        ),
        
        // Bottom Navigation Bar
        bottomNavigationBar: BottomAppBar(
          color: Colors.black.withOpacity(0.8),
          child: Padding(
            padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 10),
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                IconButton(
                  icon: const Icon(Icons.home, color: Colors.white),
                  onPressed: () {},
                ),
                IconButton(
                  icon: const Icon(Icons.explore, color: Colors.white),
                  onPressed: () {},
                ),
                FloatingActionButton(
                  mini: true,
                  backgroundColor: Colors.white,
                  onPressed: () {},
                  child: const Icon(Icons.add, color: Colors.black),
                ),
                IconButton(
                  icon: const Icon(Icons.notifications, color: Colors.white),
                  onPressed: () {},
                ),
                IconButton(
                  icon: const Icon(Icons.person, color: Colors.white),
                  onPressed: () {},
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
  
  // Widget auxiliar para estadísticas
  Widget _buildStat(IconData icon, String value, Color color) {
    return Column(
      children: [
        Icon(icon, color: color, size: 30),
        const SizedBox(height: 5),
        Text(
          value,
          style: const TextStyle(
            fontWeight: FontWeight.bold,
            fontSize: 16,
          ),
        ),
      ],
    );
  }
}
```

## 📊 Resumen de Características por Ejemplo:

| **Característica** | **Ejemplo 1** | **Ejemplo 2** | **Ejemplo 3** |
|-------------------|---------------|---------------|---------------|
| **Actions** | ✅ (Notificaciones, menú) | ✅ (Carrito) | ✅ (Compartir) |
| **Bottom** | ❌ | ✅ (Tabs + Search) | ❌ |
| **FlexibleSpace** | ❌ | ✅ (Gradiente) | ❌ |
| **Shape** | ❌ | ✅ (Bordes red.) | ❌ |
| **Transparencia** | ❌ | ❌ | ✅ |
| **Drawer** | ❌ | ✅ | ❌ |
| **Tabs** | ❌ | ✅ | ❌ |
| **Badges** | ✅ (Notificaciones) | ❌ | ❌ |

## 💡 Consejos Prácticos:

1. **Para Material 3:** Usa `useMaterial3: true` en ThemeData
2. **Responsive:** Usa `MediaQuery` para ajustar tamaño en diferentes dispositivos
3. **Accesibilidad:** Agrega tooltips a los IconButtons
4. **Performance:** Usa `const` widgets cuando sea posible
5. **Consistencia:** Mantén un estilo uniforme en toda la app

Cada ejemplo muestra diferentes casos de uso comunes en aplicaciones reales, desde redes sociales hasta galerías de fotos y tiendas online.
