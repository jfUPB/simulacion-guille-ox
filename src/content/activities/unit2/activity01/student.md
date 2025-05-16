## Análisis del Ejemplo Bouncing Ball with Vectors

**1. ¿Cómo funciona la suma de dos vectores?**

Un vector tiene dos valores: x Y y. Cuando sumamos dos vectores, sumamos cada componente por separado.

  **- Ejemplo:**
  
Si position = (3,5) y velocity = (2,-1), la suma se hace así:

position.x = 3 + 2 = 5
position.y = 5 + (-1) = 4

El resultado es position = (5,4), lo que significa que el objeto se mueve en la pantalla.

**2. ¿Por qué position = position + velocity; no funciona?**

En JavaScript, no se pueden sumar objetos con +. Como position y velocity son objetos p5.Vector, hay que usar un método especial:

```js
position.add(velocity);
```

Esto hace la suma correctamente y actualiza la posición del objeto.
