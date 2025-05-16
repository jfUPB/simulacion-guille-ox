## Investigación y experimentación con Matter.js

### Experimentos replicados

**Experimento 1:** Mundo con gravedad, cuerpos simples y suelo estático

```js
// Matter.js y p5.js integrados para simular cuerpos con gravedad

// Variables de Matter.js
let Engine = Matter.Engine,
    World = Matter.World,
    Bodies = Matter.Bodies;

let engine;
let world;
let boxes = [];
let ground;

function setup() {
  createCanvas(400, 400);
  
  // Crear el motor y mundo de Matter.js
  engine = Engine.create();
  world = engine.world;
  
  // Crear suelo estático
  ground = Bodies.rectangle(200, height - 10, 400, 20, { isStatic: true });
  World.add(world, ground);
  
  // Crear varios cuerpos rectangulares que caerán
  for (let i = 0; i < 5; i++) {
    let box = Bodies.rectangle(100 + i * 40, 50, 30, 30);
    boxes.push(box);
    World.add(world, box);
  }
}

function draw() {
  background(220);
  
  // Actualizar el motor
  Engine.update(engine);
  
  // Dibujar el suelo
  fill(170);
  rectMode(CENTER);
  rect(ground.position.x, ground.position.y, 400, 20);
  
  // Dibujar las cajas
  fill(127);
  for (let box of boxes) {
    push();
    translate(box.position.x, box.position.y);
    rotate(box.angle);
    rect(0, 0, 30, 30);
    pop();
  }
}
```

Enlace a video de experimento 1: https://drive.google.com/file/d/1K6yGrd63Kh4teIApkAZwWQHw6rmSkpAd/view?usp=drive_link

**Experimento 2:** Interacción con el mouse usando MouseConstraint

```js
// Variables Matter.js
let Engine = Matter.Engine,
    World = Matter.World,
    Bodies = Matter.Bodies,
    Mouse = Matter.Mouse,
    MouseConstraint = Matter.MouseConstraint;

let engine;
let world;
let boxes = [];
let ground;
let mConstraint;

function setup() {
  createCanvas(400, 400);
  
  engine = Engine.create();
  world = engine.world;
  
  ground = Bodies.rectangle(200, height - 10, 400, 20, { isStatic: true });
  World.add(world, ground);
  
  for (let i = 0; i < 5; i++) {
    let box = Bodies.rectangle(100 + i * 40, 50, 30, 30);
    boxes.push(box);
    World.add(world, box);
  }
  
  // Crear objeto mouse para Matter.js
  let canvasmouse = Mouse.create(canvas.elt);
  canvasmouse.pixelRatio = pixelDensity();
  
  // Crear restricción del mouse para interacción
  let options = {
    mouse: canvasmouse
  };
  
  mConstraint = MouseConstraint.create(engine, options);
  World.add(world, mConstraint);
}

function draw() {
  background(220);
  Engine.update(engine);
  
  fill(170);
  rectMode(CENTER);
  rect(ground.position.x, ground.position.y, 400, 20);
  
  fill(127);
  for (let box of boxes) {
    push();
    translate(box.position.x, box.position.y);
    rotate(box.angle);
    rect(0, 0, 30, 30);
    pop();
  }
}
```

Enlace a video de experimento 2: https://drive.google.com/file/d/1lrryfpaqDJ2LIqQeXc7l_l47ZisHLKHI/view?usp=drive_link

### Explicación de conceptos clave

**- Engine:** Es el motor que controla toda la simulación física. Se encarga de calcular el movimiento, colisiones y fuerzas entre los cuerpos.

**- World:** Es el espacio donde están todos los objetos físicos. Pienso en él como el “escenario” donde todo sucede.

**- Bodies:** Son los objetos físicos que podemos crear, como cajas, círculos o polígonos. Pueden moverse, chocar y ser afectados por fuerzas.

**- Constraint:** Es una restricción o vínculo entre dos cuerpos. Sirve para simular cosas como cuerdas o barras rígidas.

**- MouseConstraint:** Es una forma de controlar los cuerpos con el mouse, para poder arrastrarlos o interactuar con ellos en la simulación.

Dificultades encontradas
Al principio me costó entender cómo integrar Matter.js con p5.js, especialmente la forma en que se crean y actualizan los objetos y también me pareció super difícil integrar la librería de Matter.js al editor. También tuve que revisar varias veces cómo funciona el MouseConstraint para que el mouse realmente controlara los cuerpos. Pero con los ejemplos y el video de Patt Vira fue más claro.
