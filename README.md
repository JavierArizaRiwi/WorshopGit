# 🚀 Git Workshop – De Básico a Avanzado

Este documento está diseñado para ayudarte a comprender y practicar Git desde cero, ideal para coders que se están adentrando en el mundo del desarrollo colaborativo.

---

## 📚 1. Comandos Esenciales de Git

### 🔹 `git init`
Inicializa un nuevo repositorio Git en el directorio actual.

```bash
git init
```

### 🔹 `git clone <url>`
Clona un repositorio remoto a tu máquina local.

```bash
git clone https://github.com/usuario/proyecto.git
```

### 🔹 `git status`
Muestra el estado actual del repositorio.

```bash
git status
```


### 🔹 `git add <archivo> / git add .`
Agrega cambios al área de preparación (staging).

```bash
git add index.html
git add .
```

### 🔹 `git commit -m "mensaje"`
Registra los cambios en el historial local.

```bash
git commit -m "Agrega componente de login"
```

### 🔹 `git push`
Envía los cambios locales al repositorio remoto.

```bash
git push origin main
```

### 🔹 `git pull`
Descarga y fusiona los cambios del repositorio remoto.

```bash
git pull origin main
```

### 🔹 `git checkout -b <rama>`

```bash
git checkout -b feature/navbar
```

### 🔹 `git merge <rama>`
Fusiona la rama indicada con la actual.

```bash
git merge feature/navbar
```


### 🔹 `git branch -d <rama>`
Elimina una rama local.

```bash
git branch -d feature/navbar
```

### 🔹 `git log --oneline`
Muestra el historial de commits de forma compacta.`

```bash
git log --oneline
```



