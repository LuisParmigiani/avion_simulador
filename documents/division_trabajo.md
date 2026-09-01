División de trabajo — TPI Simulación 2026
(COM4K02)
Evacuación de aeronave por amerizaje (ditching) — Boeing 737-800
Integrante 1 · Integrante 2 · Integrante 3 · Integrante 4

Criterio de división

El trabajo se dividió en 4 líneas lo más independientes posible, para que cada persona tenga avance
propio y verificable sin depender de que otro termine antes. Tres de las cuatro líneas (entorno, agentes,
investigación/documentación) se pueden desarrollar en paralelo desde el día 1. La cuarta línea (lógica
de flujo y escenarios) tiene una dependencia real de las otras dos —necesita el entorno de Integrante 1
y la clase de agente de Integrante 2 para integrarse al modelo final—, así que a Integrante 3 se le
asigna trabajar con un modelo de prueba simplificado (un pasillo genérico con dos salidas y una
clase de agente placeholder) para poder avanzar y probar su lógica sin esperar a nadie. La integración
de las 3 partes en el modelo final es el único momento que requiere trabajo conjunto explícito (ver
“Fase de integración” al final).

Integrante 1
Línea A — Entorno y geometría de la cabina · Trabajo independiente desde el día 1.

(cid:127) Conseguir el plano de cabina: Bajar el documento “Boeing 737-800 Airport Planning” (público, sitio
de Boeing) con el layout a escala: distancias de pasillo, pitch de asientos, ubicación de las 8 salidas (4
pares: 2 tipo I + 2 tipo III sobre el ala).

(cid:127) Digitalizar el layout en AnyLogic: Usar el plano como imagen de fondo en el editor y calcar con
Space Markup Library: Wall para fuselaje, mamparos y filas de asientos como obstáculos; Node/Path
para el pasillo central.

(cid:127) Marcar las salidas: Target Line o Service Point en cada una de las 8 salidas, con nombre/ID único
para que después Integrante 3 las pueda referenciar desde la lógica de decisión.

(cid:127) Modelar el obstáculo de pasillo (Eje 2, parte física): Agregar el obstáculo fijo en el pasillo que
representa la condición de “piso realista” (equipaje, elemento bloqueando el paso).

Entregable con progreso visible

Un modelo AnyLogic con la cabina completa digitalizada, las 8 salidas identificadas y nombradas, y el
obstáculo de pasillo colocado. Se puede probar de forma standalone soltando unos pocos agentes
genéricos y viendo que caminan y salen sin errores de geometría — esto es progreso visible sin
depender de nadie más.

Fuentes que le corresponden

Boeing 737-800 Airport Planning (plano oficial). No necesita las fuentes académicas de
comportamiento.

Integrante 2
Línea B — Población de agentes y comportamiento · Trabajo independiente desde el día 1.

(cid:127) Definir la clase Passenger: Atributos: edad/movilidad, si lleva equipaje de mano, si es PMR (persona
con movilidad reducida).

(cid:127) Calibrar velocidades por edad y género: Usar los valores/fórmulas del paper de PATHFINDER
(Springer, single-aisle) para asignar velocidad de caminata realista según el perfil del agente, en vez
del default de la Pedestrian Library.

(cid:127) Modelar retrasos de comportamiento: Tiempo extra por recuperar equipaje de mano, tiempo de
reacción/aceleración inicial, comportamiento de conflicto al cruzarse con otro pasajero — todos
parámetros que el paper de PATHFINDER cuantifica.

(cid:127) Definir las distribuciones de población: Uniform/triangular para asignar edad, movilidad y equipaje
al crear cada agente, de forma que el mix represente un vuelo realista.

Entregable con progreso visible

Una clase Passenger completa y probada en un modelo de prueba simple (por ejemplo, un pasillo recto
con agentes caminando), mostrando que las velocidades y comportamientos calibrados dan resultados
razonables comparados con los valores del paper. Esto es progreso 100% independiente y verificable
sin la cabina final ni la lógica de decisión de Integrante 3.

Fuentes que le corresponden

Emergency evacuation simulation of commercial aircraft (Springer/PATHFINDER) como fuente principal
de datos.

Integrante 3
Línea C — Lógica de flujo y escenarios (Ejes 1 y 2) · Depende parcialmente de otras líneas — ver nota
de integración.

(cid:127) Construir el flujo base de Pedestrian Library: PedSource ﬁ bloque de decisión de salida ﬁ
PedGoTo ﬁ PedSink. Empezar en un modelo de prueba simplificado (pasillo genérico con 2 salidas y
una clase Passenger placeholder), para no depender de que Integrante 1 y Integrante 2 terminen.

(cid:127) Programar la lógica de selección de salida: Que cada agente elija la salida activa más cercana o
disponible, referenciando el ID de salida que va a definir Integrante 1.

(cid:127) Implementar el Eje 1 (disponibilidad de salidas): Parámetro booleano por salida,
activado/desactivado según el escenario: todas abiertas, 50% bloqueado alternado, 50% bloqueado
peor caso (mismo lado/salidas centrales), bloqueo asimétrico de un lado completo.

(cid:127) Implementar el Eje 2 (condiciones fijas restantes): Reducción de iluminación/visibilidad, ausencia
de aviso previo, menor cantidad de tripulantes-guía — estas se aplican igual en todas las corridas.

(cid:127) Integrar con el entorno y los agentes reales: Una vez que Integrante 1 y Integrante 2 entreguen
sus partes, reemplazar el pasillo/clase placeholder por la cabina real y la clase Passenger final. Esta
etapa es la que requiere coordinación directa con ambos.

Entregable con progreso visible

Un modelo de prueba funcional (flujo de decisión + Ejes 1 y 2) corriendo sobre un entorno simplificado,
que se pueda mostrar como avance aunque la cabina final no esté lista. La integración final sí depende
de las líneas A y B.

Fuentes que le corresponden

Ninguna fuente académica propia; usa las salidas del trabajo de Integrante 1 (IDs de salida) y de
Integrante 2 (clase Passenger) en la etapa de integración.

Integrante 4
Línea D — Marco regulatorio, instrumentación, validación y resultados · Trabajo independiente desde el
día 1.

(cid:127) Redactar el marco regulatorio y el “problema”: Con base en 14 CFR 25.803, el Appendix J, la
Advisory Circular 25.803-1A y el artículo del Royal Aeronautical Society: por qué existe la regla de 90
segundos, qué exige, y por qué se cuestiona su realismo actual.

(cid:127) Documentar el caso de validación (Hudson River): Resumir el informe NTSB AAR-10/03 del vuelo
1549: secuencia de evacuación, salidas usadas, tiempo total, factores de supervivencia. Aclarar que la
aeronave real es un A320 pero de la misma categoría que el 737-800.

(cid:127) Diseñar la instrumentación de medición: Especificar de antemano qué bloques van a usarse
(TimeMeasureStart/End, datasets, contadores por salida) para que, apenas el modelo esté integrado,
se puedan insertar sin rediseñar nada.

(cid:127) Verificación y validación: Una vez integrado el modelo (líneas A+B+C), correr las pruebas de
verificación (casos extremos, chequeo de conservación de agentes) y comparar el baseline contra el
caso Hudson y el modelo A380 de referencia.

(cid:127) Diseño de experimentos y análisis de resultados: Parameter Variation / Multi-run (30-50 corridas
por escenario), exportación a CSV/Excel, cálculo de medias y desvíos, gráfico de sensibilidad frente al
umbral de 90 segundos.

Entregable con progreso visible

Un documento de marco regulatorio + caso de validación completamente redactado desde el día 1 (no
depende de nadie), más una especificación lista de la instrumentación a insertar. La verificación,
validación y experimentos sí dependen del modelo integrado, así que esa etapa se hace en conjunto
con el resto del equipo al final.

Fuentes que le corresponden

14 CFR 25.803, AC 25.803-1A, Royal Aeronautical Society, NTSB AAR-10/03 (Hudson), tesis
A380/ARENA como validación secundaria.

Fase de integración (trabajo conjunto)

Esta es la única etapa que no se puede paralelizar del todo. Requiere que Integrante 1, Integrante 2 y
Integrante 3 se sienten juntos (presencial o por videollamada compartiendo pantalla) para: reemplazar
el entorno y la clase de agente placeholder de Integrante 3 por los definitivos de Integrante 1 y
Integrante 2, y verificar que el flujo de decisión de salidas funciona sobre la cabina real. Una vez
integrado, Integrante 4 se suma para instrumentar la medición, correr la verificación/validación y
diseñar los experimentos — en esta etapa final lo más eficiente es que los 4 estén disponibles para
resolver bugs de integración rápido, aunque no hace falta que los 4 estén todo el tiempo frente a la
pantalla.

Cronograma sugerido

Fase

Quién

Qué se hace

1. Trabajo en
paralelo

2. Integración

Integrante 1,
Integrante 2,
Integrante 4 en
paralelo. Integrante 3
arranca con modelo
de prueba.

Integrante 1 +
Integrante 2 +
Integrante 3

3. Cierre técnico

Integrante 4 (con
apoyo del resto)

Entorno digitalizado, clase Passenger
calibrada, marco regulatorio redactado,
lógica de flujo probada en entorno
simplificado.

Modo

Independien
te

Ensamblar entorno real + clase de agente
real + lógica de flujo en un solo modelo.

Conjunto

Instrumentación, verificación, validación
contra Hudson/A380, diseño de
experimentos y corridas, análisis de
resultados.

Conjunto /
liderado

Documento de trabajo interno — TPI Simulación 2026, COM4K02 — división de tareas para el equipo, no forma parte de la

propuesta a entregar a la cátedra.


