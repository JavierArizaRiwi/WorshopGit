# Workshop Colaborativo de Git con **Git Flow** (Equipos de 3–5 coders)

> **Objetivo:** Que un equipo de 3–5 personas sea capaz de trabajar en un repositorio compartido usando **Git** y el flujo **Git Flow**, creando features en paralelo, resolviendo conflictos, integrando una **release** y atendiendo un **hotfix** con etiquetas (tags).  
---

## 0) ¿Qué es Git? ¿Y qué es Git Flow?
- **Git**: Sistema de control de versiones distribuido. Permite:
  - Guardar cambios (**commits**).
  - Trabajar en paralelo en **ramas** (branches).
  - Integrar código de varias personas (**merge**/**rebase**).
  - Volver a estados anteriores si algo falla.
- **Repositorio**: carpeta con historial de cambios.
- **Remoto**: servidor que guarda el repositorio para colaborar (GitHub/GitLab/Bitbucket o un repo “bare” interno).
- **Git Flow**: Una **estrategia de ramas** que ordena el trabajo del equipo:
  - `main` → código **estable** (producción).
  - `develop` → código **en integración** (lo que se prepara para la próxima versión).
  - `feature/*` → desarrollo de nuevas funcionalidades.
  - `release/*` → estabilización previa a publicar una versión.
  - `hotfix/*` → arreglos urgentes sobre `main`.
  
> **Mental model:** Construimos nuevas cosas en `feature/*`, las unimos en `develop`, preparamos la entrega en `release/*` y publicamos en `main`. Si hay un bug en producción, lo arreglamos en `hotfix/*` y lo devolvemos a `develop`.

---

## 1) Requisitos previos 
- Tener instalado **Git**: `git --version`
- Tener acceso a un **remoto** compartido (o crear un bare repo interno).
- Elegir un **editor** (VS Code, etc.).
- (Opcional) Si usan plataforma remota (GitHub/GitLab/Bitbucket), crean un repo vacío.

> **Nota para principiantes:** Git ≠ GitHub. Git es la herramienta; GitHub es un servicio para hospedar repositorios Git.

---

## 2) Roles dentro del equipo (3–5 personas)
- **Lead**: prepara el repo remoto, crea ramas base (`main`, `develop`), protege ramas.
- **Dev A / Dev B / Dev C**: implementan features en paralelo.
- **QA (opcional si son 5)**: valida release, crea issues de bugs, prueba hotfix.

**Sugerencia de dinámica:** rota los roles en cada bloque para que todos practiquen.

---

## 3) Estructura inicial del repositorio

```
repo-colaborativo/
├─ src/
│  ├─ app.js               # punto de entrada (o README de cómo correr)
│  ├─ utils/
│  │  └─ calc.js
│  └─ features/
│     ├─ feature-a/
│     ├─ feature-b/
│     └─ feature-c/
├─ tests/
│  └─ calc.test.js
├─ docs/
│  ├─ CONTRIBUTING.md
│  └─ CHANGELOG.md
├─ .gitignore
├─ README.md               # este archivo (guía del workshop)
└─ issues.md               # lista de tareas simuladas
```

**Convenciones de commits (estilo “conventional commits”):**  
`feat: ...` (nueva funcionalidad) · `fix: ...` (corrección) · `docs: ...` (documentación) · `refactor: ...` · `test: ...` · `chore: ...`

---

## 4) Paso a paso del Workshop

### 4.1. Bloque 1 – Setup (30 min)
**Lead (una persona):**
```bash
# 1) Crear repo local y primer commit
git init
git add .
git commit -m "chore: initial scaffold"

# 2) Rama principal (producción)
git branch -M main

# 3) Conectar con el remoto (reemplaza <URL>)
git remote add origin <URL-o-ruta-bare>
git push -u origin main

# 4) Crear rama de integración
git checkout -b develop
git push -u origin develop
```

**Todos (resto del equipo):**
```bash
git clone <URL-o-ruta-remota>
cd repo-colaborativo
git config user.name "<Tu Nombre>"
git config user.email "<tu@correo>"
```

**Acordar reglas rápidas:**
- Nombres de ramas: `feature/<nombre>`, `release/<semver>`, `hotfix/<bug>`
- Commits claros y atómicos.
- PRs hacia `develop` (features), hacia `main` (release/hotfix).
- Mínimo 1 revisor por PR y checklist.

---

### 4.2. Bloque 2 – Features en paralelo
**Preparar issues (tareas) en `issues.md`:**
```md
# Sprint Taller
- Feature A: UI del menú
- Feature B: Lógica de cálculo en utils/calc.js
- Feature C: Exportar un reporte (archivo .txt con resultados)
```

**Cada dev toma una tarea y crea su rama feature:**
```bash
git checkout develop
git pull
git checkout -b feature/feature-a-ui   # ejemplo
# ... implementa cambios ...
git add .
git commit -m "feat: add basic UI for feature A"
git push -u origin feature/feature-a-ui
```

**Abrir Pull Request (PR):**
- Base: `develop`
- Título: `feat: ...`
- Descripción: qué cambia y por qué.
- Adjuntar evidencia (captura/log/comando).

**Revisión cruzada:**
- Cada dev revisa 1 PR de otra persona.
- Comentarios concretos (código, naming, tests).

**Merge a `develop`:**
- Política inicial sugerida: **squash** para features.
- Verificar que el proyecto corre (o tests pasan) en `develop`.

---

### 4.3. Bloque 3 – Integración y conflictos (35–45 min)
**Conflicto controlado (facilitador):**
- Pide a **Dev A** y **Dev B** editar la **misma línea** en `src/utils/calc.js` en ramas diferentes.
- Ambos hacen commit/push y abren PR.

**Resolver un conflicto (ejemplo en local):**
```bash
git checkout feature/feature-b-logic
git fetch origin
git merge origin/develop   # o rebase si el equipo lo prefiere
# (se produce conflicto)
# -> Abrir el archivo en el editor, elegir qué conservar
git add src/utils/calc.js
git commit -m "fix: resolve merge conflict with develop"
git push
```
- Actualizar PR, pedir re-revisión y completar el merge.
- Validar que `develop` queda estable.

---

### 4.4. Bloque 4 – Release y tag (25–35 min)
**Lead corta una rama de release desde `develop`:**
```bash
git checkout develop
git pull
git checkout -b release/1.0.0
# actualizar docs/CHANGELOG.md y versión (si aplica)
git commit -am "chore(release): prepare 1.0.0"
git push -u origin release/1.0.0
```

**QA valida la release** (ejecución, checklist, revisión de PRs).

**Publicar la release a `main` con tag:**
```bash
git checkout main
git pull
git merge --no-ff release/1.0.0 -m "release: 1.0.0"
git tag -a v1.0.0 -m "Release 1.0.0"
git push origin main --tags
```

**Propagar cambios a `develop`:**
```bash
git checkout develop
git pull
git merge --no-ff release/1.0.0 -m "merge back release 1.0.0"
git push
```

---

### 4.5. Bloque 5 – Hotfix (15–25 min)
**QA** abre un issue crítico encontrado en `main`.  
**Lead** crea rama `hotfix/*` desde `main`:
```bash
git checkout main
git pull
git checkout -b hotfix/critical-bug
# arreglar el bug...
git commit -am "fix: critical bug in calc()"
git push -u origin hotfix/critical-bug
```

**PR → `main`**, merge y **tag**:
```bash
git checkout main
git pull
git merge --no-ff hotfix/critical-bug -m "hotfix: 1.0.1"
git tag -a v1.0.1 -m "Hotfix 1.0.1"
git push origin main --tags
```

**Back-merge del hotfix a `develop`:**
```bash
git checkout develop
git pull
git merge --no-ff main -m "merge hotfix 1.0.1 into develop"
git push
```

---

## 5) Plantillas útiles

### 5.1. Plantilla de Pull Request (cópiala a `.github/pull_request_template.md` o `docs/PR_TEMPLATE.md`)
```md
## Descripción
- ¿Qué cambia y por qué?

## Checklist
- [ ] Rama basada en `develop`
- [ ] Commits claros y atómicos (conventional commits)
- [ ] Probado localmente / tests pasan
- [ ] Sin cambios no relacionados

## Evidencia
- Capturas, logs, comandos, etc.
```

### 5.2. `docs/CONTRIBUTING.md` (reglas de colaboración)
```md
# Convenciones del proyecto
- Ramas:
  - main (producción)
  - develop (integración)
  - feature/<nombre-corto>
  - release/<semver>
  - hotfix/<bug>
- Commits:
  - feat|fix|docs|refactor|test|chore: mensaje breve en minúsculas
- Pull Requests:
  - Base: develop (features), main (release/hotfix)
  - Mínimo 1 revisor, usar checklist
- Estrategia de merge:
  - squash para features (historial limpio)
  - --no-ff para release/hotfix (conservar nodo de merge)
```

### 5.3. `docs/CHANGELOG.md` (historial de cambios)
```md
## [1.0.0] - YYYY-MM-DD
### Added
- Feature A (UI)
- Feature B (logic)

### Fixed
- Conflictos integrados en utils/calc.js
```

### 5.4. `issues.md` (tareas del taller – ejemplo)
```md
# Sprint Taller
- Feature A: UI del menú (crear vista simple y navegación)
- Feature B: Lógica de cálculo en utils/calc.js (sumar/restar/multiplicar/dividir)
- Feature C: Exportar un reporte (archivo .txt con resultados)
- Bug crítico: división por cero en calc()
```

---

## 6) Ejercicios prácticos

1) **Features en paralelo:** dos devs implementan cambios distintos en `calc.js` y en `/features`.
2) **Conflicto controlado:** ambos editan la misma línea de `calc.js` y resuelven el merge.
3) **PR con checklist:** abrir PR a `develop`, revisión cruzada, solicitar cambios y aprobar.
4) **Release 1.0.0:** crear `release/1.0.0`, actualizar `CHANGELOG`, publicar a `main` con tag y merge-back a `develop`.
5) **Hotfix 1.0.1:** arreglar bug en `main`, taggear, y fusionar de vuelta a `develop`.

---

## 7) Troubleshooting (preguntas frecuentes)

- **“Mi PR tiene commits de otras personas”**  
  Actualiza tu rama antes de pushear:
  ```bash
  git fetch origin
  git checkout feature/mi-rama
  git merge origin/develop    # o rebase si el equipo lo prefiere
  ```

- **“No puedo pushear a main/develop”**  
  Es probable que estén **protegidas**. Sube a tu rama `feature/*` y abre un PR.

- **“Conflictos al publicar la release”**  
  Prioriza `main` (producción), integra con `--no-ff`, corrige y propaga a `develop`.

- **“Hice un commit por error”**  
  Usa `git revert <hash>` (seguro en ramas compartidas). Evita `reset --hard` en remoto compartido.

---

## 8) Guía “de bolsillo” (comandos esenciales)

```bash
# Crear rama develop y subirla
git checkout -b develop
git push -u origin develop

# Nueva feature
git checkout -b feature/feature-a
# ...cambios...
git add .
git commit -m "feat: implement feature A"
git push -u origin feature/feature-a

# Actualizar mi feature desde develop
git fetch
git checkout feature/feature-a
git merge origin/develop   # o rebase si lo definen
# resolver conflictos, luego:
git add .
git commit -m "fix: resolve conflicts"
git push

# Release
git checkout -b release/1.0.0 origin/develop
# actualizar versión/CHANGELOG
git commit -am "chore(release): prepare 1.0.0"
git push -u origin release/1.0.0

# Publicar release
git checkout main
git pull
git merge --no-ff release/1.0.0 -m "release: 1.0.0"
git tag -a v1.0.0 -m "Release 1.0.0"
git push origin main --tags

# Merge-back a develop
git checkout develop
git pull
git merge --no-ff release/1.0.0 -m "merge back release 1.0.0"
git push

# Hotfix
git checkout -b hotfix/critical-bug origin/main
# fix...
git commit -am "fix: critical bug"
git push -u origin hotfix/critical-bug

# Publicar hotfix y tag
git checkout main
git pull
git merge --no-ff hotfix/critical-bug -m "hotfix: 1.0.1"
git tag -a v1.0.1 -m "Hotfix 1.0.1"
git push origin main --tags

# Propagar hotfix a develop
git checkout develop
git pull
git merge --no-ff main -m "merge hotfix 1.0.1 into develop"
git push
```

---

## 9) Criterios de evaluación (rubro sugerido)
- Aplicó correctamente el **flujo Git Flow**.
- Ramas bien nombradas y PRs hacia el destino correcto.
- Commits atómicos y con mensajes claros.
- Conflictos resueltos con explicación en el PR.
- Release etiquetada (`v1.0.0`) y hotfix etiquetado (`v1.0.1`).
- Documentación mínima creada/actualizada (`README`, `CONTRIBUTING`, `CHANGELOG`, `issues.md`).

---

## 10) Anexos (opcional para tu repo)
- **Plantilla de repo** (estructura y archivos vacíos).
- **Scripts** para correr tests o pequeña demo de `app.js`.
- **Checklist de facilitador** para controlar tiempos y objetivos.

> **Consejo final:** al principio prioriza **claridad y orden** sobre atajos. Una vez el equipo domina el flujo, pueden explorar variantes (rebase, estrategias de merge, automatizaciones CI/CD, etc.).
