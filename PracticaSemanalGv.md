# Programa de curso · Programación II

**Carrera:** Ingeniería de Sistemas de Información

---

# Semana 6 – Práctica semanal

**Tema:** Objeto base para manejo de colecciones – Nivel avanzado

---

## Objetivo

Desarrollar una solución en C++ aplicando herencia, polimorfismo, memoria dinámica, clonación profunda, ordenamiento manual y buenas prácticas de diseño.

---

# Actividad 1 – Jerarquía de clases

Implemente la siguiente jerarquía:

* Clase abstracta `Figura`
* Clases derivadas:

  * `Circulo`
  * `Rectangulo`
  * `Triangulo`

## Métodos obligatorios

```cpp
virtual double area() const = 0;
virtual double perimetro() const = 0;
virtual void escalar(double factor) = 0;
virtual void imprimir() const = 0;
virtual Figura* clonar() const = 0;
virtual ~Figura() {}
```

## Requisitos

* Atributos privados
* Validación de datos
* Uso obligatorio de punteros

## Estructura de almacenamiento

```cpp
const int MAX = 20;
Figura* figuras[MAX];
int cantidad;
```

## Funcionalidades

* Agregar figuras
* Mostrar figuras
* Calcular área y perímetro
* Escalar todas las figuras
* Mostrar figura de mayor área
* Calcular promedio de áreas

---

# Actividad 2 – Clase Gestor (Regla de Tres)

```cpp
class GestorFiguras {
private:
    Figura* figuras[50];
    int cantidad;

    void liberarMemoria();
    void copiarDesde(const GestorFiguras& otro);

public:
    GestorFiguras();
    ~GestorFiguras();
    GestorFiguras(const GestorFiguras& otro);
    GestorFiguras& operator=(const GestorFiguras& otro);

    bool agregarFigura(Figura* f);
    void mostrarFiguras() const;
    void escalarTodas(double factor);
    double promedioAreas() const;
    Figura* figuraMayorArea() const;
    void ordenarPorAreaAscendente();
    void mostrarSoloCirculos() const;
};
```

## Requisitos

* Implementar Regla de Tres
* Copia profunda usando `clonar()`
* Evitar fugas de memoria
* No compartir punteros

---

# Actividad 3 – Ordenamiento

Implementar:

```cpp
void ordenarPorAreaAscendente();
```

## Restricciones

* No usar STL
* Implementar manualmente (burbuja, selección o inserción)

---

# Actividad 4 – Downcasting

Recorrer el arreglo y:

* Detectar `Circulo` con `dynamic_cast`
* Mostrar radio
* Mostrar datos de `Rectangulo` y `Triangulo`

## Ejemplo esperado

```txt
Circulo -> radio: 5.0
Rectangulo -> base: 4.0 altura: 8.0
Triangulo -> base: 6.0 altura: 3.0
```

---

# Actividad 5 – Slicing

Responda:

1. ¿Qué ocurre con:

```cpp
Figura figuras[MAX];
```

2. ¿Qué es object slicing?
3. ¿Qué información se pierde?
4. ¿Cómo afecta al polimorfismo?

**Respuesta:** 8–12 líneas.

---

# Actividad 6 – Copia profunda

Explique:

* Diferencia entre shallow copy y deep copy

Responda:

1. ¿Qué tipo usa `GestorFiguras`?
2. ¿Qué pasa si solo copia punteros?
3. ¿Qué errores genera?

---

# Actividad 7 – Menú

```txt
1. Agregar círculo
2. Agregar rectángulo
3. Agregar triángulo
4. Mostrar figuras
5. Escalar figuras
6. Ordenar por área
7. Mostrar círculos
8. Mayor área
9. Promedio de áreas
10. Probar copia
11. Salir
```

## Requisitos

* Validar entradas
* Probar copia profunda

---

# Actividad 8 – UML

```txt
ElementoUI
 ├── Boton
 ├── Etiqueta
 ├── CajaTexto
 └── CheckBox
```

## Métodos

```cpp
virtual void dibujar() const = 0;
virtual void eventoClick() = 0;
virtual ElementoUI* clonar() const = 0;
```

## Responder

* ¿Por qué usar punteros?
* ¿Qué pasa con slicing?
* ¿Ventaja del polimorfismo?

---

# Actividad 9 – Sobrecarga

Implementar:

```cpp
ostream& operator<<(ostream& out, const Figura& f);
```

Debe imprimir:

* Tipo
* Dimensiones
* Área
* Perímetro

---

# Actividad 10 – Análisis

Responder:

1. ¿Por qué destructor virtual?
2. ¿Para qué sirve `clonar()`?
3. ¿Por qué usar clase base?
4. ¿Qué principio de diseño aplica?

---

# Restricciones

* No usar `vector`
* No usar `sort`
* Uso obligatorio de punteros
* Uso correcto de `new` y `delete`
* Separación en `.h` y `.cpp`

---
# Análisis de diseño orientado a objetos – Aplicación del principio ISP

Considere el siguiente fragmento de código en C++ relacionado con un sistema de biblioteca:

```cpp
class ISistemaBiblioteca {
public:
    virtual void prestarLibro() = 0;
    virtual void devolverLibro() = 0;
    virtual void registrarLibro() = 0;
    virtual void gestionarUsuarios() = 0;
    virtual void consultarCatalogo() = 0;
    virtual ~ISistemaBiblioteca() = default;
};

class IPrestarLibro {
public:
    virtual void prestarLibro() = 0;
    virtual ~IPrestarLibro() = default;
};

class Lector : public IPrestarLibro, public IDevolverLibro, public IConsultarCatalogo {
private:
    string nombre;
public:
    Lector(string n) : nombre(n) {}

    void prestarLibro() override {
        cout << nombre << " solicita el préstamo de un libro." << endl;
    }

    void devolverLibro() override {
        cout << nombre << " devuelve un libro." << endl;
    }

    void consultarCatalogo() override {
        cout << nombre << " consulta el catálogo de libros." << endl;
    }
};
class IPrestarLibro {
public:
    virtual void prestarLibro() = 0;
    virtual ~IPrestarLibro() = default;
};

class Lector : public IPrestarLibro, public IDevolverLibro, public IConsultarCatalogo {
private:
    string nombre;
public:
    Lector(string n) : nombre(n) {}

    void prestarLibro() override {
        cout << nombre << " solicita el préstamo de un libro." << endl;
    }

    void devolverLibro() override {
        cout << nombre << " devuelve un libro." << endl;
    }

    void consultarCatalogo() override {
        cout << nombre << " consulta el catálogo de libros." << endl;
    }
};
```


##  Instrucción para el estudiante

Analice el diseño presentado y determine si cumple adecuadamente con el Principio de Segregación de Interfaces (ISP), el cual establece que una clase no debe verse obligada a depender de métodos que no utiliza.
En el código se observa una interfaz general llamada ISistemaBiblioteca que concentra múltiples responsabilidades, tales como prestar libros, devolverlos, registrar libros, gestionar usuarios y consultar el catálogo. Sin embargo, no todos los actores del sistema necesariamente requieren todas esas operaciones. Por ejemplo, un lector probablemente pueda consultar el catálogo, solicitar préstamos y devolver libros, pero no debería encargarse del registro de libros ni de la gestión de usuarios.
A partir de esta situación, realice un análisis crítico del diseño y responda:


¿Qué problema de diseño podría surgir al utilizar una interfaz demasiado grande como ISistemaBiblioteca?

¿Por qué sería incorrecto obligar a una clase como Lector a implementar métodos que no necesita?

Explique de qué manera el uso de interfaces pequeñas y específicas como IPrestarLibro favorece el cumplimiento del principio ISP.

Proponga un rediseño del sistema utilizando interfaces separadas según responsabilidades.

Justifique por qué el nuevo diseño sería más mantenible, flexible y escalable.

Lo que se espera en su análisis
El estudiante debe identificar que una interfaz grande viola el principio ISP cuando agrupa responsabilidades que no aplican a todos los tipos de usuario. También debe reconocer que una clase como Lector solo debería implementar las operaciones que realmente necesita.
Finalmente, debe proponer una solución basada en interfaces específicas, por ejemplo:


IPrestarLibro
IDevolverLibro
IConsultarCatalogo
IRegistrarLibro
IGestionarUsuarios


De esta forma, cada clase implementará únicamente los contratos que correspondan a su rol dentro del sistema.
