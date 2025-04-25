**1. ¿Qué concepto de oscilación utilizaste como base para tu obra? Describe cómo lo implementaste.**

Usé la oscilación sinusoidal para generar las ondas expansivas. Al principio me costó entender cómo hacer que las ondas no fueran solo círculos, pero aprendí que con funciones seno y coseno podía crear deformaciones en la forma de las ondas. Implementé esto sumando una variación sinusoidal al radio de cada punto de la onda, lo que hace que tenga un efecto más natural y dinámico.

**2. ¿Cómo funciona la interacción en tu obra? Explica cómo el usuario puede modificar la obra en tiempo real.**

La obra responde al sonido del micrófono. Cuando hay ruido, se generan ondas en la pantalla, y cuando hay silencio total, la próxima vez que aparezca sonido, las ondas empiezan desde un punto distinto. Esto hace que la obra nunca se vea igual. Al principio no entendía bien cómo detectar el silencio y hacer que cambiara el punto de inicio, pero con ayuda logré que se moviera cuando el volumen es menor a cierto umbral.

**3. ¿Qué desafíos encontraste durante el proceso de creación? ¿Cómo los superaste?**

Tuve varios desafíos, pero los más difíciles fueron:

- Hacer que las ondas no se generaran todas en el mismo punto todo el tiempo.

- Lograr que la deformación de la onda se viera natural y no tan geométrica.

- Controlar bien la transparencia de las ondas para que no se acumularan demasiado y saturaran la pantalla.

Al principio, cuando intenté cambiar el punto de origen de las ondas, se movían de forma aleatoria todo el tiempo, lo cual no era lo que quería. Con ayuda, entendí que necesitaba esperar hasta que hubiera un silencio total antes de cambiar el punto de inicio. También tuve que ajustar la velocidad de crecimiento de las ondas para que no desaparecieran demasiado rápido ni se quedaran en pantalla por mucho tiempo.

**4. ¿Qué aprendiste sobre las oscilaciones y su aplicación en el arte generativo?**

Aprendí que las oscilaciones no solo sirven para hacer movimientos de vaivén, sino que también pueden usarse para crear formas dinámicas en el arte generativo. También me di cuenta de que las funciones trigonométricas como seno y coseno son súper útiles para lograr efectos visuales interesantes. Además, trabajar con sonido como entrada me hizo entender cómo el volumen se puede mapear a valores visuales y cómo se puede controlar la interacción en tiempo real. Al principio me sentía perdida con tanto código, pero ahora entiendo mucho mejor cómo funcionan las ondas y la oscilación en gráficos generativos.
