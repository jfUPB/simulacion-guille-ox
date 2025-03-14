## Modelando fuerzas

Cada una de estas simulaciones demuestra cómo se modela una fuerza en el mundo de los píxeles.

**- Fricción:** La velocidad disminuye progresivamente hasta detenerse.

**- Resistencia del aire:** Afecta más a objetos rápidos, haciéndolos desacelerar progresivamente.

**- Atracción gravitacional:** El objeto se mueve hacia el centro de atracción, acelerando a medida que se acerca.

**1. Fricción**

**- Link:** https://editor.p5js.org/guille-ox/sketches/eh0qleuvh

**Cómo la modelé:**

- La fricción es una fuerza opuesta al movimiento, proporcional a la velocidad.

- **Se calcula como:** Fricción = - coef * velocidad, donde coef es el coeficiente de fricción.

- Se aplica la fricción restándola de la velocidad en cada frame.

```js
let mover;

function setup() {
  createCanvas(600, 400);
  mover = new Mover();
}

function draw() {
  background(220);
  
  let friction = mover.velocity.copy();
  friction.mult(-1);
  friction.setMag(0.05); // Coeficiente de fricción

  mover.applyForce(friction);
  mover.update();
  mover.edges();
  mover.show();
}

class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector(2, 0);
    this.acceleration = createVector(0, 0);
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  edges() {
    if (this.position.x > width || this.position.x < 0) {
      this.velocity.x *= -1;
    }
  }

  show() {
    fill(200, 0, 200);
    ellipse(this.position.x, this.position.y, 30);
  }
}
```

**2. Resistencia del Aire**

**- Link:** https://editor.p5js.org/guille-ox/sketches/x2mHcEF55

**Cómo la modelé:**

- Se aplica una fuerza proporcional a la velocidad al cuadrado, en dirección opuesta al movimiento.

- Se usa la fórmula: Fresistencia = - coef * vel^2.

```js
let mover;

function setup() {
  createCanvas(600, 400);
  mover = new Mover();
}

function draw() {
  background(220);
  
  let resistance = mover.velocity.copy();
  resistance.mult(-1);
  resistance.setMag(mover.velocity.magSq() * 0.01); // Simula resistencia del aire

  mover.applyForce(resistance);
  mover.update();
  mover.edges();
  mover.show();
}

class Mover {
  constructor() {
    this.position = createVector(width / 2, 50);
    this.velocity = createVector(2, 2);
    this.acceleration = createVector(0, 0);
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  edges() {
    if (this.position.y > height) {
      this.velocity.y *= -1;
      this.position.y = height;
    }
  }

  show() {
    fill(0, 200, 200);
    ellipse(this.position.x, this.position.y, 30);
  }
}
```

**3. Atracción Gravitacional**

**- Link:** https://editor.p5js.org/guille-ox/sketches/V0Q8AzXpw

**Cómo la modelé:**

- **Se usa la fórmula de atracción gravitacional:** F = G * (m1 * m2) / d^2, donde G es la constante gravitatoria.

- La fuerza se aplica en dirección al otro objeto.

```js
let attractor;
let mover;

function setup() {
  createCanvas(600, 400);
  attractor = new Attractor(width / 2, height / 2);
  mover = new Mover(random(width), random(height));
}

function draw() {
  background(220);

  let force = attractor.attract(mover);
  mover.applyForce(force);

  mover.update();
  mover.show();
  attractor.show();
}

class Mover {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-2, 2), random(-2, 2));
    this.acceleration = createVector(0, 0);
    this.mass = 2;
  }

  applyForce(force) {
    let f = force.copy().div(this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    fill(200, 50, 50);
    ellipse(this.position.x, this.position.y, this.mass * 10);
  }
}

class Attractor {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.mass = 20;
  }

  attract(mover) {
    let force = p5.Vector.sub(this.position, mover.position);
    let distance = constrain(force.mag(), 5, 25);
    let strength = (1 * this.mass * mover.mass) / (distance * distance);
    force.setMag(strength);
    return force;
  }

  show() {
    fill(50, 50, 200);
    ellipse(this.position.x, this.position.y, this.mass);
  }
}
```
