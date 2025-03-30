## Actividad 8 - Hashing & Colas con prioridad

## Hashing

### Ejercicio 105

> Explique qué es una función **hash**.

Una función hash es una función que convierte datos en un valor **fijo, determinista y unidireccional**. Se usa para verificar **integridad**, **almacenar contraseñas** y en estructuras como HashMap. Es fundamental en seguridad y eficiencia computacional.

Un ejemplo de resultado de hash puede ser el de un **commit en Github**  (cada commit tiene un hash unico que lo identifica): [9be7cde867b2811ad4dd148470c307adeaff28a2](https://github.com/KhalidCEU/actividad6_p2/commit/9be7cde867b2811ad4dd148470c307adeaff28a2)
### Ejercicio 106

> Explique qué función hash utiliza Java para objetos de la clase **Integer**.

En Java, la **clase Integer** utiliza el método estático `hashCode(int valor)` para generar el código hash **de un entero**. Este método simplemente **devuelve el propio valor entero como su hash**, ya que los numeros enteros son su propia representación unica en términos de hash

```
System.out.println("Hashcode de 20: " + Integer.hashCode(20));
// Me daría "Hashcode de 20: 20"
```

### Ejercicio 107

> Explique qué función hash utiliza Java para objetos de la clase **String**.

En Java, la **clase String** utiliza el método `hashCode(String cadena)` para calcular el hash de un objeto String. Este método está implementado de la siguiente manera en la clase String:

        hash = s[0] * 31^(n-1) + s[1] * 31^(n-2) + ... + s[n-2] * 31^1 + s[n-1] * 31^0

- **s[i]** es el valor Unicode del carácter en la posición `i`
- **n** es la longitud de la cadena.
- **31** es un **numero primo** que se usa para **minimizar colisiones**.

```
String king  = "king";
System.out.println("Hashcode de 'king': " + king.hashCode());

// Me daría "Hashcode de 'king': 3292055"
```

_Nota: contrariamente al de la clase Integer, este no es un método estatico / no se puede usar de la
forma String.hashcode()_

### Ejercicio 108

> Explique cómo puede implementarse un **map** mediante hashing.

Un **mapa** mediante **hashing** utiliza una **tabla hash** para **almacenar pares clave-valor**. La clave pasa por una función **hash** para obtener un **índice en el array**. Si hay colisiones, se usan técnicas como encadenamiento o direccionamiento abierto. Las operaciones (inserción, búsqueda, eliminación) son rápidas, con un tiempo promedio cercano a **O(1)**.

### Ejercicio 109

> Explique cómo puede implementarse un **conjunto** mediante hashing.

Un **conjunto** implementado mediante **hashing** utiliza una **tabla hash** para **almacenar elementos únicos**. La **clave** de **cada elemento** pasa por una **función hash** que genera un **índice** en el array subyacente.

Si hay **dos claves** con el **mismo índice** (colisión), se **resuelve** mediante **técnicas** como **encadenamiento** o **direccionamiento abierto**. Las operaciones de inserción, búsqueda y eliminación tienen un tiempo promedio cercano a **O(1)**

### Ejercicio 110

> Explique por qué Java **aumenta el tamaño máximo** de una tabla hash **antes de que se llene**

Java **aumenta** el tamaño máximo de una tabla hash **antes de que se llene** para **evitar un exceso de colisiones** y **mantener** el rendimiento constante **O(1)** en las operaciones de búsqueda, inserción y eliminación.

### Ejercicio 111

> Explique por qué Java **recoloca los elementos** de una tabla hash **cuando ésta aumenta de tamaño**.

Java **recoloca los elementos** de una **tabla hash** cuando ésta aumenta de tamaño porque la **función hash depende del tamaño de la tabla** para calcular los índices.

Al **incrementar el tamaño**, las posiciones de los elementos cambian, por lo que es necesario volver a **calcular los índices** (rehashing) y **redistribuirlos** en la nueva tabla.

Esto asegura una distribución uniforme, **minimiza colisiones** y mantiene el rendimiento casi a **O(1)** en las operaciones.

### Ejercicio 112

> Explique por qué es conveniente **especificar el tamaño inicial** de una **HashSet** o de un **HashMap** cuando se espera que éste sea grande.

Es conveniente **especificar el tamaño inicial** de un(a) **HashTable / HashMap** cuando se espera que sea grande porque **evita hacer varios redimensionamientos / recolocaciones** de elementos (lo que mejora el rendimiento).

Cada **redimensionamiento = costos adicionales de tiempo y memoria**, pero al hacer esto se **optimiza el uso de recursos** y se mantiene un **rendimiento constante** en las opereaciones.

### Ejercicio 113

> ¿Qué **consecuencias** tiene el **no reescribir el método hashCode** cuando se define un tipo de elemento para un HashSet o HashMap?

Si no se reescribe el método `hashCode` al definir un tipo de elemento para un `HashSet` o `HashMap` puede ocurrir lo siguiente:

- **Resultados impredecibles**: Objetos que son **iguales según `equals()`** podrían terminar en **diferentes grupos** (de memoria) debido a que el hash por defecto **no respeta la relacion** entre `equals()` y `hashCode`.

- **Bajo rendimiento**: Si el método `hashCode` devuelve valores poco distribuidos (por ejemplo, siempre el mismo valor), todos los elementos se almacenarán en el **mismo grupo (de memoria)**, degradando las operaciones de búsqueda e insercióon a **O(n)**.

- **Inconsistencia**: Cambiar atributos que afectan el resultado de `hashCode`, puede que se nos pierda dentro de una colección, ya que su ubicación **depende del valor original del hash**.


Ejemplo basico de un `hashCode` personalizado (/ reescrito)
```
@Override
public int hashCode() {
    return nombre.hashCode();
}
```
