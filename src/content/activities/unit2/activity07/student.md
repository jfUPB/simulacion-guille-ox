## Motion 101

**1. ¿En qué consiste Motion 101?**

Motion 101 es un marco básico para manejar el movimiento de objetos en una animación usando vectores. Se basa en tres elementos clave: posición, velocidad y aceleración.

- La posición determina dónde está el objeto en la pantalla.

- La velocidad es un vector que indica cuánto y en qué dirección se mueve el objeto en cada frame.

- La aceleración cambia la velocidad con el tiempo, lo que hace que el movimiento sea más dinámico.

El proceso funciona así en cada frame:

- Se actualiza la velocidad sumándole la aceleración.

- Se actualiza la posición sumándole la velocidad.

- (Opcional) Se cambia la aceleración para darle efectos más naturales.

**2. Ejemplo**

Si un círculo empieza en el centro de la pantalla y tiene una velocidad hacia la derecha, con cada frame se moverá más a la derecha. Si además le sumamos una aceleración hacia abajo, su movimiento parecerá una caída natural, como si la gravedad lo afectara.

```js
let position;
let velocity;
let acceleration;

function setup() {
  createCanvas(400, 400);
  position = createVector(50, 200);
  velocity = createVector(0, 0);
  acceleration = createVector(0.05, 0); // Aceleración constante hacia la derecha
}

function draw() {
  background(220);

  velocity.add(acceleration); // Velocidad cambia por la aceleración
  position.add(velocity); // Posición cambia por la velocidad

  fill(0);
  ellipse(position.x, position.y, 20, 20); // Dibujar el objeto
}
```

En este código, el círculo empieza en la izquierda y acelera gradualmente hacia la derecha. Si aumentamos la aceleración en y, simularíamos algo cayendo con gravedad. 
