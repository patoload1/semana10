# Programa de curso · Programación II

Carrera: Ingeniería de Sistemas de Información

---

# Semana 6 – Práctica semanal (Versión Avanzada)

**Tema:** Objeto base para manejo de colecciones – Nivel avanzado

---

# Actividad 1 (Polimorfismo + Gestión dinámica avanzada)

Implemente la jerarquía:

* Clase abstracta `Figura`
* Clases derivadas: `Circulo`, `Rectangulo` y **Triangulo**

Requisitos:

1. Métodos obligatorios:

   * `double area()`
   * `void escalar(double factor)`
   * `void imprimir()`

2. Use:

   ```cpp
   const int MAX = 20;
   Figura* figuras[MAX];
   ```

3. Debe permitir:

   * Agregar dinámicamente figuras
   * Mostrar información completa (tipo + área)
   * Escalar todas las figuras con un factor variable ingresado por el usuario

4. Restricciones:

   * No usar `vector`
   * Constructores con asignación en el cuerpo
   * Uso obligatorio de punteros

---

# Actividad 2 (Clonación profunda + Regla de Tres)

Extienda la jerarquía anterior:

1. Agregue:

   ```cpp
   virtual Figura* clonar() const = 0;
   ```

2. Implemente clonación en cada clase derivada.

3. Cree una clase nueva:

```cpp
class GestorFiguras {
private:
    Figura* figuras[50];
    int cantidad;

public:
    GestorFiguras();
    ~GestorFiguras();
    GestorFiguras(const GestorFiguras& otro); // constructor copia
    GestorFiguras& operator=(const GestorFiguras& otro); // asignación
};
```

4. Requisitos:

   * Implementar correctamente la **Regla de Tres**
   * Clonación profunda (deep copy)
   * Evitar fugas de memoria

---

# Actividad 3 (Ordenamiento polimórfico)

Implemente una función que:

* Reciba un arreglo de `Figura*`
* Ordene las figuras por área (de menor a mayor)

Restricciones:

* No usar STL (`sort`)
* Implementar manualmente (burbuja, selección o inserción)

---

# Actividad 4 (Downcasting seguro)

Implemente una función que:

* Recorra el arreglo de figuras
* Detecte cuáles son `Circulo` usando `dynamic_cast`
* Muestre solo los radios

Ejemplo esperado:

```
Circulo detectado -> radio: 5.0
```

---

# Actividad 5 (Slicing – análisis crítico)

Responda:

1. ¿Qué ocurre si se usa:

   ```cpp
   Figura figuras[MAX];
   ```
2. ¿Por qué se pierde el polimorfismo?
3. ¿Qué información se pierde exactamente?

Respuesta esperada: 5–8 líneas, explicación técnica.

---

# Actividad 6 (Diseño conceptual – UML en Markdown)

Diseñe la siguiente jerarquía:

Sistema de UI:

* Clase base: `ElementoUI`
* Derivadas: `Boton`, `Etiqueta`, `CajaTexto`

Requisitos:

* Método virtual `dibujar()`
* Método virtual `eventoClick()`
* Justifique:

  * Uso de punteros a la base
  * Problema de slicing
  * Beneficio del polimorfismo

Formato:

```
ElementoUI
 ├── Boton
 ├── Etiqueta
 └── CajaTexto
```

---

# Observaciones

* Se penaliza el uso de `vector`
* Se penaliza slicing
* Se evalúa uso correcto de `new` y `delete`
* Código debe compilar y ejecutar correctamente

---
