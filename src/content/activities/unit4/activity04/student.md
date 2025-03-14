**0. Link al editor:** https://editor.p5js.org/guille-ox/sketches/kkwfVOCin

**1. Identificación del marco Motion 101**

Motion 101 sigue el mismo principio que en unidades anteriores:

- Se calcula la aceleración con base en las fuerzas aplicadas.

- Se actualiza la velocidad sumando la aceleración.

- Se actualiza la posición sumando la velocidad.

En este caso, la función attract(mover) añade una fuerza de atracción gravitacional entre objetos.

**2. Modificación para incluir fuerzas acumulativas**

Cuando se agregan fuerzas acumulativas, hay que asegurarse de reiniciar la aceleración en cada frame. Esto se hace en el método update() de la clase Mover, sumando todas las fuerzas que actúan en ese instante y luego reseteando la aceleración:

```js
update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0); // Reset aceleración después de aplicarla
}
```

Si no reseteamos this.acceleration, las fuerzas se seguirían acumulando en cada frame, lo que haría que el movimiento se vuelva incontrolable.

**3. Cambio de color del Attractor**

Para cambiar el color del Attractor, modifiqué la función display(). Ahora el color del círculo es azul en lugar del gris predeterminado:

```js
display() {
    ellipseMode(CENTER);
    stroke(0);
    if (this.dragging) {
        fill(50);
    } else if (this.rollover) {
        fill(0, 0, 255, 200); // Color azul con transparencia
    } else {
        fill(175, 200);
    }
    ellipse(this.position.x, this.position.y, this.mass * 2);
}
```

**4. Hacer que el Attractor pueda moverse con el mouse**

Para permitir que el Attractor se arrastre con el mouse y cambie de color cuando el cursor está encima, agregué tres funciones:

```js
// Verificar si el mouse está sobre el Attractor
over() {
    let d = dist(mouseX, mouseY, this.position.x, this.position.y);
    this.rollover = (d < this.mass);
}

// Iniciar arrastre cuando el mouse se presiona
clicked() {
    let d = dist(mouseX, mouseY, this.position.x, this.position.y);
    if (d < this.mass) {
        this.dragging = true;
    }
}

// Mover el Attractor con el mouse
drag() {
    if (this.dragging) {
        this.position.x = mouseX;
        this.position.y = mouseY;
    }
}

// Soltar el Attractor cuando se libera el mouse
released() {
    this.dragging = false;
}
```

Luego, hay que llamar estas funciones dentro de draw() y los eventos de p5.js:

```js
function draw() {
    background(255);

    attractor.over();
    attractor.drag();
    attractor.display();
}

function mousePressed() {
    attractor.clicked();
}

function mouseReleased() {
    attractor.released();
}
```
