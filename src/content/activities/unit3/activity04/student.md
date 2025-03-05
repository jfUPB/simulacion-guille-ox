**1. ¿Dónde está el marco Motion 101 en el código?**

El marco Motion 101 está presente en la forma en que el objeto mover actualiza su posición en el método update(). Se sigue la estructura fundamental:

**- Aceleración:** Se calcula y se aplica a la velocidad.

**- Velocidad:** Se actualiza sumando la aceleración y se limita con limit(this.topSpeed).

**- Posición:** Se actualiza sumando la velocidad.

Este es el flujo básico que define el marco Motion 101:
```js
this.velocity.add(this.acceleration);  
this.velocity.limit(this.topSpeed);  
this.position.add(this.velocity);
```
Cada cuadro del **draw()**, la aceleración modifica la velocidad, que a su vez modifica la posición, generando el movimiento.

**2. ¿Cuáles eran los algoritmos usados para definir la aceleración en la unidad anterior?**

En la unidad anterior, la aceleración se definía manualmente con diferentes estrategias:

**- Aceleración constante:**
```js
this.acceleration.set(0.01, 0.01);
```
Se aplicaba una aceleración fija en cada frame.

**- Aceleración aleatoria:**
```js
this.acceleration = p5.Vector.random2D().mult(0.1);
```
La aceleración cambiaba de dirección en cada frame de manera aleatoria.

**- Aceleración hacia el mouse:**
```js
let mouse = createVector(mouseX, mouseY);
let force = p5.Vector.sub(mouse, this.position);
force.setMag(0.05);
this.acceleration = force;
```
La aceleración se calculaba en función de la dirección hacia el cursor.

**3. ¿Qué tiene que ver esto con las leyes de Newton?**

Las leyes de Newton explican cómo funciona el movimiento de los objetos, y en esta unidad se usan para calcular la aceleración en lugar de definirla directamente.

**- Primera Ley:** Si no hay fuerzas, el objeto mantiene su estado de movimiento. En update(), si la aceleración es cero, el objeto sigue moviéndose con la misma velocidad.

**- Segunda Ley:** F = ma → La aceleración se calcula a partir de fuerzas externas. Ahora, en lugar de establecer la aceleración manualmente, se deriva de una fuerza aplicada al objeto.

**- Tercera Ley:** Cada acción tiene una reacción. Si agregáramos colisiones, podríamos ver esto reflejado.

En esta unidad, se pasa de asignar directamente la aceleración a calcularla en base a fuerzas, lo que hace que la simulación sea más realista.
