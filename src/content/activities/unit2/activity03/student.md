## Análisis del código
El código define una variable posicion como un vector p5.Vector y luego pasa esta variable a la función playingVector(), que modifica sus valores x e y.

**1. ¿Qué resultado espero obtener?**

Espero que el vector posicion cambie sus valores de (6,9) a (20,30), ya que en JavaScript los objetos como p5.Vector se pasan por referencia.

**2. ¿Qué resultado obtuve?**

Si imprimimos posicion.toString() después de llamar a playingVector(posicion);, veremos que efectivamente su valor cambió a (20,30).

**3. Paso por valor vs. paso por referencia en JavaScript**

  **-Paso por valor:** cuando pasamos valores primitivos (como números o strings) a una función, se crea una copia de ese valor, por lo que los cambios dentro de la función no afectan la variable original.

```js
function cambiarValor(x) {
    x = 10;
}

let a = 5;
cambiarValor(a);
console.log(a); // Sigue siendo 5
```

  **-Paso por referencia:** cuando pasamos objetos (como arrays o instancias de clases como p5.Vector), en realidad estamos pasando una referencia a la ubicación en memoria del objeto, por lo que los cambios dentro de la función sí afectan el objeto original.

```js
function cambiarVector(v) {
    v.x = 50;
    v.y = 100;
}

let miVector = createVector(5, 10);
cambiarVector(miVector);
console.log(miVector.toString()); // (50,100)
```

**4. ¿Qué tipo de paso se está realizando en el código?**

Se está usando paso por referencia, porque p5.Vector es un objeto y se está modificando directamente dentro de la función playingVector().

**5. ¿Qué aprendí?**

- Que los objetos en JavaScript (como p5.Vector) se pasan por referencia, lo que significa que si los modificamos dentro de una función, los cambios afectan la variable original.

- Que si quisiéramos evitar modificar el original, tendríamos que hacer una copia antes de pasarlo a la función. Por ejemplo, usando copy() en p5.Vector:

```js
let copia = posicion.copy();
playingVector(copia);
```
Así, posicion no se modificaría.
