# Ejercicio 4 – Ignorar archivos con .gitignore
## Objetivo
Usar .gitignore para evitar subir archivos innecesarios.

## Instrucciones
1. Crea estos archivos:
   ```bash
   touch .env log.txt
   mkdir node_modules && touch node_modules/test.js
   ```
2. Crea el .gitignore:
   ```bash
   echo ".env" >> .gitignore
   echo "log.txt" >> .gitignore
   echo "node_modules/" >> .gitignore
   git add .gitignore
   git commit -m "Agrega .gitignore"
   ```
