# Ejercicio 3 – Conectando con GitHub
## Objetivo
Subir el repositorio a GitHub y aprender a trabajar con repositorios remotos.

---

## ¿Qué es GitHub?
GitHub es una plataforma en línea donde puedes guardar tus proyectos y colaborar con otras personas usando Git.

---

## Instrucciones paso a paso

### 1. **Crea un repositorio en GitHub**
- Ve a [github.com](https://github.com/) y haz clic en "New repository".
- Ponle un nombre y deja la opción de "Add a README file" desmarcada (sin README).

### 2. **Enlaza tu repositorio local con GitHub**
Esto conecta tu proyecto en tu computadora con el repositorio en GitHub.

```bash
git remote add origin https://github.com/usuario/repo.git   # Enlaza tu repo local con el remoto
git branch -M main                                          # Renombra la rama principal a 'main' si es necesario
git push -u origin main                                     # Sube tu proyecto a GitHub
```
- **origin** es el nombre que Git usa para el repositorio remoto principal.
- El comando `-u` permite que en el futuro solo uses `git push` para subir cambios.

### 3. **Clona el repositorio en otro directorio**
Esto descarga una copia del proyecto desde GitHub a otra carpeta de tu computadora.

```bash
git clone https://github.com/usuario/repo.git   # Descarga el proyecto en una nueva carpeta
```

---

## 📝 Notas para principiantes

- **¿Por qué enlazar y subir?** Así puedes compartir tu trabajo y colaborar con otros.
- **¿Qué significa clonar?** Es copiar todo el proyecto y su historial a otra ubicación.
- Si ves algún error, revisa que la URL sea correcta y que tengas permisos en GitHub.

---


**¡Listo! Ahora tu proyecto está en GitHub y sabes cómo descargarlo en cualquier
parte de tu computadora. ¡A compartir código se ha dicho!**

