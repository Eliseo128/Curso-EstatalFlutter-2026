Aquí tienes dos ejemplos que cumplen exactamente con lo que pides: una estructura de **Columna que contiene 3 Filas**, y dentro de cada fila una **Card** con imagen de red, título y descripción, todo usando **StatelessWidgets** y temas personalizados.

---

### Ejemplo 1: Guía de Viajes (Tema Azul Índigo)
En este ejemplo, usamos el `Row` para contener la `Card`, y dentro de la `Card` organizamos el contenido. Es un diseño clásico de lista de tarjetas.

```dart
import 'package:flutter/material.dart';

void main() => runApp(AppViajes());

class AppViajes extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      // TEMA Y COLOR
      theme: ThemeData(
        primarySwatch: Colors.indigo,
        scaffoldBackgroundColor: Colors.grey[200],
      ),
      home: PantallaInicio(),
    );
  }
}

class PantallaInicio extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Destinos Turísticos")),
      body: Padding(
        padding: const EdgeInsets.all(10.0),
        // COLUMNA PRINCIPAL
        child: Column(
          children: [
            // FILA 1
            Row(
              children: [
                Expanded(child: TarjetaLugar(
                  titulo: "París, Francia",
                  desc: "La ciudad del amor y la Torre Eiffel.",
                  url: "https://images.unsplash.com/photo-1502602898657-3e91760cbb34?w=500&q=80",
                )),
              ],
            ),
            // FILA 2
            Row(
              children: [
                Expanded(child: TarjetaLugar(
                  titulo: "Roma, Italia",
                  desc: "Historia viva en cada esquina.",
                  url: "https://images.unsplash.com/photo-1552832230-c0197dd311b5?w=500&q=80",
                )),
              ],
            ),
            // FILA 3
            Row(
              children: [
                Expanded(child: TarjetaLugar(
                  titulo: "Tokio, Japón",
                  desc: "Tradición y tecnología moderna.",
                  url: "https://images.unsplash.com/photo-1540959733332-e946670b2f51?w=500&q=80",
                )),
              ],
            ),
          ],
        ),
      ),
    );
  }
}

class TarjetaLugar extends StatelessWidget {
  final String titulo, desc, url;
  TarjetaLugar({required this.titulo, required this.desc, required this.url});

  @override
  Widget build(BuildContext context) {
    return Card(
      elevation: 5,
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Row( // Row dentro de la card para poner imagen a la izquierda
          children: [
            Image.network(url, width: 80, height: 80, fit: BoxFit.cover),
            SizedBox(width: 15),
            Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(titulo, style: TextStyle(fontWeight: FontWeight.bold, fontSize: 18)),
                Text(desc),
              ],
            )
          ],
        ),
      ),
    );
  }
}
```

---

### Ejemplo 2: Menú de Comidas (Tema Naranja)
En este ejemplo, la estructura es similar pero el diseño de la tarjeta es diferente (imagen arriba), manteniendo la jerarquía de **Column -> 3 Rows -> Card**.

```dart
import 'package:flutter/material.dart';

void main() => runApp(AppComida());

class AppComida extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.orange,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MenuPrincipal(),
    );
  }
}

class MenuPrincipal extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Menú del Día")),
      body: SingleChildScrollView( // Por si las tarjetas son muy grandes
        child: Column( // COLUMNA CON 3 FILAS
          children: [
            // FILA 1
            Row(
              children: [
                Expanded(
                  child: TarjetaComida(
                    nombre: "Hamburguesa Especial",
                    info: "Carne premium y queso fundido.",
                    imagen: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500&q=80",
                  ),
                ),
              ],
            ),
            // FILA 2
            Row(
              children: [
                Expanded(
                  child: TarjetaComida(
                    nombre: "Pizza Pepperoni",
                    info: "Masa artesanal y mucho sabor.",
                    imagen: "https://images.unsplash.com/photo-1628840042765-356cda07504e?w=500&q=80",
                  ),
                ),
              ],
            ),
            // FILA 3
            Row(
              children: [
                Expanded(
                  child: TarjetaComida(
                    nombre: "Ensalada César",
                    info: "Opción fresca y saludable.",
                    imagen: "https://images.unsplash.com/photo-1550304943-4f24f54ddde9?w=500&q=80",
                  ),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}

class TarjetaComida extends StatelessWidget {
  final String nombre, info, imagen;
  TarjetaComida({required this.nombre, required this.info, required this.imagen});

  @override
  Widget build(BuildContext context) {
    return Card(
      margin: EdgeInsets.all(10),
      clipBehavior: Clip.antiAlias, // Redondea la imagen con la card
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(15)),
      child: Column(
        children: [
          Image.network(imagen, height: 120, width: double.infinity, fit: BoxFit.cover),
          ListTile(
            title: Text(nombre, style: TextStyle(color: Colors.orange[900], fontWeight: FontWeight.bold)),
            subtitle: Text(info),
            leading: Icon(Icons.restaurant_menu),
          ),
        ],
      ),
    );
  }
}
```

### Explicación de los componentes utilizados:
1.  **`Column`**: Apila las 3 filas verticalmente.
2.  **`Row`**: Actúa como el contenedor horizontal de cada tarjeta.
3.  **`Expanded`**: Dentro de la `Row`, le dice a la `Card` que ocupe todo el ancho disponible.
4.  **`Card`**: Proporciona el diseño con sombra y bordes redondeados.
5.  **`Image.network`**: Carga las imágenes directamente desde internet mediante una URL.
6.  **`ThemeData`**: Define los colores de la aplicación en un solo lugar (`MaterialApp`).
7.  **`StatelessWidget`**: Las clases no cambian su estado internamente, lo que hace el código más simple y eficiente para mostrar información estática.
