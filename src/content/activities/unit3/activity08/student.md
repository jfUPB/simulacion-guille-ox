## Paso por valor y paso por referencia

**- El paso por valor** significa que se crea una copia independiente de la variable original. Cualquier cambio en la copia no afecta a la variable original.

**- El paso por referencia**, en cambio, significa que ambas variables apuntan al mismo objeto en memoria. Si una cambia, la otra también se ve afectada.

**1. En el código:**
```js
let friction = this.velocity.copy();
```
Aquí, friction es una copia independiente de this.velocity, porque .copy() crea un nuevo objeto p5.Vector. Cualquier modificación en friction no afectará a this.velocity.

 ```js
let friction = this.velocity;
```
Aquí, friction y this.velocity son el mismo objeto en memoria. Si se modifica friction, también se estaría modificando this.velocity, lo que puede causar errores si esperabas que friction fuera una copia independiente.

**2. ¿Qué podría salir mal?**

Si friction es solo una referencia a this.velocity en lugar de una copia, cualquier cambio en friction afectará la velocidad directamente, lo cual puede generar comportamientos inesperados en la simulación.

**3. Solución:**

Usar .copy() para asegurarse de que friction es una copia y no afecta la velocidad original.
