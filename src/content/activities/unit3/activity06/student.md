## Por qué multiplicar por cero

Es necesario multiplicar la aceleración por cero al final de cada frame porque, en cada ciclo de actualización, la aceleración es la sumatoria de todas las fuerzas que actúan sobre el objeto en ese instante. Si no la reiniciamos a cero, esas fuerzas seguirían acumulándose en cada frame, lo que haría que el objeto se acelerara sin control en cada iteración.

La aceleración debe calcularse en función de las fuerzas aplicadas en ese frame específico, no en los anteriores. Al multiplicarla por cero, nos aseguramos de que en el siguiente frame solo se consideren las nuevas fuerzas aplicadas, evitando que se acumulen indefinidamente y generen un movimiento poco realista.
