## Animación Tipográfica Semántica

**Link al editor:** https://editor.p5js.org/guille-ox/sketches/JNRz1_crP

**Link video:** https://drive.google.com/file/d/1UkOp4_QrNaLgILvof9wKcEAn0lt8nf5p/view?usp=drive_link

### Palabra elegida: Eco

**1. Idea conceptual**
   
La palabra "Eco" representa el fenómeno acústico donde un sonido se refleja y repite varias veces, disminuyendo su intensidad y tamaño a medida que se dispersa en el espacio.

En esta animación, la palabra aparece al presionar cualquier tecla y cada letra es un cuerpo físico que rebota en las paredes invisibles del canvas. Cada vez que una letra choca contra un muro, genera un "eco": una copia más pequeña que se lanza en otra dirección. La letra original se reduce progresivamente en tamaño, simulando que se desintegra en ecos. Estos ecos también rebotan y se hacen más pequeños hasta desaparecer.

Así, la animación física representa el significado de "Eco" mediante la repetición y el desvanecimiento progresivo en el espacio visual, simulando el comportamiento de un sonido reflejado que se dispersa.

**2. Aspectos técnicos clave**

- Formación de las letras: Cada letra de la palabra "Eco" es representada como un cuerpo rectangular de Matter.js con una etiqueta label para identificarlo. Las letras se crean como rectángulos dinámicos ubicados horizontalmente con un espaciado proporcional.

- Propiedades físicas importantes: restitution alta para que las letras reboten con elasticidad.

- Sin gravedad (world.gravity.y = 0) para que se muevan solo por sus velocidades y rebotes.

- frictionAir para simular una leve desaceleración.

- Cada letra original disminuye de tamaño (escala) progresivamente con cada choque contra un muro.

**3. Efecto "eco":**

Al detectar una colisión entre una letra y un muro (usando Events.on en el motor de Matter.js), se crea un nuevo cuerpo más pequeño con velocidad aleatoria en otra dirección, representando el eco. Este cuerpo también rebota y se reduce lentamente hasta desaparecer.

- Interacción: Se genera una nueva palabra "Eco" (con sus letras físicas) al presionar cualquier tecla, reiniciando la animación.

- Restricciones: No se usaron restricciones (Constraint) para mantener libertad de movimiento a las letras y ecos.

**4. Código**

```js
// Matter.js + p5.js: Animación "Eco" con letras que rebotan y generan ecos

let Engine = Matter.Engine,
    World = Matter.World,
    Bodies = Matter.Bodies,
    Events = Matter.Events,
    Body = Matter.Body;

let engine;
let world;

let letters = [];  // Letras originales (cuerpos)
let boundaries = [];

let ecoLetters = []; // Ecos (letras más pequeñas)
const originalWord = "Eco";

// Clase Boundary para muros invisibles
class Boundary {
  constructor(x, y, w, h) {
    this.w = w;
    this.h = h;
    this.body = Bodies.rectangle(x, y, w, h, {isStatic: true, label: 'boundary'});
    World.add(world, this.body);
  }
  show() {
    // No dibujamos los muros porque son invisibles
  }
}

function setup() {
  createCanvas(600, 300);
  engine = Engine.create();
  world = engine.world;
  world.gravity.y = 0; // Sin gravedad

  // Crear muros (boundaries)
  boundaries.push(new Boundary(width/2, -10, width, 20)); // arriba
  boundaries.push(new Boundary(width/2, height+10, width, 20)); // abajo
  boundaries.push(new Boundary(-10, height/2, 20, height)); // izquierda
  boundaries.push(new Boundary(width+10, height/2, 20, height)); // derecha

  textFont('Arial');
  textStyle(BOLD);
  textAlign(CENTER, CENTER);
  noStroke();

  // Registra evento de colisiones *DESPUÉS* de crear engine y world
  Events.on(engine, 'collisionStart', function(event) {
    let pairs = event.pairs;
    for (let pair of pairs) {
      let labels = [pair.bodyA.label, pair.bodyB.label];
      if(labels.includes('letter') && labels.includes('boundary')){
        let letterBody = pair.bodyA.label === 'letter' ? pair.bodyA : pair.bodyB;
        let originalLetter = letters.find(l => l.body === letterBody);
        if(originalLetter && originalLetter.size > 20){
          createEcho(originalLetter);
          originalLetter.size *= 0.85;
          Matter.Body.scale(originalLetter.body, 0.85, 0.85);
        }
      }
    }
  });
}

function draw() {
  background(30);
  Engine.update(engine);

  for(let l of letters){
    showLetter(l);
  }

  for(let i = ecoLetters.length - 1; i >= 0; i--){
    let e = ecoLetters[i];
    showLetter(e);
    e.size *= 0.97;
    if(e.size < 8){
      World.remove(world, e.body);
      ecoLetters.splice(i, 1);
    }
  }
}

function showLetter(obj) {
  let pos = obj.body.position;
  let angle = obj.body.angle;
  push();
  translate(pos.x, pos.y);
  rotate(angle);
  fill(200, 230, 255);
  textSize(obj.size);
  text(obj.letter, 0, 0);
  pop();
}

function createWord(x, y, size, velocity) {
  let spacing = size * 0.7;
  let lettersArr = [];
  for(let i = 0; i < originalWord.length; i++){
    let letter = originalWord.charAt(i);
    let body = Bodies.rectangle(x + i*spacing, y, size*0.6, size, {
      restitution: 0.95,
      friction: 0,
      frictionAir: 0.01,
      label: 'letter'
    });
    Body.setVelocity(body, velocity);
    World.add(world, body);
    lettersArr.push({body: body, letter: letter, size: size});
  }
  return lettersArr;
}

function createEcho(originalLetter) {
  let pos = originalLetter.body.position;
  let size = originalLetter.size * 0.6;
  let angle = random(PI/4, (3*PI)/4);
  let speed = random(5, 8);
  let direction = random() > 0.5 ? 1 : -1;

  let velocity = {
    x: speed * cos(angle) * direction,
    y: speed * sin(angle) * direction
  };

  let body = Bodies.rectangle(pos.x, pos.y, size*0.6, size, {
    restitution: 0.9,
    friction: 0,
    frictionAir: 0.02,
    label: 'ecoLetter'
  });
  Body.setVelocity(body, velocity);
  World.add(world, body);
  ecoLetters.push({body: body, letter: originalLetter.letter, size: size});
}

function keyPressed() {
  // Limpiar letras originales anteriores
  for(let l of letters){
    World.remove(world, l.body);
  }
  letters = createWord(width/2 - 60, height/2, 80, {x: random(-10,10), y: random(-10,10)});
}
```

**5. Video:** https://drive.google.com/file/d/1UkOp4_QrNaLgILvof9wKcEAn0lt8nf5p/view?usp=drive_link
