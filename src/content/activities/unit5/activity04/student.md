## Consolidación

**1. ¿Cómo se gestiona la creación y la desaparición de las partículas y cómo se gestiona la memoria?**

En los ejemplos que trabajé, las partículas se crean dentro del ciclo draw(), normalmente agregando una nueva instancia a un array con particles.push(). Cada partícula tiene una propiedad llamada lifespan que va disminuyendo en cada frame. Cuando esa vida llega a cero o menos, la partícula se considera "muerta" y se elimina del array con splice().

Esto me pareció importante porque si no las eliminamos, la memoria se va llenando con objetos que ya no se usan, y eso puede hacer que el sketch se vuelva más lento o incluso se trabe. Entonces aprendí que manejar la vida de los objetos y limpiarlos cuando ya no sirven es clave para que la simulación funcione bien.

**2. ¿Cómo se aplica el marco de movimiento Motion 101 en los sistemas de partículas que analizaste en la actividad anterior?**

Este marco se basa en usar vectores para controlar el movimiento. Cada partícula tiene position, velocity y acceleration. Las fuerzas se aplican sumándolas a la aceleración, luego la aceleración se suma a la velocidad y la velocidad a la posición. Es un modelo muy simple pero súper útil, porque permite que las partículas se muevan de forma fluida y natural.

Me ayudó a entender cómo funciona el movimiento en p5.js, y cómo pequeñas fuerzas pueden afectar la trayectoria de las partículas de forma acumulativa. También noté que es importante reiniciar la aceleración en cada ciclo para que no se acumulen fuerzas anteriores.

**3. ¿Cómo se aplican fuerzas externas a los sistemas de partículas que trabajaste en la unidad? ¿Qué fuerzas se aplicaron y cómo están modeladas?**

Probé varias fuerzas externas según cada ejemplo:

- La gravedad fue la más directa: un vector constante hacia abajo, como createVector(0, 0.1). Se aplica a todas las partículas en cada frame.

- También usé un atractor, que genera una fuerza hacia un punto. Esa fuerza depende de la distancia, y se calcula con una relación tipo inversa cuadrática, como en la gravedad real.

- Hice lo mismo pero al revés con un repulsor, que aleja a las partículas de su centro.

- Y en otro caso, usé oscilación para que las partículas o los sistemas se movieran como en una onda, usando funciones sin() o cos().

Me gustó ver cómo cada tipo de fuerza cambiaba totalmente el comportamiento de las partículas y cómo las podíamos combinar.

**4. ¿Cómo se aplicaste los conceptos de herencia y polimorfismo en los sistemas de partículas que trabajaste en la unidad?**

Esta parte me costó al principio, pero cuando entendí la lógica, me pareció muy útil. Creé una clase base Particle con todas las funciones comunes (update(), display(), etc.). Luego hice subclases como OscillatingParticle que heredan de Particle, pero modifican algunos métodos para hacer cosas diferentes (por ejemplo, mostrar con colores distintos o moverse en forma de onda).

Lo que más me gustó fue el polimorfismo. Aunque en el array tengo distintas subclases, puedo tratarlas todas como si fueran Particle, y cada una ejecuta su versión propia de los métodos. Es como si hablaran el mismo idioma, pero con personalidad propia. Eso me permitió mezclar comportamientos sin complicar el código del sistema.
