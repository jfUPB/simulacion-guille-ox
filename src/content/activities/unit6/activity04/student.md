## Actividad 4 — Arte Generativo Interactivo

**1. Algoritmo elegido:** Flocking (basado en el algoritmo de Craig Reynolds y el ejemplo de The Nature of Code)

**2. Concepto de aplicación inesperada:**

"Recuerdos que se agrupan"

En esta pieza, los agentes no representan aves o peces, sino fragmentos de recuerdos dispersos en un espacio abstracto. La forma en que se mueven y se atraen entre sí representa cómo la mente agrupa memorias según estados emocionales o estímulos externos.

Los modos de agrupación reflejan distintos estados mentales:

**Modo 1:** equilibrio mental — los recuerdos flotan suavemente, manteniendo una distancia razonable.

**Modo 2:** nostalgia intensa — los recuerdos se agrupan con fuerza, buscando proximidad emocional.

**Modo 3:** sobrecarga mental — los recuerdos se rechazan entre sí, generando caos interno.

**3. Adaptación del algoritmo:**

El comportamiento de los "boids" se modificó para representar memorias flotando y se implementaron tres modos emocionales con pesos distintos en las reglas de alineación, cohesión y separación. Cada modo tiene además un color característico:

- Blanco (normal)

- Verde (agrupamiento fuerte)

- Rojo (dispersión)

También se añadió una etiqueta visual del modo activo en pantalla para hacer la experiencia más comprensible.

**4. Interacción implementada:**

- Micrófono: la intensidad del sonido ambiente controla el radio de percepción de los agentes. Cuanto más fuerte el sonido, más se “escuchan” entre ellos y más afectan sus comportamientos.

- Teclado:

Tecla 1 → Modo Normal

Tecla 2 → Agrupamiento fuerte (nostalgia)

Tecla 3 → Dispersión (sobrecarga)

- Mouse: clic o pulsación para agregar nuevos recuerdos (boids) al sistema.

**5. Código completo del sketch**

```js

let flock;
let mic;
let mode = 1; // 1 = normal, 2 = agrupamiento fuerte, 3 = dispersión

function setup() {
  createCanvas(800, 600);
  flock = new Flock();

  for (let i = 0; i < 120; i++) {
    flock.addBoid(new Boid(random(width), random(height)));
  }

  mic = new p5.AudioIn();
  mic.start();

  background(0);
  textFont('monospace');
}

function draw() {
  let vol = mic.getLevel(); // Volumen del micrófono
  let mappedVol = map(vol, 0, 0.3, 30, 150); // Afecta radio de percepción

  // Fondo translúcido para efecto de estela
  fill(0, 10);
  noStroke();
  rect(0, 0, width, height);

  // Mostrar modo actual
  fill(255);
  textSize(16);
  textAlign(LEFT, TOP);
  let modeText = '';
  if (mode === 1) {
    modeText = 'Modo 1: Normal';
  } else if (mode === 2) {
    modeText = 'Modo 2: Agrupamiento fuerte';
  } else if (mode === 3) {
    modeText = 'Modo 3: Dispersión';
  }
  text(modeText, 10, 10);

  // Ejecutar el flock
  flock.run(mappedVol, mode);
}

function keyPressed() {
  if (key === '1') {
    mode = 1;
  } else if (key === '2') {
    mode = 2;
  } else if (key === '3') {
    mode = 3;
  }
}

function mousePressed() {
  flock.addBoid(new Boid(mouseX, mouseY));
}

// FLOCK
class Flock {
  constructor() {
    this.boids = [];
  }

  run(perceptionRadius, mode) {
    for (let boid of this.boids) {
      boid.run(this.boids, perceptionRadius, mode);
    }
  }

  addBoid(b) {
    this.boids.push(b);
  }
}

// BOID
class Boid {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = p5.Vector.random2D();
    this.velocity.setMag(random(2, 4));
    this.acceleration = createVector();
    this.maxForce = 0.05;
    this.maxSpeed = 3;
  }

  run(boids, perceptionRadius, mode) {
    this.flock(boids, perceptionRadius, mode);
    this.update();
    this.edges();
    this.show(mode);
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  flock(boids, perceptionRadius, mode) {
    let alignment = createVector();
    let cohesion = createVector();
    let separation = createVector();
    let total = 0;

    for (let other of boids) {
      let d = dist(
        this.position.x,
        this.position.y,
        other.position.x,
        other.position.y
      );
      if (other != this && d < perceptionRadius) {
        alignment.add(other.velocity);
        cohesion.add(other.position);

        let diff = p5.Vector.sub(this.position, other.position);
        diff.div(d * d);
        separation.add(diff);

        total++;
      }
    }

    if (total > 0) {
      alignment.div(total);
      alignment.setMag(this.maxSpeed);
      alignment.sub(this.velocity);
      alignment.limit(this.maxForce);

      cohesion.div(total);
      cohesion.sub(this.position);
      cohesion.setMag(this.maxSpeed);
      cohesion.sub(this.velocity);
      cohesion.limit(this.maxForce);

      separation.div(total);
      separation.setMag(this.maxSpeed);
      separation.sub(this.velocity);
      separation.limit(this.maxForce);
    }

    // Pesos según el modo
    if (mode === 1) {
      alignment.mult(1.0);
      cohesion.mult(1.0);
      separation.mult(1.5);
    } else if (mode === 2) {
      alignment.mult(2.0);
      cohesion.mult(2.5);
      separation.mult(0.5);
    } else if (mode === 3) {
      alignment.mult(0.2);
      cohesion.mult(0.1);
      separation.mult(3.0);
    }

    this.applyForce(alignment);
    this.applyForce(cohesion);
    this.applyForce(separation);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.maxSpeed);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  edges() {
    if (this.position.x > width) this.position.x = 0;
    else if (this.position.x < 0) this.position.x = width;

    if (this.position.y > height) this.position.y = 0;
    else if (this.position.y < 0) this.position.y = height;
  }

  show(mode) {
    // Cambiar color según modo
    if (mode === 1) {
      stroke(255, 200); // blanco
    } else if (mode === 2) {
      stroke(0, 255, 100, 200); // verde
    } else if (mode === 3) {
      stroke(255, 60, 60, 200); // rojo
    }

    strokeWeight(2);
    point(this.position.x, this.position.y);
  }
}
```

**6. Enlace al editor de p5.js:** https://editor.p5js.org/guille-ox/sketches/BNL_a6Xk4

**7. Video de la pieza en acción** https://drive.google.com/file/d/136jW4QITkj2zmDhVxUFwE1NHRCrWbUaz/view?usp=sharing
