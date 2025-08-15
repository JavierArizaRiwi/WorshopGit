# 🧪 Ejercicios Prácticos de Git

Este documento te guía paso a paso en las tareas más comunes de Git, con ejemplos y explicaciones para que aprendas practicando, incluso si nunca has usado Git antes.

---

## Ejercicio 1: Inicialización de repositorio

**Objetivo:** Crear un nuevo proyecto y guardar el primer cambio.

```bash
mkdir proyecto-git && cd proyecto-git      # Crea una carpeta y entra en ella
git init                                   # Inicializa el repositorio Git
echo "# Proyecto Git" > README.md          # Crea un archivo README.md con un título
git add README.md                          # Prepara el archivo para guardarlo
git commit -m "Primer commit"              # Guarda el cambio con un mensaje
```
**Comentario:**  
Así tu proyecto ya tiene historial y puedes empezar a registrar todos los cambios.

---

## Ejercicio 2: Conectar a un repositorio remoto

**Objetivo:** Subir tu proyecto local a GitHub para compartirlo y colaborar.

1. Crea un nuevo repositorio en GitHub (desde la web).
2. Ejecuta estos comandos en tu terminal:

```bash
git remote add origin https://github.com/usuario/proyecto.git   # Conecta tu repo local con el remoto
git branch -M main                                             # Renombra la rama principal a 'main' si es necesario
git push -u origin main                                        # Sube tu proyecto a GitHub
```
**Comentario:**  
Ahora tu proyecto está en línea y puedes trabajar desde cualquier lugar.

---

## Ejercicio 3: Crear una rama y trabajar en ella

**Objetivo:** Desarrollar una nueva funcionalidad sin afectar el código principal.

```bash
git checkout -b feature/formulario           # Crea y cambia a una nueva rama
# Edita tu código (por ejemplo, agrega un formulario)
git add .                                   # Prepara todos los archivos modificados
git commit -m "Agrega formulario de contacto" # Guarda los cambios con un mensaje claro
git push origin feature/formulario           # Sube la rama al repositorio remoto
```

Luego:

- Ve a GitHub y crea un **Pull Request** desde `feature/formulario` hacia `main`.
- Otro coder revisa y aprueba el PR.
- Se hace **merge** (se integran los cambios a `main`) y se elimina la rama.

**Comentario:**  
Trabajar en ramas permite que varias personas colaboren sin pisarse el trabajo.

---

## Ejercicio 4: Resolver conflictos

**Objetivo:** Aprender a solucionar cuando dos personas modifican la misma parte de un archivo.

1. Coder A y Coder B modifican la misma línea de `README.md` en ramas diferentes.
2. Ambos hacen commit en sus ramas.
3. Uno intenta hacer merge a `main`:

```bash
git checkout main
git merge feature/coder-a
```

4. Git detecta conflicto y marca el archivo así:

```
<<<<<<< HEAD
Texto de main
=======
Texto de la rama feature/coder-a
>>>>>>> feature/coder-a
```

5. Edita el archivo para dejar solo la versión correcta (puedes combinar ambos textos si lo deseas).
6. Guarda el archivo y resuelve el conflicto:

```bash
git add README.md
git commit -m "Resuelve conflicto de README"
```

**Comentario:**  
Los conflictos son normales cuando se trabaja en equipo. Edita el archivo, guarda solo lo que debe quedar y haz commit.

---

## Recomendaciones para el trabajo en equipo

- Haz `git pull` antes de comenzar a trabajar para tener la última versión.
- Crea ramas por cada funcionalidad o corrección.
- Haz commits descriptivos y frecuentes para facilitar el seguimiento.
- Usa Pull Requests para revisar y mantener la calidad del código.
- Elimina ramas locales y remotas cuando ya no se usen para mantener el repositorio limpio.
- Si tienes dudas, pregunta o consulta la documentación oficial de Git.

---

**¡Con estos ejercicios y recomendaciones ya puedes empezar a trabajar en proyectos colaborativos usando Git y GitHub!**
