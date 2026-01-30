Para navegar entre pantallas en Flutter, se utiliza la clase **`Navigator`**. Imagina que las pantallas son una "pila" (stack) de hojas: cuando navegas a una nueva, pones una hoja encima; cuando regresas, quitas la de arriba.

Aquí tienes los 2 métodos más comunes para principiantes:

---

### Ejemplo 1: Navegación Directa (Usando `Navigator.push`)
Este es el método más sencillo. Le dices a Flutter exactamente qué pantalla quieres mostrar en el momento que presionas un botón.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(home: PrimeraPantalla()));

// --- PRIMERA PANTALLA ---
class PrimeraPantalla extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Pantalla 1")),
      body: Center(
        child: ElevatedButton(
          child: Text("Ir a la Pantalla 2"),
          onPressed: () {
            // Navigator.push añade la nueva pantalla a la pila
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SegundaPantalla()),
            );
          },
        ),
      ),
    );
  }
}

// --- SEGUNDA PANTALLA ---
class SegundaPantalla extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Pantalla 2")),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Navigator.pop quita la pantalla actual y vuelve a la anterior
            Navigator.pop(context);
          },
          child: Text("Regresar"),
        ),
      ),
    );
  }
}
```

---

### Ejemplo 2: Navegación por Rutas Nombradas
Este método es más organizado para aplicaciones grandes. Defines todas tus pantallas en un solo lugar (como un menú) y les asignas un nombre (un "path" como `/segunda`).

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    title: 'Rutas Nombradas',
    // Definimos la ruta inicial
    initialRoute: '/',
    // Aquí registramos todas las rutas
    routes: {
      '/': (context) => PantallaInicio(),
      '/segunda': (context) => PantallaDetalle(),
    },
  ));
}

class PantallaInicio extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Inicio")),
      body: Center(
        child: ElevatedButton(
          child: Text("Ir a Detalles"),
          onPressed: () {
            // Navegamos usando el nombre que definimos arriba
            Navigator.pushNamed(context, '/segunda');
          },
        ),
      ),
    );
  }
}

class PantallaDetalle extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Detalles")),
      body: Center(
        child: ElevatedButton(
          onPressed: () => Navigator.pop(context),
          child: Text("Volver"),
        ),
      ),
    );
  }
}
```

---

### Diferencias clave:

1.  **Navegación Directa (`push`):**
    *   **Pros:** Rápido de implementar, no necesitas configurar nada previamente.
    *   **Uso:** Ideal para apps muy pequeñas o pantallas que solo se abren desde un único lugar.

2.  **Rutas Nombradas (`pushNamed`):**
    *   **Pros:** El código es más limpio y centralizado. Si decides cambiar el nombre de una clase, solo lo haces en la configuración de rutas.
    *   **Uso:** Es la mejor práctica recomendada para proyectos que van a crecer.

**Tip para principiantes:** Flutter detecta automáticamente si estás en una pantalla secundaria y añade el botón "Atrás" (una flecha) en la barra superior (`AppBar`) sin que tengas que programarlo.
