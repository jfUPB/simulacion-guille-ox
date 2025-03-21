## Movimiento

**1. Código**

```js
let base;
let v1, v2, v3;
let movingArrow;
let t = 0;
let scaleFactor = 1;

function setup() {
  createCanvas(400, 400);
  base = createVector(width / 2, height / 2);
  setVectors();
}

function draw() {
  background(220);

  // Flecha interpolada entre azul y roja
  let lerpFactor = (sin(t) + 1) / 2;
  movingArrow = p5.Vector.lerp(v1, v2, lerpFactor);
  let movingColor = lerpColor(color("blue"), color("red"), lerpFactor);

  // Dibujar el triángulo y la flecha animada
  drawArrow(base, v1, "red");   // Flecha roja
  drawArrow(base, v2, "blue");  // Flecha azul
  drawArrow(v1.copy().add(base), v3, "green"); // Flecha verde (cierra el triángulo)
  drawArrow(base, movingArrow, movingColor); // Flecha animada

  t += 0.02;
}

function drawArrow(base, vec, myColor) {
  push();
  stroke(myColor);
  strokeWeight(3);
  fill(myColor);
  translate(base.x, base.y);
  line(0, 0, vec.x, vec.y);
  rotate(vec.heading());
  let arrowSize = 5;
  translate(vec.mag() - arrowSize, 0);
  triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
  pop();
}

// Cuando se hace clic, la base cambia y los vectores cambian de tamaño aleatorio
function mousePressed() {
  base.set(mouseX, mouseY);
  scaleFactor = random(0.5, 1.5);
  setVectors();
}

function setVectors() {
  v1 = createVector(50 * scaleFactor, 0);   // Flecha roja
  v2 = createVector(0, 50 * scaleFactor);   // Flecha azul
  v3 = p5.Vector.sub(v2, v1);               // Flecha verde (desde v1 hasta v2)
}
```

**2. ¿Cómo solucioné el problema?**

Para hacer que la base de las flechas cambie con cada clic y que el tamaño de los vectores varíe aleatoriamente, hice lo siguiente:

**- Actualizar la base de las flechas:** Cada vez que se hace clic, la nueva base se guarda en la posición actual del mouse.

**- Modificar el tamaño de los vectores aleatoriamente:** Cuando se hace clic, los vectores aumentan o disminuyen su tamaño de forma aleatoria. Esto lo logré multiplicando los vectores por un valor aleatorio que puede ser mayor o menor que 1.

**- Mantener la estructura del triángulo:** La flecha verde debía cerrar correctamente el triángulo, por lo que me aseguré de que siempre comenzara en la punta de la flecha roja y apuntara a la azul.

Con estos ajustes, ahora el triángulo se ajusta dinámicamente y mantiene su estructura, sin importar dónde hagas clic o cómo cambie el tamaño de los vectores. 

