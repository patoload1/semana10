

**Carrera:** Ingeniería de Sistemas de Información  
**Universidad:** UNA – Escuela de Informática  
**Semana 6 – Sesión 1 (Estudiantes)** **Duración:** 2 horas  
**Tema:** Objeto base para manejo de colecciones – Parte 1

---

## 1. Fundamento Teórico: Polimorfismo y Clases Base

En Programación Orientada a Objetos (POO), el polimorfismo permite tratar distintos tipos de objetos como si fueran del mismo tipo base. Esto se logra mediante herencia, métodos virtuales y el uso de punteros o referencias.

Una clase base define un conjunto de operaciones comunes que serán implementadas por sus clases derivadas. Esto permite diseñar sistemas más flexibles, extensibles y mantenibles.

Una clase base abstracta se caracteriza por tener al menos un método virtual puro, lo que obliga a las clases derivadas a implementar dicho comportamiento.


```python?code_reference&code_event_index=2

### Ejemplo de clase base
```cpp
class Figura {
public:
    virtual double area() = 0;
    virtual void escalar(double factor) = 0;
    virtual ~Figura() {}
};
```

### Características importantes
* No se puede instanciar directamente.
* Define un contrato para las clases hijas.
* Permite polimorfismo en tiempo de ejecución.

---

## 2. Polimorfismo en C++

El polimorfismo permite que un mismo puntero o referencia a la clase base invoque diferentes implementaciones de métodos dependiendo del tipo real del objeto. Esto se logra mediante el uso de funciones virtuales.

### Ejemplo
```cpp
Figura* f = new Circulo(5.0);
cout << f->area();
```

Aunque `f` es de tipo `Figura*`, el método ejecutado es el de **Circulo**. Esto se conoce como enlace dinámico o despacho dinámico.

### Conceptos clave
* **Enlace estático:** ocurre en tiempo de compilación.
* **Enlace dinámico:** ocurre en tiempo de ejecución.
* El uso de `virtual` permite habilitar el enlace dinámico.

---

## 3. Manejo de Colecciones con Punteros

Para manejar múltiples objetos de distintas clases derivadas de forma uniforme, se utiliza un arreglo de punteros a la clase base.

```cpp
const int MAX = 10;
Figura* figuras[MAX];
int numFiguras = 0;
```

### Ventajas
* Permite almacenar diferentes tipos de objetos.
* Mantiene el comportamiento polimórfico.
* Evita pérdida de información del objeto.

### Inserción de elementos
```cpp
figuras[numFiguras++] = new Circulo(1.0);
figuras[numFiguras++] = new Rectangulo(2.0, 3.0);
```

### Recorrido del arreglo
```cpp
for (int i = 0; i < numFiguras; i++) {
    cout << figuras[i]->area() << endl;
}
```

### Aplicar una operación común
```cpp
for (int i = 0; i < numFiguras; i++) {
    figuras[i]->escalar(2.0);
}
```

---

## 4. Clases Derivadas

Las clases derivadas heredan de la clase base y deben implementar los métodos virtuales.

### Clase Circulo
```cpp
class Circulo : public Figura {
private:
    double radio;

public:
    Circulo(double r) {
        radio = r;
    }

    double area() {
        return 3.1416 * radio * radio;
    }

    void escalar(double factor) {
        radio = radio * factor;
    }
};
```

### Clase Rectangulo
```cpp
class Rectangulo : public Figura {
private:
    double base;
    double altura;

public:
    Rectangulo(double b, double h) {
        base = b;
        altura = h;
    }

    double area() {
        return base * altura;
    }

    void escalar(double factor) {
        base = base * factor;
        altura = altura * factor;
    }
};
```

---

## 5. Manejo de Memoria Dinámica

Cuando se utiliza `new` para crear objetos, es obligatorio liberar la memoria utilizando `delete`.

```cpp
for (int i = 0; i < numFiguras; i++) {
    delete figuras[i];
}
```

### Problemas si no se libera memoria
* Fugas de memoria.
* Consumo innecesario de recursos.
* Posibles fallos del sistema.

---

## 6. Concepto Clave: Slicing

El slicing ocurre cuando un objeto derivado se copia en una variable de tipo base por valor.

### Ejemplo incorrecto
```cpp
Figura figuras[MAX];
```

### Problema
* Se pierde la información específica del objeto derivado.
* Se eliminan atributos adicionales.
* Se pierde el comportamiento polimórfico.

**Explicación breve:** El slicing ocurre cuando un objeto derivado se asigna a una variable de tipo base, lo que provoca la pérdida de los datos y comportamientos específicos de la clase derivada. Esto impide el uso correcto del polimorfismo.

---

## 7. Comparación de Enfoques

| Tipo de almacenamiento | Polimorfismo | Resultado |
| :--- | :--- | :--- |
| `Figura figuras[MAX]` | No | **Incorrecto** |
| `Figura* figuras[MAX]` | Sí | **Correcto** |

---

## 8. Buenas Prácticas

* Declarar métodos virtuales en la clase base.
* Usar destructor virtual.
* Utilizar punteros para manejar polimorfismo.
* Liberar memoria con `delete`.
* Evitar el uso de objetos por valor en jerarquías.
* Mantener consistencia en constructores (asignación en el cuerpo).

---

## 9. Criterios de Evaluación

* [ ] Uso correcto de arreglo de punteros.
* [ ] No utilización de vector.
* [ ] Constructores con asignación en el cuerpo.
* [ ] Uso de `using namespace std;`.
* [ ] Aplicación correcta de polimorfismo.
* [ ] Liberación adecuada de memoria.

---

## 10. Conclusión

El uso de una clase base abstracta junto con un arreglo de punteros permite manejar diferentes tipos de objetos de manera uniforme. Este enfoque es fundamental para aplicar polimorfismo, evitar errores como el slicing y desarrollar sistemas más escalables y mantenibles en C++.
