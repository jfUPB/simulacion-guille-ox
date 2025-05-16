## Visualización Generativa con p5.sound

**Link al editor:** https://editor.p5js.org/guille-ox/sketches/EPU5Zorl4

### ¿Cómo configuré p5.sound y qué datos de audio estoy extrayendo?

Para esta obra generativa en tiempo real, usé la librería `p5.sound` para trabajar con audio. Primero cargué y reproduje una canción (`Wildflowerr.mp3`) usando `loadSound()` y luego la analicé en tiempo real con dos herramientas:

* `p5.Amplitude`: para obtener el volumen general del audio (`getLevel()`).
* `p5.FFT`: para obtener la energía de distintas frecuencias:

  * **Bajas frecuencias** (20–200 Hz) → controlan la dirección de las fuerzas que mueven las partículas.
  * **Altas frecuencias** (2000–10000 Hz) → controlan la velocidad de las partículas tipo "spark".

Estos datos permiten que el sistema de partículas reaccione de forma dinámica al ritmo y tono de la música, generando una visualización que refleja su energía en tiempo real.

---

### Fragmentos clave donde el audio modula el algoritmo generativo

#### 1. **Volumen del sonido controla la cantidad de partículas y su tamaño**:

```js
let vol = amplitude.getLevel();
let emitCount = floor(map(vol, 0, 0.3, 0, 10));
...
particleSystem.updateSize(map(vol, 0, 0.3, 2, 10));
```

#### 2. **Energía de frecuencias bajas controla el movimiento de las partículas**:

```js
let lowEnergy = fft.getEnergy(20, 200);
particleSystem.applyForceToAll(createVector(
  noise(frameCount * 0.01) * lowEnergy * 0.001,
  noise(frameCount * 0.01 + 1000) * lowEnergy * 0.001
));
```

#### 3. **Energía de frecuencias altas aumenta la velocidad de las "spark"**:

```js
let highEnergy = fft.getEnergy(2000, 10000);
particleSystem.updateSparksSpeed(highEnergy * 0.1);
```

Estos tres componentes convierten el audio en una experiencia visual viva y orgánica.

---

### Código completo del sketch

```js
let song;
let amplitude;
let fft;
let particleSystem;

function preload() {
  song = loadSound('Assets/Wildflowerr.mp3');
}

function setup() {
  createCanvas(800, 600);
  amplitude = new p5.Amplitude();
  fft = new p5.FFT();
  
  song.loop();
  
  particleSystem = new ParticleSystem();
}

function draw() {
  background(20, 30, 50, 50);
  
  let vol = amplitude.getLevel();
  let lowEnergy = fft.getEnergy(20, 200);
  let highEnergy = fft.getEnergy(2000, 10000);

  let emitCount = floor(map(vol, 0, 0.3, 0, 10));
  emitCount = constrain(emitCount, 0, 10);
  for(let i = 0; i < emitCount; i++){
    particleSystem.addParticle();
  }

  particleSystem.applyForceToAll(createVector(
    noise(frameCount * 0.01) * lowEnergy * 0.001,
    noise(frameCount * 0.01 + 1000) * lowEnergy * 0.001
  ));
  
  particleSystem.updateSparksSpeed(highEnergy * 0.1);
  particleSystem.updateSize(map(vol, 0, 0.3, 2, 10));
  
  particleSystem.run();
  particleSystem.display();
}

// CLASES PARTICULAS Y SISTEMA

class Particle {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.size = random(2, 5);
    this.lifespan = 255;
    this.type = random() < 0.7 ? 'organic' : 'spark';
  }
  
  applyForce(force) {
    this.acc.add(force);
  }
  
  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.lifespan -= 2;
  }
  
  display() {
    noStroke();
    if(this.type === 'organic') {
      fill(100, 150, 255, this.lifespan);
      ellipse(this.pos.x, this.pos.y, this.size);
    } else {
      fill(255, 255, 150, this.lifespan);
      ellipse(this.pos.x, this.pos.y, this.size / 2);
    }
  }
  
  isDead() {
    return this.lifespan < 0;
  }
}

class ParticleSystem {
  constructor() {
    this.particles = [];
  }
  
  addParticle() {
    this.particles.push(new Particle());
  }
  
  applyForceToAll(force) {
    for(let p of this.particles) {
      p.applyForce(force);
    }
  }
  
  updateSparksSpeed(factor) {
    for(let p of this.particles) {
      if(p.type === 'spark') {
        p.vel.mult(1 + factor);
      }
    }
  }
  
  updateSize(size) {
    for(let p of this.particles) {
      p.size = size;
    }
  }
  
  run() {
    for(let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.update();
      if(p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
  
  display() {
    for(let p of this.particles) {
      p.display();
    }
  }
}
```

---

### VIDEO SIMULACIÓN

https://drive.google.com/file/d/1XGRQVbBVPvVxEqs6I8T3vYO6LiJ1BTFl/view?usp=drive_link

