# Pasando de Python a PHP: Guía para Principiantes

¡Hola! Este documento está pensado para ayudarte a pasar tus conocimientos de programación de Python a PHP. Damos por sentado que ya tenés una base de Programación Orientada a Objetos (POO) de lo que viste en la materia. Vamos a chusmear las diferencias y similitudes clave entre los dos lenguajes, con ejemplos y ejercicios para que te quede todo más claro.

---

## 1. Diferencias Fundamentales

Aunque tanto Python como PHP son lenguajes potentes para el desarrollo web, tienen algunas diferencias de base:

| Característica | Python | PHP |
| :--- | :--- | :--- |
| **Uso Principal** | Lenguaje de propósito general, muy fuerte en desarrollo web, ciencia de datos, IA y scripting. | Principalmente un lenguaje de scripting del lado del servidor para desarrollo web. |
| **Sintaxis** | Famoso por su sintaxis limpia, legible y concisa, que le da mucha importancia a la indentación. | La sintaxis es más parecida a la de lenguajes como C, usando llaves `{}` y punto y coma `;`. |
| **Curva de Aprendizaje** | Generalmente se lo considera más fácil para principiantes absolutos por su sintaxis simple. | Puede ser más fácil para quienes ya vengan de programar en C, C++ o Java. |

---

## 2. Sintaxis y Conceptos Básicos

Veamos una comparación, lado a lado, de algunas estructuras de programación fundamentales.

### **Salida por Consola**

Para mostrar información, ambos lenguajes tienen formas muy directas.

**Python:**
Usa la función `print()`, que automáticamente agrega un salto de línea al final.
```python
print("Hola, consola")
print("Otra línea")
```

**PHP:**
Usa la construcción `echo`. **Importante:** no agrega un salto de línea, tenés que ponerlo vos con `\n`. Además, cada sentencia termina con `;`.
```php
echo "Hola, consola\n";
echo "Otra línea";
```

### **Variables**

En Python, declarás las variables sin ningún carácter especial. En PHP, a las variables se les pone un signo de pesos `$` adelante.

**Python:**
```python
mi_variable = "¡Hola, Python!"
```

**PHP:**
```php
$mi_variable = "¡Hola, PHP!";
```

### **Arreglos (Listas)**

Lo que en Python conocés como `list`, en PHP se llama `array`. La sintaxis moderna es muy parecida.

**Python:**
```python
mi_lista = ["manzana", "banana", "naranja"]
print(mi_lista)  # Imprime "manzana"
```

**PHP:**
```php
$mi_array = ["manzana", "banana", "naranja"];
echo $mi_array; // Imprime "manzana"
```

### **Diccionarios (Arrays Asociativos)**

Los diccionarios de Python son `associative arrays` en PHP. En lugar de un índice numérico, usás una clave (string) para acceder a los valores.

**Python:**
```python
mi_diccionario = {
    "nombre": "Juan",
    "edad": 30
}
print(mi_diccionario["nombre"]) # Imprime "Juan"
```

**PHP:**
```php
$mi_array_asociativo = [
    "nombre" => "Juan",
    "edad" => 30
];
echo $mi_array_asociativo["nombre"]; // Imprime "Juan"
```

### **Estructuras Condicionales**

Python usa la indentación para definir los bloques de código, mientras que PHP usa llaves `{}`.

**Python:**
```python
if x > y:
    print("x es mayor que y")
elif x == y:
    print("x es igual a y")
else:
    print("x es menor que y")
```

**PHP:**
```php
if ($x > $y) {
    echo "x es mayor que y";
} elseif ($x == $y) {
    echo "x es igual a y";
} else {
    echo "x es menor que y";
}
```

### **Bucles (Loops)**

PHP tiene varias formas de recorrer estructuras, siendo `foreach` la más común y útil para arrays.

**Python:**
```python
for i in range(5):
    print(i)

# Bucle while
contador = 0
while contador < 5:
    print(contador)
    contador += 1
```

**PHP:**
```php
// Bucle for
for ($i = 0; $i < 5; $i++) {
    echo $i;
}

// Bucle foreach (ideal para recorrer arrays)
$frutas = ["manzana", "banana", "naranja"];
foreach ($frutas as $fruta) {
    echo $fruta . "\n";
}

// Bucle while
$contador = 0;
while ($contador < 5) {
    echo $contador;
    $contador++;
}

// Bucle do-while (se ejecuta al menos una vez)
$contador = 10;
do {
    echo "El contador es: " . $contador;
} while ($contador < 5); // Aunque la condición es falsa, se ejecuta una vez
```
---

## 3. Programación Orientada a Objetos (POO)

Tanto Python como PHP tienen un soporte muy completo para POO. Así es como se implementan los conceptos clave en cada lenguaje.

### **Clases y Objetos**

Definir una clase y crear un objeto es bastante directo en los dos lenguajes.

**Python:**
```python
class MiClase:
    def __init__(self, nombre):
        self.nombre = nombre

mi_objeto = MiClase("Objeto de Python")
```

**PHP:**
```php
class MiClase {
    public $nombre;

    public function __construct($nombre) {
        $this->name = $nombre;
    }
}

$mi_objeto = new MyClass("Objeto de PHP");
```

### **Herencia**

La herencia permite que una clase "hija" herede propiedades y métodos de una clase "padre".

**Python:**
```python
class ClaseHija(ClasePadre):
    # ...
```

**PHP:**
```php
class ClaseHija extends ClasePadre {
    // ...
}
```

### **Miembros Estáticos (Variables y Métodos de Clase)**

Los miembros estáticos pertenecen a la clase en sí, no a una instancia particular. Todas las instancias comparten la misma variable estática.

**Python:**
Se usan variables de clase y el decorador `@classmethod`.
```python
class Usuario:
    # Variable de clase (estática)
    contador = 0

    def __init__(self, nombre):
        self.nombre = nombre
        Usuario.contador += 1 # Se accede a través de la clase

    @classmethod
    def obtener_contador(cls):
        return cls.contador

user1 = Usuario("Ana")
user2 = Usuario("Beto")
print(f"Total de usuarios: {Usuario.obtener_contador()}") # Se llama desde la clase
```

**PHP:**
Se usa la palabra clave `static` y el operador `::` (Scope Resolution Operator).
```php
class Usuario {
    // Variable estática
    public static $contador = 0;
    public $nombre;

    public function __construct($nombre) {
        $this->nombre = $nombre;
        self::$contador++; // Se accede con self::
    }

    public static function obtenerContador() {
        return self::$contador;
    }
}

$user1 = new Usuario("Ana");
$user2 = new Usuario("Beto");
echo "Total de usuarios: " . Usuario::obtenerContador(); // Se llama desde la clase
```

---

## 4. Ejercicios Prácticos

1.  **El clásico "¡Hola, Mundo!"**
    Escribí un programa simple en Python y en PHP que imprima "¡Hola, Mundo!".

2.  **Recorrer un Array**
    Creá un array de tus 3 películas favoritas en PHP y recorrelo con un bucle `foreach` para imprimir cada una en una línea distinta.

3.  **Clase con Miembro Estático**
    Creá una clase `Producto` en PHP con una variable estática que cuente cuántos productos se han creado. Añade un método estático para obtener ese contador.

---

## 5. Autoevaluación

1.  ¿Cuál es el carácter principal que se usa para identificar una variable en PHP?
2.  ¿Cómo se define un bloque de código en Python versus PHP?
3.  ¿Qué palabra clave se usa para la herencia en PHP?
4.  ¿Cómo se accede a un método estático en PHP? ¿Y a una variable estática dentro de la misma clase?
5.  ¿Qué bucle usarías en PHP si necesitás la clave y el valor de un array asociativo? (Pista: `foreach ($array as $clave => $valor)`)

***

Este documento te da un pantallazo general para que arranques tu camino de Python a PHP. Recordá siempre consultar la documentación oficial de cada lenguaje para tener información más detallada.