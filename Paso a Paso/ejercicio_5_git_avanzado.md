# Ejercicio 5 – Git Avanzado
## Objetivo
Practicar comandos avanzados: stash, tags, cherry-pick.

## Instrucciones
1. Guarda cambios sin hacer commit:
   ```bash
   git stash
   git stash list
   git stash apply
   ```
2. Crea una etiqueta:
   ```bash
   git tag v1.0
   git push origin --tags
   ```
3. Cherry-pick:
   ```bash
   git cherry-pick <hash-del-commit>
   ```
