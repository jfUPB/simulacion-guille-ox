## mag() y magSq()

**1. ¿Para qué sirve mag()?**

Sirve para saber qué tan largo es un vector. Básicamente, te dice la distancia desde el origen hasta el punto del vector.

**2. ¿Cuál es la diferencia entre mag() y magSq()? ¿Cuál es más eficiente?**

- mag() te da la longitud exacta del vector.

- magSq() te da el cuadrado de la longitud.
  
magSq() es más rápido porque no hace la raíz cuadrada, pero si necesitas la longitud real, mag() es el que hay que usar.

**3. ¿Para qué sirve normalize()?**

Hace que el vector tenga una longitud de 1, sin cambiar su dirección. Sirve cuando solo te importa la dirección, como en movimientos o direcciones de luz en animación.

**4. Explicación rápida del dot()**
 
El dot() sirve para saber qué tan alineados están dos vectores.

- Si el resultado es grande, van casi en la misma dirección.

- Si es 0, son perpendiculares (como una cruz).

- Si es negativo, van en direcciones opuestas.

Se usa en efectos de iluminación y sombras en animaciones.

**5. Diferencia entre la versión estática y la de instancia de dot()**

La versión de instancia se usa con un vector específico:
```js
let resultado = v1.dot(v2);
```

La versión estática se llama desde p5.Vector, sin usar un objeto:
```js
let resultado = p5.Vector.dot(v1, v2);
```

Ambas hacen lo mismo, pero la estática no necesita que v1 sea un objeto específico.

**6. ¿Qué significa el producto cruz geométricamente?**

El producto cruz genera otro vector que es perpendicular a los dos que ya tienes. Su tamaño te dice qué tan grande es el área entre esos dos vectores.

Se usa en animación para calcular normales de superficies, que sirven para hacer sombras y reflejos.

**7. ¿Para qué sirve dist()?**

Te dice qué tan lejos están dos puntos. Por ejemplo, en una animación puedes usarlo para saber si dos objetos están cerca y hacer que choquen o interactúen.

**8. ¿Para qué sirven normalize() y limit()?**

- normalize() hace que un vector tenga longitud 1 (mantiene la dirección, pero no el tamaño).

- limit(n) impone un límite máximo a la longitud del vector.

Ejemplo: Si una partícula se mueve muy rápido, limit(5) puede hacer que no supere una velocidad máxima.
