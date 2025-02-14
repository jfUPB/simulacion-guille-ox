## Actividad 4

### 1. Diferencia entre distribuciones uniformes y no uniformes:

**- Distribución Uniforme:** En una distribución uniforme, todos los resultados posibles tienen la misma probabilidad de ocurrir.  Como en el ejemplo, random(100) genera un número entre 0 y 100, y cada número en ese rango tiene la misma chance de salir.  Es como lanzar un dado justo: cada cara tiene la misma probabilidad (1/6).

**-Distribución No Uniforme:** En una distribución no uniforme, algunos resultados tienen más probabilidad de ocurrir que otros. randomGaussian(50, 10) en el ejemplo genera números alrededor de 50, pero los números más cercanos a 50 tienen mucha más probabilidad de aparecer que los números lejanos a 50. Es como si tuvieras un dado cargado: algunas caras salen más frecuentemente que otras.  La distribución Gaussiana (normal) es un ejemplo común de distribución no uniforme.

### 2. Código modificado de la caminata con distribución no uniforme (sesgada a la derecha):

```js

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
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    let r = random(1); // Número aleatorio entre 0 y 1

    if (r < 0.7) { // 70% de probabilidad de moverse a la derecha
      this.x++;
    } else if (r < 0.8) { // 10% de probabilidad de moverse a la izquierda
      this.x--;
    } else if (r < 0.9) { // 10% de probabilidad de moverse hacia abajo
      this.y++;
    } else { // 10% de probabilidad de moverse hacia arriba
      this.y--;
    }
  }
}
```

### 3. Screenshot resultado del código:

![Resultado codigo sesgo a la derecha](../../../../assets/Actividad4.png)
