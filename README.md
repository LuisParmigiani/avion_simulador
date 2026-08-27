# avion_simulador

Modelo de simulación en **AnyLogic** del amaraje de emergencia (*ditching*) de un Boeing 737-801.

El modelo vive en `anylogic/DitchingBoeing737-801/`:

- `DitchingBoeing737-801.alp` — el modelo principal de AnyLogic.
- `3d/` — recursos 3D (sillas, personas, valijas).
- `cabina.png`, `image1.png` — imágenes usadas en el modelo.

## Cómo trabajar en equipo sin romper el modelo

El archivo `.alp` es un **único archivo** que contiene todo el modelo. Git **no puede fusionarlo
automáticamente** si dos personas lo editan a la vez, así que hay que coordinar para no pisarse:

1. **Antes de empezar a editar, hacé `git pull`.** Así arrancás siempre desde la última versión que
   subió el equipo.
2. **No editen el mismo `.alp` en paralelo.** Coordinen (por chat/grupo) quién lo está tocando en
   cada momento. Idealmente, una persona por vez.
3. **Cuando termines, cerrá AnyLogic, commiteá y pusheá enseguida** (`git add`, `git commit`,
   `git push`). Cuanto menos tiempo tengas cambios sin subir, menos chance de conflicto.
4. **Avisale al equipo** cuando terminaste de editar, para que el próximo pueda hacer su `pull` y
   arrancar tranquilo.

Si igual se genera un conflicto en el `.alp` (Git lo marca como binario y no lo puede unir), **no lo
edites a mano**: hablen entre ustedes para decidir qué versión queda y esa persona vuelve a subir el
modelo completo.

> Los archivos `.DS_Store` de macOS están ignorados en `.gitignore` — no hace falta que los toquen.
