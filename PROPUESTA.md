# Tesoro de los Números: propuesta del juego

Juego de matemáticas para niños (unos 7 a 9 años) con temática pirata. El jugador navega por un mapa con 4 islas. Cada isla trabaja una operación y tiene 5 retos, 20 en total. Al terminar cada isla se gana un trozo del mapa, y con los 4 trozos se abre el cofre del tesoro.

## 1. Estructura

| Orden | Isla | Operación | Decoración en el mapa |
|---|---|---|---|
| 1 | Isla del Coco | Suma (+) | Palmeras |
| 2 | Isla Calavera | Resta (−) | Roca con forma de calavera |
| 3 | Isla de los Loros | Multiplicación (×) | Palmeras |
| 4 | Isla del Volcán | División (÷) | Volcán |
| Final | El tesoro (X) | — | Cofre que se abre |

- Las islas se desbloquean en orden. La siguiente isla tiene un anillo punteado que gira y el barco navega hasta ella.
- Una isla terminada muestra una bandera y su mejor puntaje. Se puede volver a jugar y se guarda el mejor resultado.

## 2. Los retos (dificultad creciente dentro de cada isla)

Cada isla tiene 5 niveles. Cada nivel tiene entre 3 y 4 historias distintas y números al azar.

| Nivel | Suma | Resta | Multiplicación | División (exacta) |
|---|---|---|---|---|
| 1 | 2–6 + 2–6 | 6–10 − 1–5 | 2–5 × 2–5 | entre 2–3, cociente 2–5 |
| 2 | 6–12 + 3–8 | 12–20 − 3–9 | tablas del 2 y del 3 | entre 2–5, cociente 2–6 |
| 3 | 2 cifras sin llevar | 2 cifras sin prestar | 3–6 × 4–8 | agrupar: "¿cuántas cajas?" |
| 4 | 2 cifras llevando | 2 cifras prestando (comparar) | tablas del 5, 7 y 8 | entre 4–8, cociente 4–8 |
| 5 | tres sumandos | hasta 99 | 6–9 × 6–9 | entre 6–9, cociente 5–9 |

Cada reto muestra la historia y debajo la operación con un espacio para la respuesta: `7 + 5 = ?`.

## 3. Variedad: que los retos no se repitan

1. **Historias**: por cada nivel se elige una historia que el jugador todavía no ha visto. Las historias vistas se guardan en el navegador (`localStorage`). Cuando ya se vieron todas las de un nivel, esa lista se reinicia, pero sin repetir la última que salió.
2. **Números**: cada vez se generan números nuevos. Dentro de una misma partida no se repite la misma operación (por ejemplo `4 × 6` dos veces). Si sale repetida, se vuelve a generar (hasta 20 intentos).
3. Volver a jugar una isla da historias y números diferentes.

## 4. Cómo se juega un reto

- Teclado en pantalla con botones de madera (0–9, Borrar, "¡Fuego! Comprobar"). También funciona con el teclado físico (números, Retroceso, Enter).
- **Acierto al primer intento sin ayuda**: 2 doblones. **Acierto con ayuda o en el segundo o tercer intento**: 1 doblón.
- **Error**: el mensaje dice si el número es muy grande o muy pequeño. Al segundo error aparece la ayuda del loro sola.
- **Tercer error**: se muestra la respuesta correcta con la ayuda, se ganan 0 doblones y se pasa al siguiente reto (para que el niño no se frustre).
- **Ayuda del loro** (botón):
  - Suma: grupos de monedas para contar (si el total es 40 o menos); si no, sumar decenas y luego unidades.
  - Resta: monedas tachadas (hasta 40); si no, restar decenas y luego unidades.
  - Multiplicación: filas de monedas y la suma repetida.
  - División: "¿qué número por b da n?" y filas de b monedas para contar.
- Máximo de puntos: 10 por isla, 40 en total.

## 5. Final

Cofre animado que se abre, lluvia de monedas, total de doblones y un rango:

| Doblones | Rango |
|---|---|
| 36–40 | Leyenda de los siete mares |
| 28–35 | Navegante experto |
| 18–27 | Pirata valiente |
| 0–17 | Grumete en entrenamiento |

El botón "Nueva aventura" borra el progreso.

## 6. Diseño visual

- Fondo de mar nocturno y un mapa de pergamino con islas, olas, rosa de los vientos y una ruta punteada roja.
- Tipografías: **Pirata One** para títulos y nombres de islas, y **Andika** para el texto. Andika está hecha para niños que están aprendiendo a leer.
- Sonidos cortos generados con Web Audio y un botón para silenciarlos.
- Funciona en celular (unos 400 px de ancho), tablet y computadora. Respeta `prefers-reduced-motion`.

## 7. Técnica

- Un solo archivo: `tesoro-de-los-numeros.html` (HTML, CSS y JS, sin librerías). Se publica como Artifact de claude.ai.
- El progreso (`scores`) y las historias vistas (`seen`) se guardan en `localStorage` con try/catch. Si el navegador no deja guardar, el juego funciona igual.

## 8. Estado y tareas pendientes

**Ya hecho (Opus):** mapa, islas, barco, pantallas de isla, modal y final, teclado, ayudas, sonidos, puntaje, guardado de progreso, y el banco de historias por nivel (`ISLANDS[i].levels`, 5 niveles con 3–4 variantes cada uno).

**Para la ejecución (Sonnet):**
1. Conectar `startIsland()` con `levels`. Ahora llama a `isl.gens`, que ya no existe, y por eso el juego está roto.
2. Implementar la regla de no repetir de la sección 3 (historias vistas en `localStorage` y números sin repetir en la partida).
3. Probar el juego completo en el navegador: las 4 islas, un error, la ayuda, el tercer error, el final y "Nueva aventura". Probar también en ancho de celular. Corregir los errores que aparezcan.
4. Revisar que todas las historias tengan sentido con sus números (por ejemplo, que ninguna resta dé negativo y que las divisiones sean exactas).

## 9. Criterios de aceptación

- No hay errores en la consola y se puede jugar de principio a fin.
- En 3 partidas seguidas de la misma isla, no se repite la historia de ningún nivel mientras queden historias sin ver.
- Todas las respuestas son enteros positivos.
- En 375 px de ancho no hay scroll horizontal y el teclado se puede usar con el dedo.
