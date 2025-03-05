El problema con el código es que cada vez que se llama a applyForce(), la aceleración se sobrescribe en vez de acumularse. O sea, si aplico viento y gravedad, solo se va a quedar con la última fuerza que agregué, lo cual no es correcto porque en la vida real las fuerzas se suman.

**1. ¿Qué solución propongo?**

En lugar de simplemente igualar la aceleración a la fuerza, lo que hay que hacer es sumar todas las fuerzas antes de actualizar el movimiento. También es importante dividir la fuerza por la masa (a = F / m), y al final del frame, resetear la aceleración para que no se acumule de un frame a otro.

**Código:**
```js
class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1; // Se puede cambiar para probar diferentes efectos
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass); // Se divide por la masa para simular correctamente la aceleración
    this.acceleration.add(f); // Se acumula la fuerza en la aceleración
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0); // Se reinicia la aceleración para el siguiente frame
  }

  show() {
    fill(150, 0, 255);
    noStroke();
    ellipse(this.position.x, this.position.y, this.mass * 10);
  }
}

let mover;

function setup() {
  createCanvas(600, 400);
  mover = new Mover();
}

function draw() {
  background(220);

  let gravity = createVector(0, 0.2); // Gravedad
  let wind = createVector(0.1, 0); // Viento

  mover.applyForce(gravity);
  mover.applyForce(wind);
  
  mover.update();
  mover.show();
}
```

**2. ¿Qué cambia con esto?**

- Ahora sí se suman todas las fuerzas en cada frame.

- La aceleración se reinicia después de actualizar la posición, para que no se quede acumulada de un frame a otro.

- La simulación es más realista porque ahora el objeto se ve afectado por múltiples fuerzas al mismo tiempo.
