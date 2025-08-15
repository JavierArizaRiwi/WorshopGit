# Ejercicio 4 – Ignorar archivos con .gitignore
## Objetivo
Usar .gitignore para evitar subir archivos innecesarios.

---

## ¿Qué es .gitignore?
Es un archivo especial donde le dices a Git qué archivos o carpetas no debe guardar ni subir al repositorio.  
Por ejemplo: archivos de configuración, carpetas de dependencias o archivos temporales.

---

## Instrucciones paso a paso

### 1. **Crea algunos archivos y carpetas de ejemplo**
Estos suelen ser archivos que no quieres compartir en el repositorio.

```bash
touch .env log.txt                       # Crea dos archivos: .env y log.txt
mkdir node_modules && touch node_modules/test.js   # Crea una carpeta y un archivo dentro
```

### 2. **Crea el archivo .gitignore**
Agrega los nombres de los archivos y carpetas que quieres ignorar.

```bash
echo ".env" >> .gitignore                # Ignora el archivo .env
echo "log.txt" >> .gitignore             # Ignora el archivo log.txt
echo "node_modules/" >> .gitignore       # Ignora la carpeta node_modules
git add .gitignore                       # Prepara el archivo .gitignore para guardarlo
git commit -m "Agrega .gitignore"        # Guarda el cambio en el historial
```

---

## 📝 Notas para principiantes

- **¿Por qué ignorar archivos?** Para no subir información privada, archivos grandes o carpetas que se generan automáticamente.
- **¿Qué pasa si ya subí un archivo antes de agregarlo a .gitignore?** Debes borrarlo del repositorio con `git rm --cached nombre_del_archivo` y luego hacer commit.
- Puedes agregar cualquier archivo o carpeta que no quieras compartir, solo escribe su nombre en `.gitignore`.

---

**¡Listo! Ahora tu repositorio solo tendrá los archivos importantes y no subirá los que no necesitas
