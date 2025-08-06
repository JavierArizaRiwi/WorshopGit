
## 🧪 2. Ejercicios Prácticos

---

### Ejercicio 1: Inicialización de repositorio

```bash
mkdir proyecto-git && cd proyecto-git
git init
echo "# Proyecto Git" > README.md
git add README.md
git commit -m "Primer commit"
```

---

### Ejercicio 2: Conectar a un repositorio remoto

1. Crea un nuevo repositorio en GitHub.
2. Ejecuta:

```bash
git remote add origin https://github.com/usuario/proyecto.git
git branch -M main
git push -u origin main
```

---

### Ejercicio 3: Crear una rama y trabajar en ella

```bash
git checkout -b feature/formulario
# Edita código
git add .
git commit -m "Agrega formulario de contacto"
git push origin feature/formulario
```

Luego:

- Crea un **Pull Request** en GitHub.
- Otro coder lo revisa y aprueba.
- Se hace **merge** y se elimina la rama.

---

### Ejercicio 4: Resolver conflictos

1. Coder A y Coder B modifican la misma línea de `README.md`.
2. Ambos hacen commit en ramas diferentes.
3. Uno hace merge:

```bash
git checkout main
git merge feature/coder-a
```

4. Git detecta conflicto. Se resuelve manualmente editando el archivo, luego:

```bash
git add README.md
git commit -m "Resuelve conflicto de README"
```

---

## Recomendaciones

-  Haz `git pull` antes de comenzar a trabajar.
-  Crea ramas por cada funcionalidad.
-  Haz commits descriptivos y frecuentes.
-  Usa Pull Requests para mantener calidad de código.
-  Elimina ramas locales y remotas cuando ya no se usen.
