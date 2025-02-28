## Intención de diseño

Voy a crear una pieza de arte generativo interactivo inspirada en el movimiento de partículas. La idea es que varias partículas se muevan por la pantalla siguiendo el marco MOTION 101, pero con ciertas variaciones:

- Algunas partículas tendrán una aceleración constante.

- Otras tendrán aceleración aleatoria.

- Y otras seguirán el mouse, como si fueran atraídas por él.

El usuario podrá interactuar con el sistema moviendo el mouse para atraer las partículas o presionando teclas para cambiar su comportamiento.

**1. Aplicación de MOTION 101**

Voy a aplicar los principios de posición, velocidad y aceleración para controlar el movimiento de las partículas:

- Posición: Cada partícula tendrá su propia posición en el lienzo.

- Velocidad: Se actualizará en cada frame sumando la aceleración.

- Aceleración: Variará según el tipo de partícula (constante, aleatoria o dirigida al mouse).

Esto permitirá que las partículas se comporten de formas distintas, creando un efecto visual dinámico.

**2. Referentes de inspiración**

- "The Nature of Code" de Daniel Shiffman, especialmente la sección de vectores y motion.

- Sistemas de partículas usados en arte generativo, como los de Casey Reas y generative artists en p5.js.

- Simulaciones de enjambres y boids, donde elementos siguen ciertas reglas para moverse colectivamente.
