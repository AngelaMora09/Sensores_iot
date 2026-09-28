# Preguntas de pensamiento crítico — Semana 3

## Pregunta 1
Una empresa tiene un millón de registros y realiza únicamente cinco búsquedas durante todo el día. ¿Tiene sentido diseñar toda la estrategia de almacenamiento alrededor de una búsqueda binaria? ¿Qué otros costos o factores considerarías?

Respuesta: No tiene sentido diseñar todo alrededor de la búsqueda binaria. Mantener los datos ordenados cuesta (ordenar al inicio y reordenar con cada dato nuevo), y con solo cinco búsquedas la lineal es suficiente: en el experimento, 1.000.000 de comparaciones tardaron unos milisegundos. También pesan la complejidad del código y el costo de mantenimiento. La binaria vale la pena cuando las búsquedas son muy frecuentes.

## Pregunta 2
Un algoritmo puede ser mucho más rápido que otro y, sin embargo, producir una respuesta incorrecta. ¿Por qué consideras que la corrección debe analizarse antes que la eficiencia?

Respuesta: Un algoritmo rápido que responde mal solo entrega respuestas equivocadas más rápido. En el Experimento 4, la binaria por PM2.5 terminó enseguida pero encontró 0 de 20 valores que sí existían. Primero hay que asegurar que el resultado sea correcto y después compararlo en velocidad.

## Pregunta 3
Una plataforma consulta constantemente por `timestamp`, pero ocasionalmente necesita consultar por `PM2.5`. ¿Qué consecuencias tendría organizar los datos pensando principalmente en uno de estos campos?

Respuesta:Los datos solo pueden estar ordenados por un campo a la vez. Si se ordenan por timestamp, esas consultas son muy rápidas y las de PM2.5 quedan lineales, y al revés. Hay que decidir según la consulta más frecuente o más crítica para la plataforma y aceptar que la otra será más lenta, o mantener una estructura adicional con su costo de espacio y actualización.

## Pregunta 4
Tienes un conjunto de datos perfectamente ordenado y alguien modifica algunos registros sin conservar el orden. ¿Qué riesgos aparecen si el sistema continúa utilizando búsqueda binaria sin verificar las condiciones de los datos?

Respuesta: El riesgo es que el sistema falle sin avisar. No lanza error, simplemente dice "no existe" para datos que sí están, y eso puede llevar a decisiones equivocadas sin que nadie lo note. Por eso conviene verificar la precondición del orden, documentarla y controlar quién modifica los datos.

## Pregunta 5
"Que funcione no significa que sea una buena solución." Relaciona esta afirmación con lo aprendido en las semanas 1, 2 y 3 del proyecto. ¿Qué ha cambiado en la manera en que analizas una solución desde que comenzó el proyecto?

Respuesta: En las tres semanas pasé de preguntarme solo si el programa corre a preguntarme cuántas operaciones hace, si escala a millones de datos, si se cumplen las precondiciones de los algoritmos y si las decisiones quedaron documentadas. Esta es la única pregunta sobre ti, así que cámbiala por lo que de verdad sea tu experiencia.