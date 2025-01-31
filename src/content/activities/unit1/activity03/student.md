## Actividad 3

**setup():** Esta función se ejecuta una vez al inicio. Crea un lienzo de 640x640 píxeles, crea un objeto Walker llamado walker y establece un fondo gris.

**draw():** Esta función se ejecuta repetidamente en bucle. En cada iteración, llama a las funciones walker.step() y walker.show() del objeto walker.

**class Walker:** Define una clase que representa a nuestro caminante.

**constructor():** Inicializa la posición del caminante en el centro del lienzo (width/2, height/2).

**show():** Dibuja un punto negro en la posición actual del caminante.

**step():** Esta es la función que genera el movimiento aleatorio. Elige un número aleatorio entre 0 y 3 (floor(random(4))). Dependiendo del número, el caminante se mueve un píxel a la derecha, izquierda, arriba o abajo.
Experimento:

**1.  Pregunta:** ¿Qué pasaría si, en lugar de moverse solo un píxel a la vez, el caminante se moviera una cantidad aleatoria de píxeles en cada paso?

**2. Hipótesis:**  Si el caminante se mueve una cantidad aleatoria de píxeles en cada paso,  el patrón generado será más "disperso" y menos uniforme que el original.  Es decir,  en lugar de una "nube" densa de puntos alrededor del centro, veremos  "saltos" más largos y una distribución más amplia de los puntos en el lienzo.

**3. Modificación del código:**

Para implementar esta modificación, cambié la función step() de la siguiente manera:

![Imagen del código] (https://drive.google.com/file/d/1gWHd7lR3IdEZVQeKBzaouttyNXXEChlR/view?usp=share_link)

**4. Resultado al ejecutar el código:**

![Imagen del resultado] (https://drive.google.com/file/d/1gWHd7lR3IdEZVQeKBzaouttyNXXEChlR/view?usp=share_link)

**5. Documentación del experimento:**

**Descripción del experimento:** Modificar el código para que el caminante se mueva una cantidad aleatoria de píxeles (entre 1 y 4) en cada 
**Pregunta:** ¿Cómo afecta la magnitud del paso a la distribución de los puntos en el lienzo?
**Resultados esperados:** Se espera una distribución más dispersa de los puntos, con "saltos" más largos y una menor densidad de puntos alrededor del origen.
**Resultados obtenidos:** Al ejecutar el código modificado, se observa que la distribución de los puntos es efectivamente más dispersa que en la versión original. Los puntos ya no se concentran tanto alrededor del centro del lienzo, sino que se extienden hacia los bordes con mayor facilidad. Se aprecian "saltos" más largos en el recorrido del caminante, lo que genera un patrón visual con una apariencia más "caótica" o "explosiva".
Aprendizaje: Este experimento me ha permitido comprender cómo la magnitud del paso aleatorio afecta la forma en que se distribuyen los puntos en el lienzo. Un paso mayor genera una dispersión más rápida y un patrón visual menos uniforme. He aprendido que pequeñas modificaciones en el código pueden tener un impacto significativo en el resultado visual, y que la experimentación es clave para comprender y controlar el comportamiento de sistemas con componentes aleatorios.
