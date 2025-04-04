## Modificación: Random walk traditional

**1. ¿Qué cambios hice?**

- En lugar de this.x y this.y, ahora hay un vector position para la posición del walker.

- En step(), creé un vector step con valores aleatorios en x o y, en lugar de modificar x e y directamente.

- Usé .add() para actualizar la posición sumando el vector step.

**2. Código:**

```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.position = createVector(width / 2, height / 2);
  }

  show() {
    stroke(0);
    point(this.position.x, this.position.y);
  }

  step() {
    let step = createVector(0, 0);
    const choice = floor(random(4));

    if (choice == 0) {
      step.x = 1;
    } else if (choice == 1) {
      step.x = -1;
    } else if (choice == 2) {
      step.y = 1;
    } else {
      step.y = -1;
    }

    this.position.add(step);
  }
}
```

Ahora el código usa vectores para manejar la posición del walker de forma más flexible y escalable. 
