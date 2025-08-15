# Guía Completa: Configurar y Trabajar **solo con Pull Requests** (PR)

> **Objetivo:** Que tu equipo trabaje **siempre** mediante Pull Requests para integrar cambios, con ramas protegidas, revisiones obligatorias y buenas prácticas claras.  
> **Público:** Coders que inician con Git y colaboración.

---

## 1) Conceptos clave (rápido)
- **Repositorio remoto**: servidor compartido (GitHub, GitLab, Bitbucket o bare interno).
- **Ramas protegidas**: ramas a las que **no se puede pushear directamente** (ej. `main` y `develop`). Solo aceptan cambios mediante PR.
- **Pull Request (PR)**: propuesta de cambios de una rama (ej. `feature/login`) hacia otra (ej. `develop`) para revisión y merge.
- **Revisión / Code Review**: compañeros validan el PR (comentarios, correcciones, aprobación).
- **Estrategia de merge**: cómo entra el PR (merge commit, squash, rebase).

---

## 2) Estructura de ramas sugerida
- `main` → producción (siempre estable).
- `develop` → integración para la próxima versión.
- `feature/<nombre>` → nuevas funcionalidades.
- `release/<versión>` → estabilización antes de publicar.
- `hotfix/<bug>` → parches urgentes desde `main`.

> Si tu equipo es pequeño, puedes empezar solo con `main` + `feature/*` y PR directamente a `main`.

---

## 3) Reglas del repositorio (obligatorias)
1. **Prohibido** hacer push directo a `main` (y `develop`, si la usas).
2. Todo cambio entra por **PR** con al menos **1 aprobación**.
3. Commits **atómicos** y mensajes claros (convenciones abajo).
4. PR con **checklist** y **evidencia** mínima (cómo probaste).
5. Resolver **conflictos** y **comentarios** antes de merge.

---

## 4) Configuración de ramas protegidas (GUI)
> Los nombres de menús cambian poco entre GitHub y GitLab. Ajusta según tu plataforma.

### 4.1. GitHub
1. Repo → **Settings** → **Branches** → **Branch protection rules** → **Add rule**.
2. **Branch name pattern**: `main` (repite para `develop` si aplica).
3. Habilita opciones recomendadas:
   - ✅ **Require a pull request before merging**
     - **Require approvals**: 1 (o 2)  
     - **Dismiss stale pull request approvals when new commits are pushed**
     - **Require review from Code Owners** (si usas `CODEOWNERS`)
     - **Require conversation resolution before merging**
   - ✅ **Require status checks to pass before merging** (si usas CI)
   - ✅ **Require linear history** (opcional, mantiene historial limpio)
   - ✅ **Restrict who can push to matching branches** (vacío si solo PRs)
4. Guardar. Repetir para `develop` si la usas.

### 4.2. GitLab
1. Repo → **Settings** → **Repository** → **Protected branches**.
2. Agrega `main` (y `develop` si aplica) como **Protected**:
   - **Allowed to merge**: Maintainers (o rol que decidan).
   - **Allowed to push**: No one (o solo CI si corresponde).
3. **Merge requests** (PR en GitLab):
   - Activar **Approval rules** (1 o 2 revisores).
   - Requerir **resolve all threads** antes de merge (Discussions).

> **Bitbucket**: Repos → Settings → **Branch permissions** (muy similar).


---

## 5) Plantillas que ayudan (colocar en tu repo)

### 5.1. `.github/pull_request_template.md` (o `docs/PR_TEMPLATE.md`)
```md
## Descripción
- ¿Qué cambia y por qué?

## Checklist
- [ ] Rama basada en `develop` (o `main` si no usas develop)
- [ ] Commits atómicos y claros (conventional commits)
- [ ] Probado localmente / tests pasan
- [ ] Sin cambios no relacionados
- [ ] Documentación/CHANGELOG actualizado (si aplica)

## Evidencia
- Comandos / capturas / logs
```

### 5.2. `CODEOWNERS` (opcional, fuerza revisiones de dueños de área)
```
# Raíz: todos los cambios requieren revisión del equipo core
*       @equipo-core

# Ejemplos por carpeta
/docs/  @equipo-docs
/src/   @equipo-backend @equipo-frontend
```

### 5.3. `docs/CONTRIBUTING.md`
```md
# Guía de contribución
- Ramas: feature/<nombre>, release/<x.y.z>, hotfix/<bug>
- Base de PR: a develop (o main si no usas develop)
- Estrategia de merge:
  - Features: squash
  - Release/Hotfix: --no-ff (conservar nodo de merge)
- Commits (conventional):
  - feat|fix|docs|refactor|test|chore: mensaje breve en minúsculas
- Reglas de PR:
  - Mínimo 1 aprobación
  - Resolver discusiones antes del merge
  - Adjuntar evidencia de pruebas
```

---

## 6) Flujo de trabajo para los coders (paso a paso)

> Ejemplo con `develop` como rama base de features. Si no la usas, cambia `develop` por `main`.

### 6.1. Preparar entorno local (una vez)
```bash
git clone <url-del-repo>         # Descarga el repositorio remoto
cd <carpeta>                     # Entra a la carpeta del proyecto
git config user.name "<Tu Nombre>"   # Configura tu nombre
git config user.email "<tu@correo>" # Configura tu correo
git fetch --all                  # Actualiza toda la información remota
```

### 6.2. Crear una feature
```bash
git checkout develop             # Cambia a la rama de integración
git pull                         # Actualiza la rama
git checkout -b feature/formulario-contacto   # Crea y cambia a una nueva rama
# (editar archivos, implementar cambios)
git add -A                       # Prepara todos los cambios
git commit -m "feat: agrega formulario de contacto"   # Guarda los cambios con mensaje claro
git push -u origin feature/formulario-contacto        # Sube la rama al remoto
```

### 6.3. Abrir PR
- Ve al remoto (GitHub/GitLab).
- **Base**: `develop` (o `main` si no usas develop).
- **Compare**: `feature/formulario-contacto`.
- Rellena plantilla, sube evidencia y solicita **revisores**.

### 6.4. Mantener tu rama actualizada (antes de merge)
```bash
git fetch origin
git checkout feature/formulario-contacto
git merge origin/develop        # o: git rebase origin/develop (si la política lo permite)
# resolver conflictos si aparecen
git add -A
git commit -m "fix: resuelve conflictos con develop"
git push
```

### 6.5. Revisión y merge
- Atiende comentarios en el PR (commits adicionales).
- Pide aprobación (mín. 1).
- Cuando CI y checklist estén OK → **Merge** según la política:
  - **Squash** para features (historial limpio).
  - **--no-ff** para release/hotfix (conservar nodo de merge).

### 6.6. Después del merge
```bash
git checkout develop
git pull
# (opcional) borrar rama remota desde el PR y local:
git branch -d feature/formulario-contacto
git push origin --delete feature/formulario-contacto
```

---

## 7) Releases y Hotfix (opcional si usas Git Flow completo)

### 7.1. Release
```bash
git checkout develop
git pull
git checkout -b release/1.0.0
# actualizar versión/CHANGELOG
git commit -am "chore(release): prepara 1.0.0"
git push -u origin release/1.0.0
# PR: release/1.0.0 -> main (require approvals)
# tras merge:
git tag -a v1.0.0 -m "Release 1.0.0"
git push origin main --tags
# merge-back a develop (PR o merge protegido):
git checkout develop && git pull && git merge --no-ff main && git push
```

### 7.2. Hotfix
```bash
git checkout main
git pull
git checkout -b hotfix/critical-bug
# fix...
git commit -am "fix: corrige bug crítico"
git push -u origin hotfix/critical-bug
# PR: hotfix -> main
# tras merge:
git tag -a v1.0.1 -m "Hotfix 1.0.1"
git push origin main --tags
# merge-back a develop
git checkout develop && git pull && git merge --no-ff main && git push
```

---

## 8) Buenas prácticas de equipo
- **Pequeños PRs** (fáciles de revisar).
- **Mensajes de commit claros** (qué y por qué).
- **Checklist de PR** siempre completa.
- **Resuelve conversaciones** antes de merge.
- **CI básico** (si existe): linting, tests rápidos.
- **Changelog** actualizado en releases.
- Documentar **cómo correr** el proyecto en `README`.

---

## 9) Troubleshooting rápido
- **No puedo pushear a `main`/`develop`:** las ramas están protegidas. Crea **feature/** y abre PR.
- **Mi PR tiene commits ajenos:** sincroniza tu rama con `develop` o `main` antes de pushear (merge o rebase).
- **Conflictos al actualizar PR:** resuélvelos localmente, añade y commitea la resolución, vuelve a pushear.
- **Aprobación desapareció:** si hiciste nuevos commits, es normal (regla de “dismiss stale approvals”). Solicita re-revisión.

---

## 10) Checklist del facilitador (para entrenamientos)
- [ ] Ramas `main` (y `develop`) protegidas.
- [ ] Plantilla de PR + `CONTRIBUTING.md` + (opcional) `CODEOWNERS`.
- [ ] Política de merge definida (squash en features).
- [ ] Ejercicios preparados: 2 features paralelas + conflicto controlado.
- [ ] Simular 1 release y 1 hotfix (si hay tiempo).
- [ ] Evaluación: PRs con checklist, revisiones efectivas, merges limpios, tags creados.

---

### Anexo: Convenciones de commits (conventional commits)
```
feat: nueva funcionalidad
fix: corrección de bug
docs: solo documentación
refactor: cambio interno sin alterar funcionalidad
test: agrega o corrige pruebas
chore: tareas de soporte (build, dependencias, etc.)
```
