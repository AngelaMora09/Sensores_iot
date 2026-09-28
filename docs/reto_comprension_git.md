
# Reto de comprensión — Git y ramas

## Pregunta 1
¿Por qué `main` debe mantenerse estable mientras una nueva funcionalidad está en desarrollo?

Respuesta: main es la versión que siempre debe compilar y funcionar. Es el punto de partida de todo lo demás. Si trabajas ahí y dejas la búsqueda binaria a medias, rompes la versión que otros (o tú misma) usan. En una rama, el desorden no afecta a main, y si sale mal, se descarta.

## Pregunta 2
¿Cuál es la diferencia conceptual entre `feature/` y `bugfix/`?

Respuesta:feature/ agrega una capacidad nueva (por ejemplo, la búsqueda de la Semana 3). bugfix/ corrige algo que ya existía y se comporta mal (por ejemplo, un cálculo o un algoritmo incorrecto). El prefijo dice qué tipo de trabajo hay dentro.

## Pregunta 3
¿Por qué `feature/semana-3-busqueda` es un nombre más útil que `rama3`?

Respuesta:Porque el nombre cuenta el propósito. El del ejemplo dice el tipo de trabajo (feature), el contexto (semana-3) y qué se hace (busqueda). rama3 no dice nada, y con muchas ramas nadie sabría cuál es cuál.

## Pregunta 4
¿Qué ventaja tiene desarrollar una funcionalidad en una rama antes de fusionarla con `main`?

Respuesta: Puedes experimentar, equivocarte y hacer commits sin poner en riesgo main. Solo fusionas cuando ya probaste que funciona. Además, el historial queda ordenado por tarea.

## Pregunta 5
¿Por qué es importante probar `main` después de realizar un merge?

Respuesta:Porque al unir dos líneas de trabajo puede aparecer un error que ninguna tenía por separado (un conflicto mal resuelto, por ejemplo). Probar main confirma que la versión estable sigue estable después de integrar lo nuevo.





Claude es una IA y puede cometer errores. Verifica siempre las respuestas.



