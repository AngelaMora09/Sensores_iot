# Bitacora individual - Semana [XX]

> Copia este archivo y renombralo como `s[XX]-[tu-nombre].md`.
> Completa todas las secciones con tus propias palabras. Esta bitacora es
> individual, aunque el codigo pueda haberse construido en equipo.

## 1. Datos de la actividad

- **Estudiante:** Angela Mora 
- **Equipo:** Individual
- **Semana:** 3
- **Fecha del laboratorio:** [28-09-2026]
- **Fecha del taller:** [28-09-2026]
- **Tema principal:** Búsqueda lineal, búsqueda binaria y análisis de eficiencia
- **Pregunta de la semana:** ¿Cómo encontramos una lectura específica cuando el repositorio pasa de cientos a cientos de miles o millones de registros?

## 2. Prediccion antes de ejecutar

Antes de abrir o ejecutar el programa, responde:

1. **Que creo que va a ocurrir?**
   Esperaba que la búsqueda binaria por PM2.5 encontrara los 20 valores buscados, igual que la búsqueda lineal. (Escribo esta predicción después de ejecutar el programa, pero corresponde a lo que esperaba antes de ver ese resultado.)

2. **Que parte del programa o del algoritmo puede fallar?**
   La parte que quería comprobar era la búsqueda binaria por PM2.5: si encontraba los mismos valores que la búsqueda lineal.

3. **Como comprobare mi prediccion?**
   IngestaSensores y comparando cuántos de los 20 valores encontraba cada búsqueda.

## 3. Evidencia del laboratorio

### Resultado observado

[Al ejecutar IngestaSensores, la ingesta de las semanas anteriores siguió funcionando (201 lecturas almacenadas, 2 descartadas por formato y 8 por rango) y después se ejecutaron los experimentos de la Semana 3:

Con 1.000.000 de lecturas, la búsqueda lineal necesitó 1.000.000 de comparaciones y la búsqueda binaria por timestamp necesitó 20.
Con 100.000 lecturas y un timestamp que no existe, ambas devolvieron -1: la lineal con 100.000 comparaciones y la binaria con 17.
Al buscar por PM2.5 20 valores que sí existen, la búsqueda lineal encontró 20 y la binaria encontró 0.
Los 10 casos de prueba de la búsqueda binaria (primer elemento, elemento intermedio, último elemento, y timestamp inexistente antes y después, en arreglos de 10 y de 1.000.000 de lecturas) dieron OK.]

### Diferencia entre la prediccion y el resultado

[Esperaba que la búsqueda binaria encontrara los 20 valores y encontró 0. La diferencia se explica porque los datos no están ordenados por PM2.5: la búsqueda binaria descarta la mitad del arreglo en cada paso suponiendo que está ordenado, y con datos desordenados puede descartar justo la mitad donde estaba el valor.]

### Error o comportamiento inesperado

- **Que ocurrio?** [La búsqueda binaria por PM2.5 encontró 0 de 20 valores que sí existen en el arreglo, mientras que la búsqueda lineal encontró los 20. Además, un caso de prueba ("inexistente antes") no probaba el borde izquierdo, porque su timestamp no seguía el formato de los datos generados (0000000000, 0000000001, ...) y quedaba después de todos ellos.]
- **Por que ocurrio?** [Los datos no están ordenados por PM2.5, y la búsqueda binaria solo funciona si el arreglo está ordenado por el campo buscado. En el caso de prueba, el texto elegido se comparaba como mayor que todos los timestamps generados.]
- **Como lo corregimos o que falta corregir?** [La búsqueda por PM2.5 se conserva como experimento para mostrar la precondición; para usarla de verdad habría que ordenar antes (tema de la Semana 4). El caso de prueba se corrigió usando -000000001, que sí queda antes de todos los timestamps.]

## 4. Explicacion en lenguaje llano

Explica el concepto principal como se lo explicarias a una persona de doce
anos. Usa entre tres y cinco lineas y evita palabras tecnicas que no expliques.

Es como imaginar que se tienen 1.000.000 de tarjetas ordenadas de menor a mayor número y buscas una. En vez de revisarlas una por una, miras la tarjeta del medio: si la que buscas tiene un número mayor, tiras toda la primera mitad, y si es menor, tiras la segunda. Repites con la mitad que queda hasta encontrarla. Solo funciona si las tarjetas están bien ordenadas; si estuvieran revueltas, podrías tirar justo la mitad donde estaba la que buscabas.
### Ejemplo o analogia

[Buscar una palabra en un diccionario abriéndolo por la mitad. La página del medio representa el valor del medio, y el orden alfabético representa el orden de los datos: según la palabra que veas, sabes si tu palabra está antes o después, y descartas la otra mitad. La analogía deja de ser exacta porque una persona ve la letra y salta cerca de donde debería estar, mientras que la búsqueda binaria siempre va exactamente al punto medio.]

## 5. El vacio que encontre

Al intentar explicar el tema, identifica el punto que aun no comprendes bien.

- **Mi duda concreta es:** [¿Por qué bastan unas 20 comparaciones para buscar entre 1.000.000 de lecturas?]
- **Lo que ya puedo explicar es:** [Que la búsqueda binaria descarta la mitad de los datos en cada paso y que necesita datos ordenados. Lo vi en la traza y en el experimento 3.]
- **Para resolver la duda consulte:** [El experimento 3, que muestra 20 comparaciones con 1.000.000 de lecturas, y la explicación de un asistente.]
- **Ahora lo entiendo asi:** [Cada comparación reduce a la mitad lo que queda por revisar: 1.000.000, luego 500.000, 250.000, y así hasta llegar a 1. Si cuento cuántas veces puedo dividir a la mitad hasta llegar a 1, salen unas 20 veces, porque 2 multiplicado por sí mismo 20 veces es 1.048.576, un poco más de un millón.]

## 6. Trazado de la solucion

Caso: buscar el 3 en el arreglo [0, 1, 2, 3] con una versión incorrecta del ciclo, que usa inicio = medio en lugar de inicio = medio + 1. Fórmula: medio = (inicio + fin) / 2, con división entera.

| Paso | Estado de los datos o estructura | Decision o resultado |
|---|---|---|
| 1 | inicio = 0, fin = 3, medio = 1, valor medio = 1] | [1 < 3, entonces inicio = medio = 1] |
| 2 | [inicio = 1, fin = 3, medio = 2, valor medio = 2] | [2 < 3, entonces inicio = medio = 2] |
| 3 | [	inicio = 2, fin = 3, medio = 2, valor medio = 2] | [2 < 3, entonces inicio = medio = 2 (no cambia)] |
| 4 | [	inicio = 2, fin = 3, medio = 2, valor medio = 2] | [Igual que el paso 3: el ciclo se repite sin terminar] |

**Con la regla correcta (inicio = medio + 1), en el paso 3 inicio pasaría a 3, medio sería 3 y encontraría el valor en la posición 3.

## 7. Decision de diseño

Relaciona lo aprendido con la Plataforma de Monitoreo Ambiental Urbano.

- **Problema que debiamos resolver:** [Encontrar una lectura por timestamp entre cientos de miles o millones de lecturas sin revisarlas una por una.]
- **Estructura, algoritmo o estrategia elegida:** [Búsqueda binaria por timestamp, sobre lecturas ordenadas cronológicamente.]
- **Alternativa descartada:** [Búsqueda lineal por timestamp. También se descartó la búsqueda binaria por PM2.5, porque los datos no están ordenados por ese campo.]
- **Por que elegimos la primera:** [Con 1.000.000 de lecturas necesita 20 comparaciones en lugar de 1.000.000. Su costo es que exige mantener los datos ordenados; si dejan de estarlo, puede responder "no existe" sin avisar.]
- **Que evidencia respalda la decision:** [El experimento 3 (20 comparaciones contra 1.000.000), los 10 casos de prueba en OK y el experimento 4 (binaria por PM2.5 encontró 0 de 20).]

## 8. Aporte al proyecto

- **Archivo(s) o modulo(s) trabajado(s):** [src/BancoDePruebas.java, src/IngestaSensores.java, docs/ y bitacoras/.]
- **Cambio realizado:** [Con ayuda de un asistente, agregué el método casosDePrueba() en BancoDePruebas (primer elemento, elemento intermedio, último elemento y timestamps inexistentes, en arreglos de 10 y de 1.000.000 de lecturas) y la línea que lo llama desde IngestaSensores. También preparé la traza, las mediciones y mis respuestas de comprensión y pensamiento crítico. El código de búsqueda (BuscadorLecturas, GeneradorDatos) y los experimentos 1 a 4 ya venían hechos en el repositorio.]
- **Como se conecta con la capa anterior:** [Los casos de prueba se ejecutan desde el único main de IngestaSensores, después de la ingesta y del perfil horario de las semanas 1 y 2.]
- **Que queda pendiente para la siguiente semana:** [Estudiar ordenamiento y responder si conviene ordenar los datos antes de buscar.]

## 9. Commits realizados

Registra los commits que muestran tu aporte individual.

| Commit | Mensaje | Que demuestra |
|---|---|---|
| `[hash corto]` | `[mensaje del commit]` | [Cambio realizado] |
| `[hash corto]` | `[mensaje del commit]` | [Cambio realizado] |

## 10. Reexplicacion final

Despues del taller, vuelve a responder la pregunta de la semana en cinco lineas
o menos. Esta respuesta debe ser mas precisa que la de la seccion 4 y debe
incluir la razon de tu decision tecnica.

> [Para encontrar una lectura entre millones conviene usar búsqueda binaria por timestamp, porque los datos están ordenados cronológicamente y cada comparación descarta la mitad de lo que queda: con 1.000.000 de lecturas bastan unas 20 comparaciones, frente a 1.000.000 de la búsqueda lineal. Esta decisión depende de que el orden se cumpla: en PM2.5, donde los datos no están ordenados, la binaria encontró 0 de 20 valores. Por eso la binaria se usa solo donde el orden está garantizado.]

## 11. Reflexion individual

Responde con honestidad:

1. **Lo que ahora puedo hacer y antes no podia:**
   [Ahora puedo ejecutar una búsqueda binaria con casos de prueba (primero, medio, último e inexistente) y leer el número de comparaciones para saber si el algoritmo es correcto y cuánto cuesta.]
2. **El error o supuesto que mas me enseno:**
   [Suponer que la búsqueda binaria encontraría los 20 valores de PM2.5 solo porque es rápida. Me enseñó que un algoritmo rápido solo sirve si se cumplen sus precondiciones.]
3. **La pregunta que llevaria a la proxima clase:**
   [¿Conviene ordenar los datos antes de buscar, y cuánto cuesta ordenarlos?]
4. **Que parte del trabajo fue realmente mia:**
   [Ejecutar, probar y entender el código que ya venía hecho en el repositorio. El código de búsqueda y los experimentos no los escribí yo, y los casos de prueba y los documentos los preparé con ayuda de un asistente que me guió.]

## Lista de verificacion antes de entregar

- [ ] Escribi la prediccion antes de consultar el resultado.
- [ ] Inclui evidencia concreta del laboratorio.
- [ ] Explique un concepto sin depender de jerga.
- [ ] Registre un vacio, una duda o un error real.
- [ ] Trace al menos un caso paso a paso.
- [ ] Justifique una decision del proyecto y una alternativa descartada.
- [ ] Registre mis commits y mi aporte individual.
- [ ] Deje claro que queda pendiente.
- [ ] Renombre el archivo con el formato `sXX-nombre.md`.
