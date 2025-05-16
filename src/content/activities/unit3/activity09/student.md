**Para modelar una fuerza en una simulación, hay que seguir estos pasos:**

**1. Identificar la fuerza**

  - Decidir qué tipo de fuerza queremos modelar (gravedad, fricción, resistencia del aire, etc.).
  
  - Entender cómo se comporta en la vida real para imitarlo en código.
    
**2. Definir su ecuación matemática**

  - Las fuerzas en la física suelen tener fórmulas específicas. Por ejemplo, la gravedad **se calcula con:** F=m⋅g

  - Si es fricción, **se usa:** F = − μ ⋅ N    

  - Se debe escribir en términos de vectores para que funcione en la simulación.

**3. Implementarla en código**

  - Crear un p5.Vector que represente la fuerza.
    
  - Si depende de la masa, dividir por ella para obtener la aceleración.

  - Aplicarla al objeto usando applyForce().

**4. Actualizar en cada frame**

  - Cada fuerza se debe aplicar en cada frame dentro del draw().

  - Sumar todas las fuerzas antes de actualizar la aceleración y velocidad.
    
En resumen, modelar una fuerza es entender cómo funciona en la realidad, expresarla con ecuaciones, implementarla en código y aplicarla constantemente en la simulación.
