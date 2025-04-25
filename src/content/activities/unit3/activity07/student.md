El problema aquí es que la función applyForce(force) está dividiendo directamente force entre 10, pero como force es un objeto de la clase p5.Vector, se está modificando el vector original en lugar de solo su copia dentro de la función. Esto significa que si esa misma fuerza force se usa en otro objeto o en otro cálculo, ya estará modificada, lo cual puede generar errores inesperados en la simulación.

**1. Solución:**

En lugar de modificar force directamente, hay que hacer una copia del vector antes de dividirlo. Esto se puede hacer usando el método copy() de p5.Vector, para asegurarnos de que la división solo afecte a la copia y no al vector original.

**2. Implementación en p5.js:**
```js
applyForce(force) {
    let f = force.copy(); // Crear una copia del vector
    f.div(10); // Dividir por la masa
    this.acceleration.add(f); // Sumar a la aceleración
}
```

Así, cada vez que se aplique una fuerza, se trabajará con una copia, evitando modificar la fuerza original.
