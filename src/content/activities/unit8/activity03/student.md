## Diseño del algoritmo generativo (proceso y outputs)

### Algoritmo generativo (proceso)

Para crear una atmósfera visual orgánica y fluida, usaré un **sistema de partículas con fuerzas moduladas por los inputs de audio**, combinado con ruido Perlin para aportar naturalidad y variación continua.

* **Técnicas usadas:**

  * Sistema de partículas que representan formas orgánicas (líneas y burbujas).

  * Ruido Perlin para deformar formas suavemente.

  * Fuerzas vectoriales que afectan a las partículas, donde la dirección y magnitud se ajustan con el análisis FFT y la amplitud.

  * Aleatoriedad controlada para que cada ejecución sea distinta, usando semillas variables en el ruido y parámetros iniciales aleatorios.

* **Modulación por inputs:**

  * La **amplitud (volumen general)** controla la **cantidad de partículas emitidas** y su tamaño máximo. Cuando el volumen aumenta, más partículas nacen y crecen, y cuando disminuye, las partículas se reducen o desaparecen.

  * La **energía en frecuencias bajas (graves)** modifica la **dirección y fuerza de las fuerzas que mueven las partículas**, creando movimientos ondulantes y lentos que simulan vibraciones profundas.

  * La **energía en frecuencias altas (agudos)** influye en la **velocidad de las partículas más pequeñas** (partículas tipo chispa), haciendo que se muevan más rápido y con más energía cuando hay más agudos.

  * El **mouseX** cambia el parámetro de ruido Perlin que controla la deformación de las formas, alternando entre texturas más suaves o más angulosas.

  * Las **teclas + y -** ajustan la sensibilidad general del sistema a la música (escalar la amplitud y FFT para hacer la reacción más o menos intensa).

Este diseño garantiza que, aunque la misma canción se reproduzca, el uso de ruido y aleatoriedad controlada dará visuales siempre distintas, manteniendo la experiencia fresca.

### Outputs visuales

* **Elementos generados:**

  * Partículas orgánicas que forman líneas curvas o burbujas translúcidas, que se agrupan y se mueven.

  * Pequeñas partículas tipo chispa que aparecen y desaparecen, dando brillo y energía visual.

  * Colores que cambian suavemente según la interacción (mouseX), oscilando entre tonos cálidos y fríos.

* **Propiedades dinámicas controladas por el algoritmo:**

  * **Posición:** Movida por fuerzas moduladas por FFT y ruido Perlin.

  * **Tamaño:** Controlado por amplitud y sensibilidad.

  * **Color:** Varía con interacción y energía de frecuencias.

  * **Opacidad:** Modulada por la edad de partículas y la amplitud.

  * **Velocidad:** Afectada por agudos y gravedad del sonido.

  * **Cantidad:** Variable según el volumen.

---

### Pseudocódigo clave

```pseudocode
inicializar sistema de partículas con posiciones aleatorias
inicializar ruidoPerlin con semilla variable

loop cada frame:
    obtener amplitud_actual
    obtener espectro_fft (bajas y altas frecuencias)
    obtener mouseX, teclas (+/-)

    ajustar sensibilidad según tecla presionada

    calcular numero_particulas_emitir = amplitud_actual * factor_sensibilidad
    emitir nuevas partículas si es necesario

    para cada partícula:
        calcular fuerza_base = vector_ruidoPerlin(posicion, tiempo)
        modificar fuerza_base por energia_bajas (FFT)
        aplicar fuerza_base a velocidad de la partícula

        si partícula es chispa:
            velocidad *= energia_altas (FFT)

        actualizar posición y tamaño según amplitud_actual
        actualizar color según mouseX
        actualizar opacidad según edad y amplitud_actual

    renderizar todas las partículas con sus propiedades
```

