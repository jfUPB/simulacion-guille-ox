## Diseño de la aplicación interactiva

**1. ¿De qué trata la aplicación?**

Es un sistema de partículas que se mueve de forma fluida y cambia con la interacción del usuario. La idea es que las partículas sigan un patrón natural usando ruido Perlin para hacer que sus trayectorias sean suaves y orgánicas.
Cada vez que el usuario hace clic con el mouse, ocurren dos cosas:

***Cambio de color:*** Todas las partículas adoptan un nuevo color al mismo tiempo, creando un efecto visual llamativo.

***Aumento de velocidad:*** Con cada clic, las partículas se van moviendo más rápido, lo que hace que la animación se vuelva más intensa y dinámica.
Esto hace que la obra cambie constantemente, dependiendo de cuántas veces interactúe el usuario.

**2. ¿Qué conceptos estoy usando y por qué?**

**a. Ruido Perlin:** Para generar movimientos más naturales y fluidos en las partículas, en lugar de movimientos completamente aleatorios.
**b. Distribución Normal (randomGaussian):** Para que la distribución inicial de las partículas sea más orgánica y no se vean dispersas sin sentido.
**c. Interacción en Tiempo Real:** Porque el usuario puede cambiar el color y la velocidad de todas las partículas simplemente con un clic, haciendo que la animación evolucione de forma interactiva.
Referentes e inspiración
**d. Arte generativo:** Creación de una pieza de arte mediante código.

**3. Referentes:**

- "Flow Fields" de Daniel Shiffman, que usa ruido Perlin para crear trayectorias dinámicas y fluidas.
- Arte generativo de Jared Tarbell, quien explora cómo las partículas pueden formar patrones visuales interesantes.
- El concepto de "Levy Flight", que inspiró la idea de aumentar la velocidad de manera progresiva con cada clic del usuario.
