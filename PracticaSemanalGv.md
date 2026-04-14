# Programa de curso · Programación II

**Carrera:** Ingeniería de Sistemas de Información

---

# Semana 6 – Práctica semanal

**Tema:** Objeto base para manejo de colecciones – Nivel avanzado

---

## Objetivo de la práctica

Desarrollar una solución orientada a objetos utilizando **herencia, polimorfismo, memoria dinámica, clonación profunda, ordenamiento manual, downcasting seguro y análisis técnico de diseño**, aplicando buenas prácticas de implementación en C++.

---

# Actividad 1 (Jerarquía polimórfica avanzada)

Implemente la siguiente jerarquía de clases:

- Clase abstracta `Figura`
- Clases derivadas:
  - `Circulo`
  - `Rectangulo`
  - `Triangulo`

## Requisitos obligatorios

1. La clase base `Figura` debe declarar como métodos virtuales puros:

```cpp
virtual double area() const = 0;
virtual double perimetro() const = 0;
virtual void escalar(double factor) = 0;
virtual void imprimir() const = 0;
virtual Figura* clonar() const = 0;
virtual ~Figura() {}
