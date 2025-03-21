**0. Links al editor:**

  **- Ejemplo 4.2: An Array of Particles:** https://editor.p5js.org/guille-ox/sketches/jaf8MSOGj

## 1. Ejemplo 4.2: An Array of Particles

**- Gestión de creación y desaparición de partículas y manejo de memoria:**

En este ejemplo, se crea un array para almacenar múltiples partículas. En cada ciclo de dibujo (draw()), se añade una nueva partícula al array. Luego, se itera sobre el array para actualizar y mostrar cada partícula. Si una partícula ha "muerto" (es decir, su tiempo de vida ha llegado a cero), se elimina del array utilizando el método splice(). Esto asegura que la memoria se gestione adecuadamente al eliminar las partículas que ya no son necesarias.

**- Modificación propuesta: Incorporar el concepto de fuerzas (Unidad 2)**

Añadí una fuerza de gravedad que afecta a todas las partículas. Esto implica aplicar una fuerza constante hacia abajo en cada ciclo de dibujo.

**- Implementación:**

```js
let particles = [];
let gravity;

function setup() {
  createCanvas(800, 600);
  gravity = createVector(0, 0.1);
}

function draw() {
  background(255);

  // Añadir una nueva partícula en cada frame
  particles.push(new Particle(createVector(width / 2, 50)));

  // Iterar sobre el array de partículas
  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];
    p.applyForce(gravity);
    p.update();
    p.display();
    if (p.isDead()) {
      particles.splice(i, 1);
    }
  }
}

class Particle {
  constructor(position) {
    this.position = position.copy();
    this.velocity = createVector(random(-1, 1), random(-2, 0));
    this.acceleration = createVector(0, 0);
    this.lifespan = 255;
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    this.lifespan -= 2;
  }

  display() {
    stroke(0, this.lifespan);
    fill(175, this.lifespan);
    ellipse(this.position.x, this.position.y, 12, 12);
  }

  isDead() {
    return this.lifespan < 0;
  }
}
```

**- Explicación:**

**Concepto aplicado:** Fuerzas (Unidad 2)

**Aplicación:** Se define un vector de gravedad que se aplica a cada partícula en cada ciclo de dibujo.

**Razón:** Incorporar fuerzas realistas mejora la simulación, haciendo que las partículas se comporten de manera más natural.

**- Captura de la simulación**

foto

## 2. Ejemplo 4.4: A System of Systems

**- Gestión de creación y desaparición de partículas y manejo de memoria:**

En este ejemplo, se gestionan múltiples sistemas de partículas. Cada sistema de partículas es responsable de crear, actualizar y eliminar sus propias partículas. La memoria se gestiona eliminando partículas "muertas" de cada sistema y eliminando sistemas vacíos del array principal.

**- Modificación propuesta:** Incorporar el concepto de oscilaciones (Unidad 3)

Añadí una oscilación a la posición inicial de cada sistema de partículas para que se muevan de forma ondulatoria en la pantalla.

**- Implementación:**

```js
let systems = [];
let angle = 0;

function setup() {
  createCanvas(800, 600);
}

function draw() {
  background(255);

  // Añadir un nuevo sistema de partículas en una posición oscilante
  let x = width / 2 + sin(angle) * 100;
  let y = 50;
  systems.push(new ParticleSystem(createVector(x, y)));
  angle += 0.05;

  // Iterar sobre el array de sistemas de partículas
  for (let i = systems.length - 1; i >= 0; i--) {
    let ps = systems[i];
    ps.addParticle();
    ps.run();
    if (ps.isEmpty()) {
      systems.splice(i, 1);
    }
  }
}

class ParticleSystem {
  constructor(position) {
    this.origin = position.copy();
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin));
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.update();
      p.display();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }

  isEmpty() {
    return this.particles.length === 0;
  }
}

class Particle {
  constructor(position) {
    this.position = position.copy();
    this.velocity = createVector(random(-1, 1), random(-2, 0));
    this.acceleration = createVector(0, 0);
    this.lifespan = 255;
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    this.lifespan -= 2;
  }

  display() {
    stroke(0, this.lifespan);
    fill(175, this.lifespan);
    ellipse(this.position.x, this.position.y, 12, 12);
  }

  isDead() {
    return this.lifespan < 0;
  }
}
```

**- Explicación:**

**Concepto aplicado:** Oscilaciones (Unidad 3)

**Aplicación:** Se utiliza una función seno para mover la posición inicial de cada sistema de partículas en un patrón oscilante.

**Razón:** Esto añade un movimiento dinámico y atractivo a la simulación, mostrando cómo las oscilaciones pueden integrarse en sistemas de partículas.
