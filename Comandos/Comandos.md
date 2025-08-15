# 🚀 Git Workshop – De Básico a Avanzado

Este documento está diseñado para ayudarte a comprender y practicar Git desde cero, ideal para coders que se están adentrando en el mundo del desarrollo colaborativo.

---

## 📚 1. Comandos Esenciales de Git

### 🔹 `git init`
Inicializa un nuevo repositorio Git en el directorio actual.  
**Úsalo cuando quieras empezar a usar Git en un proyecto que aún no lo tiene.**

```bash
git init
```


### 🔹 `git clone <url>`
Clona un repositorio remoto a tu máquina local.  
**Sirve para obtener una copia de un proyecto existente desde GitHub u otro servidor.**

```bash
git clone https://github.com/usuario/proyecto.git
```

### 🔹 `git status`
Muestra el estado actual del repositorio.  
**Te dice qué archivos han cambiado, cuáles están listos para guardar y cuáles no.**

```bash
git status
```

### 🔹 `git add <archivo>` / `git add .`
Agrega cambios al área de preparación (staging).  
**Prepara los archivos para ser guardados en el historial. Usa `git add .` para agregar todos los cambios.**

```bash
git add index.html
git add .
```

### 🔹 `git commit -m "mensaje"`
Registra los cambios en el historial local.  
**Guarda los cambios preparados con un mensaje que explique qué hiciste.**

```bash
git commit -m "Agrega componente de login"
```

### 🔹 `git push`
Envía los cambios locales al repositorio remoto.  
**Sube tus cambios a GitHub u otro servidor para compartirlos con tu equipo.**

```bash
git push origin main
```

### 🔹 `git pull`
Descarga y fusiona los cambios del repositorio remoto.  
**Actualiza tu copia local con los cambios que otros hayan subido.**

```bash
git pull origin main
```

### 🔹 `git checkout -b <rama>`
Crea y cambia a una nueva rama.  
**Las ramas te permiten trabajar en nuevas funciones sin afectar el código principal.**

```bash
git checkout -b feature/navbar
```

### 🔹 `git merge <rama>`
Fusiona la rama indicada con la actual.  
**Combina los cambios de otra rama con la rama en la que estás trabajando.**

```bash
git merge feature/navbar
```

### 🔹 `git branch -d <rama>`
Elimina una rama local.  
**Útil para limpiar ramas que ya no necesitas después de fusionarlas.**

```bash
git branch -d feature/navbar
```

### 🔹 `git log --oneline`
Muestra el historial de commits de forma compacta.  
**Te permite ver rápidamente los cambios realizados en el proyecto.**

```bash
git log --oneline
```

---

## 🛠️ Comandos Útiles Adicionales

### 🔹 `git diff`
Muestra las diferencias entre archivos modificados y la última versión guardada.  
**Útil para ver exactamente qué cambió antes de guardar o subir tus cambios.**

```bash
git diff
```

### 🔹 `git stash`
Guarda temporalmente los cambios que no quieres comprometer aún.  
**Ideal si necesitas cambiar de rama pero no quieres perder tu trabajo actual.**

```bash
git stash
```

### 🔹 `git remote -v`
Muestra las direcciones de los repositorios remotos asociados.  
**Sirve para verificar a dónde se suben o descargan los cambios.**

```bash
git remote -v
```

### 🔹 `git reset <archivo>`
Quita archivos del área de preparación (staging).  
**Si agregaste un archivo por error, puedes quitarlo antes de hacer el commit.**

```bash
git reset index.html
```

---

> **Consejo:** Si tienes dudas sobre cualquier comando, puedes usar `git help <comando>` para ver detalles y ejemplos de uso. ¡Git tiene una curva de aprendizaje, pero es una herramienta poderosa una vez que la dominas!



