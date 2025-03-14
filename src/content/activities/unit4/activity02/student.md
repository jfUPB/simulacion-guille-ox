## Conceptos fundamentales

### Manejo de Ángulos

**1. ¿Qué está pasando en la simulación? ¿Cuál es la interacción?**

La simulación muestra un sistema donde los elementos gráficos parecen girar alrededor del centro de la pantalla. Esto se logra mediante la función rotate(), que hace que los objetos roten en cada frame.

**2. ¿Por qué se traslada el origen al centro de la pantalla?**

Se hace para que la rotación ocurra alrededor del centro en lugar de la esquina superior izquierda (que es el origen por defecto en p5.js). Al mover el origen con translate(width/2, height/2), cualquier rotación se aplicará alrededor del nuevo centro, haciendo que los objetos giren como si estuvieran conectados a un punto central.

**3. ¿Cuál es la relación entre el sistema de coordenadas y la función rotate()?**

rotate() rota todo el sistema de coordenadas alrededor del origen actual. Si se cambia el origen con translate(), la rotación ocurre en ese nuevo punto en lugar del (0,0) original de la pantalla.

**4. ¿Por qué los elementos gráficos parecen estar dibujándose en (0,0) pero aún así rotan?**

Esto pasa porque, después de trasladar el origen con translate(), el punto (0,0) del sistema de coordenadas ahora está en el centro de la pantalla. Entonces, cuando se dibujan los círculos en (-50,0) y (50,0), en realidad se están posicionando relativos al nuevo origen. Como el sistema de coordenadas entero gira con rotate(), los objetos también giran sin necesidad de recalcular posiciones manualmente en cada frame.

### Rotación en Dirección del Movimiento

**1. ¿Dónde está el marco motion 101 en esta simulación?**

Se encuentra en la forma en la que se actualiza la posición del objeto en función de su velocidad y aceleración. Además, se añade un nuevo concepto: la dirección de movimiento se usa para determinar el ángulo de rotación del objeto.

**2. ¿Qué hace la función heading()?**

heading() obtiene el ángulo de un vector en relación con el eje X. En este caso, devuelve el ángulo de la velocidad del objeto, lo que permite usarlo para rotar el gráfico en la misma dirección en la que se mueve.

**3. ¿Qué hacen push() y pop()?**

**- push()** guarda la configuración actual del sistema de coordenadas.

**- pop()** la restaura después de hacer transformaciones.

Esto es útil porque evita que rotate() y translate() afecten otros objetos dibujados en el mismo frame.

**4. ¿Qué hace rectMode(CENTER)?**

Hace que los rectángulos se dibujen desde su centro en lugar de desde la esquina superior izquierda, lo que ayuda a alinear el objeto correctamente cuando se rota.

**5. ¿Cuál es la relación entre el ángulo de rotación y el vector de velocidad?**

El ángulo de rotación del objeto es el mismo que el ángulo del vector de velocidad. Esto permite que el objeto apunte en la dirección de su movimiento, simulando algo más realista (como un cohete que siempre apunta hacia donde va).
