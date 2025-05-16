## Modificación Ejemplo 1.7

**1. Modificación:**

Me pregunté: ¿Qué pasa si la dirección de la velocidad cambia aleatoriamente en cada frame?

**2. Hipótesis**

Si la dirección cambia aleatoriamente, la bola debería moverse de forma caótica, sin un patrón definido.

**3. Modificación en el código**

En cada frame, la dirección del vector de velocidad se ajusta ligeramente con un pequeño valor aleatorio.

```js
let position;
let velocity;

function setup() {
  createCanvas(400, 400);
  position = createVector(width / 2, height / 2);
  velocity = createVector(2, 2); // Velocidad inicial
}

function draw() {
  background(220);

  // Cambiar ligeramente la dirección de la velocidad
  velocity.rotate(random(-PI / 6, PI / 6));

  // Aplicar movimiento
  position.add(velocity);

  // Rebote en los bordes
  if (position.x > width || position.x < 0) {
    velocity.x *= -1;
  }
  if (position.y > height || position.y < 0) {
    velocity.y *= -1;
  }

  // Dibujar el objeto
  fill(0, 0, 255);
  ellipse(position.x, position.y, 20, 20);
}
```

**4. Resultado**

La bola se mueve de manera errática, cambiando de dirección constantemente. A diferencia del ejemplo original, donde la trayectoria es predecible, aquí el movimiento se vuelve más impredecible y caótico.

**5. Explicación**

- El método rotate() en velocity cambia la dirección del vector en un ángulo aleatorio entre -30° y 30° en cada frame.

- Como la dirección se modifica constantemente, el objeto nunca sigue una línea recta y parece moverse de manera aleatoria.

Aún así, los rebotes en los bordes siguen funcionando, lo que evita que el objeto se salga de la pantalla.

**6. Conclusión**

Este tipo de movimiento es útil para simular trayectorias impredecibles, como el movimiento de partículas en el agua o el vuelo errático de un insecto. Sin embargo, si el cambio de dirección es muy drástico, el movimiento se vuelve demasiado caótico y puede parecer más como un "parpadeo" en lugar de un movimiento natural.
