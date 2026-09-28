# Mediciones — Semana 3

Resultados obtenidos al ejecutar IngestaSensores en mi computador.

| Tamaño | Lineal (comparaciones) | Binaria (comparaciones) | Tiempo lineal (ms) | Tiempo binaria (ms) |
|---:|---:|---:|---:|---:|
| 1.000 | 1.000 | 10 | 0,731 | no medido |
| 100.000 | 100.000 | 17 | 6,836 | no medido |
| 1.000.000 | 1.000.000 | 20 | 21,332 | no medido |

Notas:
- Las comparaciones y el tiempo lineal vienen de los experimentos 1 y 3.
- El experimento 3 no mide el tiempo de la búsqueda binaria, por eso esa columna queda sin dato.
- Los tiempos cambian en cada ejecución (en otra corrida el lineal con 1.000.000 dio 13,835 ms).