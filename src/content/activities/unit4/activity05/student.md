## Coordenadas polares

**0. Link al editor:** https://editor.p5js.org/guille-ox/sketches/BaO_2oROF

**1. Relación entre _r_ y _theta_ con _x_ y _y_**

En coordenadas polares, **r** es la distancia desde el origen y **theta** es el ángulo de rotación. Para convertir estas coordenadas a cartesianas, se usan las fórmulas:

**x = r * cos(θ)
y = r * sin(θ)**

Básicamente, _**x**_ y _**y**_ determinan la posición del punto en el plano, dependiendo del radio y del ángulo. A medida que _**theta**_ aumenta, el punto gira alrededor del origen.

**2. Primera Modificación**

```js
function draw() {
  background(255);
  // Translate the origin point to the center of the screen
  translate(width / 2, height / 2);
  let v = p5.Vector.fromAngle(theta);
  fill(127);
  stroke(0);
  strokeWeight(2);
  line(0, 0, x, y);
  circle(v.x, v.y, 48);
  theta += 0.02;
}
```

  **a. ¿Qué ocurre?****

Aquí el código usa p5.Vector.fromAngle(theta), que crea un vector con un ángulo pero sin escalarlo por r. Esto significa que el punto se mueve dentro de un círculo de radio 1 en lugar del radio definido antes.

  **b. ¿Por qué?**

Porque p5.Vector.fromAngle(theta) devuelve un vector con x = cos(theta) y y = sin(theta), pero no multiplica por r. Entonces, los valores de _**x**_ y _**y**_ quedan dentro del rango [−1,1], haciendo que el círculo sea mucho más pequeño de lo esperado.

**3. Segunda Modificación**

```js
function draw() {
  background(255);
  // Translate the origin point to the center of the screen
  translate(width / 2, height / 2);
  let v = p5.Vector.fromAngle(theta, r);
  fill(127);
  stroke(0);
  strokeWeight(2);
  line(0, 0, v.x, v.y);
  circle(v.x, v.y, 48);
  theta += 0.02;
}
```

  **a. ¿Qué ocurre aquí?**

Ahora el círculo vuelve a moverse a la distancia correcta r del origen.

  **b. ¿Por qué?**

La función p5.Vector.fromAngle(theta, r) crea un vector de ángulo theta, pero esta vez lo escala por r. Es decir, es lo mismo que hacer:

```js
let x = r * cos(theta);
let y = r * sin(theta);
```
Ahora el movimiento es el esperado: un círculo con el radio correcto, moviéndose alrededor del centro de la pantalla.
