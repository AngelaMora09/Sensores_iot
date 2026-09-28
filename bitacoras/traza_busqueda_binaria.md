# Traza de la búsqueda binaria — límite incorrecto

Razonamiento a mano sobre qué ocurriría si el ciclo usara `inicio = medio` en lugar de `inicio = medio + 1`. El código final del proyecto usa la versión correcta.

Arreglo: `[0, 1, 2, 3]`. Objetivo: `3`.
Fórmula del medio: `medio = (inicio + fin) / 2`, con división entera.

| Paso | inicio | fin | medio | valor medio | comparación | acción |
|---:|---:|---:|---:|---:|---|---|
| 1 | 0 | 3 | 1 | 1 | 1 < 3 | inicio = medio = 1 |
| 2 | 1 | 3 | 2 | 2 | 2 < 3 | inicio = medio = 2 |
| 3 | 2 | 3 | 2 | 2 | 2 < 3 | inicio = medio = 2 (no cambia) |
| 4 | 2 | 3 | 2 | 2 | 2 < 3 | igual que el paso 3: se repite sin terminar |

## Conclusión

En el paso 3, `(2 + 3) / 2 = 2` porque se descarta el decimal, así que `medio` cae en la misma posición que `inicio`. Al hacer `inicio = medio`, `inicio` no avanza, y `inicio`, `fin` y `medio` quedan iguales en cada vuelta. El ciclo `while (inicio <= fin)` nunca termina.

Con la regla correcta (`inicio = medio + 1`), en el paso 3 `inicio` pasaría a 3, `medio` sería 3 y encontraría el valor en la posición 3. Se suma 1 porque `medio` ya fue comparado y se puede descartar.