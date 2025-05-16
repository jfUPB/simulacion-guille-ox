## Reflexión final del proyecto audiovisual generativo

---

### 1. Conexión sonido-visión

Creo que la conexión entre el sonido y lo visual me salió bastante bien al final. Usé tres cosas principales del audio: el volumen general (amplitude), las frecuencias bajas y las altas. Eso me ayudó a controlar cuántas partículas salían, su tamaño, y qué tan rápido se movían.

En los momentos suaves de la canción, se ve todo más tranquilo, y cuando sube el ritmo, explota con más movimiento y luz. Me gustó mucho que se sintiera como si todo respirara con la música.
Lo más difícil fue entender cómo mapear bien los datos del audio sin que se viera demasiado caótico. Tuve que hacer muchas pruebas para encontrar valores que funcionaran.

---

### 2. Generatividad vs. Control

Desde el principio quería que el sistema respondiera al sonido, pero también que no se repitiera siempre igual. O sea, que cada vez fuera un poco diferente. Para eso mezclé el control del sonido con varias cosas aleatorias:

* Las partículas aparecen en lugares aleatorios.
* Algunas son “orgánicas” y otras tipo “chispas”.
* También usé **ruido Perlin** para que los movimientos fueran más suaves, no como movimientos locos sin sentido.

Así logré un equilibrio entre lo que la música pedía y lo que el sistema inventaba por su cuenta.

---

### 3. Qué conceptos apliqué

En este proyecto usé casi todo lo que vimos en el curso:

* **Fuerzas**: cada partícula siente una fuerza que se genera con el ruido y la energía del sonido.
* **Sistemas de partículas**: todo se organiza con una clase `ParticleSystem` que controla cuántas partículas hay, cómo se actualizan y cuándo se mueren.
* **Ruido Perlin**: lo usé para que el movimiento no fuera tan mecánico.
* **Tamaño y velocidad dinámica**: se modifican según el volumen y las frecuencias.

Fue como juntar todo lo que aprendí, pero aplicado a algo visual y musical que se siente más artístico.

---

### 4. Dificultades con p5.sound

La verdad, al principio me costó entender cómo usar `p5.sound`. El `getLevel()` me daba valores muy bajos o muy cambiantes, y no sabía cómo controlar eso. Lo solucioné usando `map()` con cuidado y también `constrain()` para que los valores no se salieran de control.

Otra cosa complicada fue que si dejaba que salieran muchas partículas sin control, el programa se volvía lento. Tuve que implementar bien el sistema de vida (`lifespan`) para que las viejas se borraran solas.

También me costó un poco entender cómo usar `fft.getEnergy()` en diferentes rangos de frecuencia, pero una vez vi cómo afectaba a las partículas, entendí mejor cómo funcionaba.

---

### 5. Resultado final

Aunque al principio tenía otra idea, siento que este resultado se parece mucho a lo que quería: una visualización que se siente viva, suave, y que reacciona a la música sin ser tan literal.

Lo que más me gusta es que logré un equilibrio entre movimiento y calma, con partículas que parecen flotar y luego explotar con la música. Me hace sentir orgullosa porque al principio todo esto de programar me parecía muy difícil.

Si tuviera más tiempo, me gustaría:

* Agregar más tipos de visuales, como líneas o formas que conecten partículas.
* Tal vez integrar más interacción (con el mouse o el teclado).
* O analizar más el ritmo para hacer que ciertas partes reaccionen de forma más puntual.

---

Fue un proyecto retador, pero también muy bonito de hacer. Aprendí mucho sobre cómo juntar sonido y visuales, y aunque me costó en varios momentos, ver el resultado final en movimiento con la música me hizo sentir que valió la pena.

