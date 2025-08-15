# Ejercicio 2 – Trabajando con ramas
## Objetivo
Crear y fusionar ramas, resolver conflictos.

---

## ¿Qué es una rama en Git?
Una rama es una copia del proyecto donde puedes trabajar en nuevas ideas sin afectar el código principal. Así puedes experimentar y luego unir tus cambios al proyecto principal.

---

## Instrucciones paso a paso

### 1. **Crea una rama y realiza cambios**
Primero, crea una nueva rama llamada `desarrollo` y haz un cambio en el archivo `README.md`.

```bash
git checkout -b desarrollo   # Crea y cambia a la rama 'desarrollo'
echo "Linea nueva" >> README.md   # Agrega una línea al archivo README.md
git add .                     # Prepara los cambios para guardarlos
git commit -m "Cambios en desarrollo"   # Guarda los cambios con un mensaje
```

---

### 2. **Vuelve a la rama principal (`main`) y fusiona los cambios**
Ahora regresa a la rama principal y une los cambios de la rama `desarrollo`.

```bash
git checkout main             # Cambia a la rama principal
git merge desarrollo          # Une los cambios de 'desarrollo' a 'main'
```
Si no hay conflictos, el proceso termina aquí.

---

### 3. **Simula un conflicto**
Un conflicto ocurre cuando dos ramas modifican la misma parte de un archivo. Vamos a provocarlo para aprender a resolverlo.

- Cambia la misma línea de `README.md` en la rama `main` y guarda el cambio:

  ```bash
  echo "Cambio diferente en la misma línea" > README.md
  git add README.md
  git commit -m "Cambio en main que genera conflicto"
  ```

- Cambia a la rama `desarrollo` y modifica la misma línea de nuevo:

  ```bash
  git checkout desarrollo
  echo "Otro cambio en la misma línea" > README.md
  git add README.md
  git commit -m "Cambio en desarrollo que genera conflicto"
  ```

- Vuelve a `main` e intenta fusionar:

  ```bash
  git checkout main
  git merge desarrollo
  ```

---

### 4. **Resuelve el conflicto**
Git te avisará que hay un conflicto y marcará el archivo con líneas como estas:

```
<<<<<<< HEAD
Cambio diferente en la misma línea
=======
Otro cambio en la misma línea
>>>>>>> desarrollo
```

- Abre el archivo y decide qué versión dejar (puedes combinar ambas si lo deseas).
- Borra las líneas `<<<<<<<`, `=======`, y `>>>>>>>` y deja solo el texto final.
- Guarda el archivo.

- Indica a Git que resolviste el conflicto y guarda el cambio:

  ```bash
  git add README.md
  git commit -m "Resuelve conflicto entre main y desarrollo"
  ```

---

### 5. **Verifica que el conflicto se resolvió y el historial está correcto**

```bash
git log --oneline --graph   # Muestra el historial de cambios de forma visual
```

---

## 📝 Notas y consejos para principiantes

- **¿Por qué usar ramas?** Permiten trabajar en nuevas funciones sin afectar el proyecto principal.
- **¿Qué es un conflicto?** Es cuando dos personas (o ramas) cambian la misma parte de un archivo. Git no sabe cuál elegir y te pide ayuda.
- **¿Cómo resolverlo?** Edita el archivo, decide qué cambios conservar y guarda el resultado.
- **¿Qué pasa si me equivoco?** Puedes pedir ayuda, ¡no tengas miedo de experimentar!
- **¿Cómo saber si hay conflictos?** Git te lo dirá y marcará los archivos afectados.

---

### 💡 Tip extra
Puedes usar editores como VS Code, que te muestran los conflictos de forma visual y te ayudan a elegir qué cambios conservar.

---

**¡Felicidades! Ahora sabes cómo crear ramas, fusionarlas y resolver conflictos.
