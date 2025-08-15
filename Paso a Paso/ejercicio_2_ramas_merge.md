# Ejercicio 2 – Trabajando con ramas
## Objetivo
Crear y fusionar ramas, resolver conflictos.

## Instrucciones
1. Crea una rama:
   ```bash
   git checkout -b desarrollo
   echo "Linea nueva" >> README.md
   git add . && git commit -m "Cambios en desarrollo"
   ```
2. Vuelve a main y haz merge:
   ```bash
   git checkout main
   git merge desarrollo
   ```
3. Crea conflicto editando misma línea en ambas ramas y repite el proceso.
