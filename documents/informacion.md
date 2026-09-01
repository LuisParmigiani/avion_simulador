Documento de trabajo — TPI Simulación 2026
(COM4K02)
Escenario elegido: Evacuación de aeronave por amerizaje (ditching) — Simulación Basada en
Agentes
Versión actualizada — modelo narrowbody (Boeing 737-800)
Conti Stéfano · Dana Agustín · Vitali Bruno · Parmigiani Luis

1. Resumen del escenario y avión de referencia definitivo

El equipo evaluó dos alternativas de avión para el escenario de evacuación por amerizaje: un widebody
(Airbus A330-300) y un narrowbody (Boeing 737-800). Tras encontrar un caso real de amerizaje
comercial extensamente documentado —el vuelo 1549 de US Airways, un Airbus A320, misma
categoría que el 737-800— se decidió avanzar con el Boeing 737-800 como avión de referencia
definitivo.

Por qué 737-800 y no widebody

La razón principal no es de facilidad de modelado sino de calidad de validación: existe un caso real
de amerizaje exitoso, con informe oficial de investigación de accidentes (NTSB), en la misma categoría
de avión (single-aisle). Esto permite comparar los resultados del modelo contra un evento real de
ditching —no solo contra una demostración de certificación en tierra o un modelo de otro autor— lo cual
fortalece mucho la sección de validación del TPI. Además, la reducción de complejidad (un solo pasillo
en vez de doble pasillo con cross-aisles) acorta el tiempo de construcción del modelo, algo relevante
dado el plazo del TPI.

Caso real de referencia: US Airways 1549 (“Miracle on the Hudson”)

El 15 de enero de 2009, el vuelo 1549 de US Airways (Airbus A320-214) amerizó en el río Hudson, a
8.5 millas del aeropuerto LaGuardia, tras perder empuje en ambos motores por impacto con una
bandada de aves. Los 150 pasajeros y 5 tripulantes evacuaron el avión por las salidas delanteras y
sobre el ala. Los 155 ocupantes sobrevivieron y fueron retirados del avión y del agua 24 minutos
después del amerizaje. El NTSB publicó un informe completo de investigación (NTSB/AAR-10/03) con
factores de supervivencia y secuencia de evacuación, además de testimonios de la tripulación ante el
Congreso de EE.UU.

Nota: la aeronave del caso real es un A320, no un 737-800, pero ambos son single-aisle de capacidad
y configuración de salidas equivalente (misma categoría de certificación), por lo que el caso sigue
siendo un ancla de validación razonable en orden de magnitud y dinámica de evacuación.

Configuración de referencia del 737-800

Cabina de un solo pasillo (single-aisle). Configuración típica de salidas: 2 pares de puertas
delanteras/traseras tipo I, más 2 pares de salidas tipo III sobre el ala — 4 pares en total (8 salidas).
Esta es la base sobre la que se definen los 4-6 escenarios de disponibilidad de salidas del Eje 1 de la
propuesta original.

2. Marco regulatorio (base del problema)

La norma central es 14 CFR 25.803(c): exige mostrar que la capacidad máxima de asientos puede
evacuarse a tierra en condiciones simuladas de emergencia dentro de 90 segundos. El detalle de cómo
se testea esto está en el Appendix J de la Part 25: se conduce de noche o simulando oscuridad,
usando solo el sistema de iluminación de emergencia y solo las salidas de un lado del fuselaje (esto
justifica el supuesto de “50% de salidas disponibles” del proyecto).

Ángulo crítico para el “problema” de la propuesta: reportes de la OIG (Departamento de Transporte de
EE.UU.) cuestionan si los supuestos de la norma siguen siendo realistas, dado que factores como
comportamiento de pasajeros, dimensiones de asientos, equipaje de mano y humo en cabina
cambiaron con los años sin que la norma se actualice en la misma medida. El caso Hudson es un buen
contrapunto real: fue una evacuación exitosa fuera del marco de un ensayo de certificación, lo cual da
una segunda capa de justificación al “problema”: ¿el modelo de certificación predice bien lo que pasa
en un evento real?

3. Fuentes de información y para qué sirve cada una

14 CFR 25.803 — Emergency evacuation (eCFR)
https://www.ecfr.gov/current/title-14/chapter-I/subchapter-C/part-25/subpart-D/subject-group-ECFR88992669bab3b

52/section-25.803

Texto legal completo de la regla de los 90 segundos. Fuente primaria para la sección “Problema” de la
propuesta.

AC 25.803-1A — Emergency Evacuation Demonstrations (FAA)
https://www.faa.gov/documentLibrary/media/Advisory_Circular/AC_25.803-1A.pdf

Detalle de cómo se conducen las demostraciones reales de evacuación (condiciones de luz, salidas
usadas, etc.). Útil para definir los supuestos exactos del “piso realista” del modelo.

“Gone in 90 seconds?” — Royal Aeronautical Society
https://www.aerosociety.com/news/gone-in-90-seconds/

Análisis crítico de si la regla de 90s sigue siendo realista hoy. Mejor fuente para justificar el “problema”
del TPI y para argumentar por qué el bloqueo del mismo lado/salidas centrales es el peor caso
geométrico.

NTSB Aircraft Accident Report AAR-10/03 — US Airways Flight 1549 (Hudson River)
https://www.ntsb.gov/investigations/AccidentReports/Reports/AAR1003.pdf

FUENTE DE VALIDACIÓN PRINCIPAL. Único caso real y bien documentado de amerizaje comercial
con evacuación exitosa. Da un punto de comparación real (no solo de certificación en tierra ni de otro
modelo de simulación) para contrastar los resultados del modelo propio: qué salidas se usaron, cuánto
tardó la evacuación completa, y qué factores de supervivencia identificó el NTSB.

Emergency evacuation simulation of commercial aircraft (Springer — modelo PATHFINDER)
https://link.springer.com/article/10.1007/s42452-021-04295-z

FUENTE PRINCIPAL DE DATOS. Es un modelo de avión single-aisle, igual que el 737-800, por lo que
ahora sí aplica de forma directa. Aporta los parámetros de agente a usar: velocidad de caminata,
dimensiones corporales, comportamiento de conflicto entre pasajeros, tiempo de respuesta a colisiones
y tiempo de aceleración, y cómo cada uno afecta el tiempo de evacuación.

Evaluating personnel evacuation risks under fire scenario of Airbus wide-body aircraft
(PMC)
https://pmc.ncbi.nlm.nih.gov/articles/PMC9493476/

GUÍA DE MÉTODO (secundaria). Es un modelo de avión widebody de doble pasillo, por lo que su
geometría ya no matchea con el 737-800. Igual sirve como referencia de método: las fórmulas de
velocidad de caminata por edad/género y el ajuste por cabina inclinada son un buen punto de partida
conceptual, aunque conviene priorizar los valores del paper de PATHFINDER (single-aisle) para
calibrar el modelo final.

An Aircraft Evacuation Simulation Baseline Using DES (tesis, modelo A380 en ARENA)
https://commons.erau.edu/edt/207/

Referencia de validación secundaria/complementaria. El modelo fue validado contra una evacuación
real de certificación del A380 (78.2 segundos). Sirve como segundo punto de comparación de orden de
magnitud, aunque el caso Hudson (arriba) es la referencia principal por ser de la misma categoría de
avión y un evento real, no una demostración de certificación.

4. Cómo vamos a trabajar — pasos de construcción en AnyLogic

Los pasos están mapeados a la metodología de 7 etapas indicada por la cátedra: definición del
problema, formulación del modelo, construcción, verificación, validación, diseño de experimentos y
análisis de resultados.

l 1. Definir alcance y confirmar el avión de referencia

Boeing 737-800, single-aisle, un solo pasillo central. Configuración de referencia: 4 pares de salidas (2
tipo I delanteras/traseras + 2 tipo III sobre el ala) — 8 salidas totales. Esto define todo lo que sigue.

l 2. Conseguir y digitalizar el plano de cabina

Bajar el documento “Boeing 737-800 Airport Planning” (público, en el sitio de Boeing), que trae el layout
a escala con distancias de pasillo, pitch de asientos y ubicación de salidas. Usarlo como imagen de
fondo en el editor de AnyLogic para calcar paredes, obstáculos y salidas con medidas reales.

l 3. Levantar el entorno con Space Markup Library

Wall para fuselaje, mamparos y filas de asientos como obstáculos; un único Node/Path para el pasillo
central; Target Line o Service Point en cada una de las 8 salidas.

l 4. Construir el flujo de agentes con Pedestrian Library

PedSource para generar pasajeros en sus asientos, bloque de decisión para elegir salida (más cercana
o disponible), PedGoTo para el movimiento hacia la salida, PedSink al llegar. La velocidad de cada
agente se parametriza con los valores del paper de PATHFINDER (Springer), no con el default de la
librería.

l 5. Modelar los atributos de agente (población heterogénea)

Clase Passenger con edad/movilidad (afecta velocidad y tiempo de reacción), equipaje de mano
(retraso), condición de PMR. Distribuciones (uniform, triangular) basadas en la literatura relevada.

l 6. Implementar el Eje 1 — disponibilidad de salidas por escenario

Parámetro booleano por salida, activado/desactivado según el escenario (todas abiertas, 50%
bloqueado alternado, 50% bloqueado peor caso geométrico —mismo lado/salidas centrales—, bloqueo
asimétrico de un lado completo). Los agentes solo consideran salidas activas al elegir ruta.

l 7. Implementar el Eje 2 — condiciones de piso fijas

Obstáculo en el pasillo, iluminación reducida, sin aviso previo, menor cantidad de tripulantes-guía.
Estas condiciones van fijas en TODAS las corridas, no varían entre escenarios.

l 8. Instrumentar la medición del tiempo de evacuación

TimeMeasureStart al inicio de la simulación, TimeMeasureEnd en cada PedSink, dataset que registre
cuándo sale el último pasajero (tiempo total de evacuación). Contadores por salida para identificar
cuellos de botella.

l 9. Verificación

Correr con pocos agentes y revisar visualmente que eligen salida y se mueven correctamente;
chequear que los contadores sumen el total de pasajeros sin pérdidas; probar casos extremos (todas
las salidas bloqueadas menos una).

l 10. Validación

Comparar el baseline del modelo (todas las salidas abiertas, sin piso realista) contra el caso real del
Hudson (orden de magnitud del tiempo de evacuación total, uso de salidas delanteras y sobre el ala) y,
como referencia secundaria, contra el modelo A380 validado en 78.2 segundos. Si el modelo da
tiempos y tendencias razonables frente a ambos, está validado apropiadamente para un TPI de grado.

l 11. Diseño de experimentos y corridas

Parameter Variation o Multi-run en AnyLogic, mínimo 30-50 corridas por escenario (hay estocasticidad
en velocidades y decisiones). Exportar resultados a CSV/Excel.

l 12. Análisis de resultados

Tiempo medio y desvío estándar por escenario, comparación contra el umbral de 90 segundos,
identificación de cuellos de botella recurrentes, gráfico de sensibilidad (tiempo de evacuación vs. % de
salidas bloqueadas).

5. Notas prácticas

(cid:127) Empezar simple: primero el baseline (todas las salidas abiertas, sin piso realista) verificado y

funcionando, antes de sumar los demás escenarios y las condiciones fijas.

La licencia educativa/PLE de AnyLogic alcanza para este proyecto; no hace falta la versión
Professional salvo que se necesiten escalators o densidades extremas.

(cid:127) El libro “AnyLogic in Three Days” tiene un capítulo de Pedestrian Library con un ejemplo de evacuación

de edificio: la lógica PedSource ﬁ decisión ﬁ PedGoTo ﬁ PedSink es la misma que se va a reusar
acá, aunque no sea un ejemplo de avión.

(cid:127) Para el eje del “peor caso geométrico”, el artículo del Royal Aeronautical Society es la mejor fuente

teórica para justificar por qué ese caso es más grave que el bloqueo alternado.

(cid:127) Al citar el caso Hudson en el informe final, aclarar que la aeronave real fue un A320 (misma

categoría/single-aisle que el 737-800 elegido), no el mismo modelo exacto — es una validación de
orden de magnitud y dinámica, no una réplica exacta.

Documento de trabajo interno — TPI Simulación 2026, COM4K02 — no es la propuesta final a entregar a la cátedra.

(cid:127)

