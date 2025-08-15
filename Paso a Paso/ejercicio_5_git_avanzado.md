# Ejercicio 5 – Git Avanzado
## Objetivo
Practicar comandos avanzados: stash, tags, cherry-pick.

---

## ¿Qué hacen estos comandos?

- **stash:** Guarda temporalmente tus cambios sin hacer commit, útil si necesitas cambiar de rama pero no quieres perder tu trabajo.
- **tags:** Permiten marcar versiones importantes del proyecto, como lanzamientos o entregas.
- **cherry-pick:** Copia un cambio específico (commit) de una rama a otra, útil si solo quieres traer un cambio y no todos.

---

## Instrucciones paso a paso

### 1. **Guarda cambios sin hacer commit**
Si tienes cambios y necesitas cambiar de rama, puedes guardarlos temporalmente.

```bash
git stash                # Guarda los cambios sin hacer commit
git stash list           # Muestra la lista de cambios guardados
git stash apply          # Recupera los cambios guardados
```


### 2. **Crea una etiqueta (tag)**
Marca una versión importante del proyecto.


```bash
git tag v1.0             # Crea una etiqueta llamada v1.0
git push origin --tags   # Sube las etiquetas al repositorio remoto
```


### 3. **Cherry-pick**
Trae un commit específico de otra rama usando su identificador (hash).

```bash
git cherry-pick <hash-del-commit>   # Aplica el commit indicado en tu rama actual
```
- Para obtener el hash, usa `git log --oneline`.

---

## 📝 Notas para principiantes

- **¿Cuándo usar stash?** Cuando necesitas cambiar de rama y no quieres perder cambios no guardados.
- **¿Por qué usar tags?** Para identificar versiones estables o entregas.
- **¿Qué es cherry-pick?** Es útil para traer solo un cambio específico, no toda una rama.

---

**¡Con estos comandos puedes manejar situaciones más avanzadas en tus proyectos con Git!**
