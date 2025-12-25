# 📚 Guía Completa de Git

Una guía completa y práctica para dominar Git, desde los comandos básicos hasta técnicas avanzadas.

## 📋 Tabla de Contenidos

- [📚 Guía Completa de Git](#-guía-completa-de-git)
  - [📋 Tabla de Contenidos](#-tabla-de-contenidos)
  - [⚡ Alias de Git](#-alias-de-git)
    - [🔍 Ver toda la configuración](#-ver-toda-la-configuración)
  - [⚙️ Configuración Inicial](#️-configuración-inicial)
    - [Configurar usuario y correo](#configurar-usuario-y-correo)
    - [Inicializar repositorio](#inicializar-repositorio)
  - [🎯 Comandos Básicos](#-comandos-básicos)
    - [`git status`](#git-status)
    - [`git add`](#git-add)
    - [`git commit`](#git-commit)
    - [`git log`](#git-log)
    - [`git diff`](#git-diff)
    - [`git checkout`](#git-checkout)
    - [`git reset`](#git-reset)
    - [`git reflog`](#git-reflog)
  - [🔧 Configuración Avanzada](#-configuración-avanzada)
    - [Alias personalizados](#alias-personalizados)
    - [`.gitignore`](#gitignore)
  - [🏷️ Etiquetado (Tags)](#️-etiquetado-tags)
  - [🌿 Trabajo con Ramas](#-trabajo-con-ramas)
    - [`git branch`](#git-branch)
    - [`git switch`](#git-switch)
    - [`git merge`](#git-merge)
  - [⚔️ Resolución de Conflictos](#️-resolución-de-conflictos)
  - [📦 Git Stash](#-git-stash)
  - [🔄 Flujo de Trabajo con Ramas](#-flujo-de-trabajo-con-ramas)
    - [Flujo básico de desarrollo](#flujo-básico-de-desarrollo)
    - [📌 Buenas prácticas con ramas](#-buenas-prácticas-con-ramas)
  - [🧹 Comandos de Limpieza](#-comandos-de-limpieza)
  - [💡 Consejos y Mejores Prácticas](#-consejos-y-mejores-prácticas)
  - [📚 Recursos Adicionales](#-recursos-adicionales)

## ⚡ Alias de Git

Acelera tu flujo de trabajo con estos alias útiles:
```bash
~/.zshrc
```
```bash

alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git log --oneline --graph'
alias gd='git diff'
alias grel='git reflog'
```

### 🔍 Ver toda la configuración

```bash
git config --list --show-origin
```

## ⚙️ Configuración Inicial

### Configurar usuario y correo

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tuemail@ejemplo.com"
```

### Inicializar repositorio

```bash
git init
git branch -m main  # Cambiar nombre de rama principal
```

## 🎯 Comandos Básicos

### `git status`

Muestra el estado actual del repositorio.

```bash
git status
```

### `git add`

Añade archivos al área de preparación (staging area).

```bash
git add archivo.txt    # Añadir archivo específico
git add .              # Añadir todos los archivos
```

### `git commit`

Crea una instantánea del estado actual.

```bash
git commit -m "Descripción de los cambios"
git commit  # Abrir editor para mensaje detallado
```

**💡 Buenas prácticas para mensajes de commit:**
- ✅ Usa presente imperativo: "Añade", "Corrige", "Actualiza"
- ✅ Primera línea breve (máximo 50 caracteres)
- ✅ Deja línea en blanco antes de descripción detallada
- ✅ Explica el "qué" y el "por qué", no el "cómo"

### `git log`

Muestra el historial de commits.

```bash
git log                    # Log completo
git log --oneline --graph  # Log compacto con gráfico
git log --stat             # Log con estadísticas
```

### `git diff`

Muestra diferencias entre archivos.

```bash
git diff              # Cambios no preparados
git diff --staged     # Cambios preparados
git diff <hash1> <hash2>  # Comparar commits
```

### `git checkout`

Restaura archivos o cambia entre ramas.

```bash
git checkout -- archivo.txt  # Descartar cambios
git checkout nombre-rama     # Cambiar a rama
git checkout <hash>          # Ir a commit específico
```

### `git reset`

Deshace commits o mueve el HEAD.

```bash
git reset --soft HEAD~1   # Mantener cambios en staging
git reset --mixed HEAD~1  # Mantener cambios sin staging
git reset --hard HEAD~1   # ⚠️ ELIMINAR todos los cambios
git reset --hard <hash>   # Volver a commit específico
```

> ⚠️ **Advertencia:** `git reset --hard` elimina cambios permanentemente. Úsalo con precaución.

### `git reflog`

Muestra registro de movimientos del HEAD (útil para recuperar commits).

```bash
git reflog
```

## 🔧 Configuración Avanzada

### Alias personalizados

```bash
git config --global alias.lg "log --oneline --graph --all"
git config --global alias.unstage "reset HEAD --"
git config --global alias.last "log -1 HEAD"
```

### `.gitignore`

Especifica archivos que Git debe ignorar.

```bash
touch .gitignore
```

**Ejemplos de patrones comunes:**

```gitignore
# Archivos del sistema
.DS_Store
Thumbs.db

# Dependencias
node_modules/
vendor/

# Archivos de compilación
*.pyc
*.class
*.o
dist/
build/

# Configuración local
.env
config.local.js

# IDEs
.vscode/
.idea/
*.swp
```

**Después de crear `.gitignore`:**

```bash
git add .gitignore
git commit -m "Añade archivo .gitignore"
```

## 🏷️ Etiquetado (Tags)

Marca puntos importantes en el historial (versiones, hitos).

```bash
# Tag ligero
git tag v1.0.0

# Tag anotado (recomendado)
git tag -a v1.0.0 -m "Versión 1.0.0 - Lanzamiento inicial"

# Listar tags
git tag

# Ver información de tag
git show v1.0.0

# Cambiar a tag
git checkout tags/v1.0.0

# Eliminar tag
git tag -d v1.0.0
```

## 🌿 Trabajo con Ramas

Las ramas permiten desarrollar funcionalidades de forma aislada.

### `git branch`

Gestiona ramas en el repositorio.

```bash
git branch              # Listar ramas
git branch nombre-rama  # Crear rama
git branch -d nombre-rama    # Eliminar rama
git branch -D nombre-rama    # Eliminar forzosamente
git branch -m nuevo-nombre   # Renombrar rama actual
```

### `git switch`

Comando moderno para cambiar entre ramas.

```bash
git switch nombre-rama       # Cambiar a rama
git switch -c nueva-rama     # Crear y cambiar
git switch -                 # Volver a rama anterior
```

### `git merge`

Integra cambios de una rama a otra.

```bash
git merge nombre-rama        # Fusionar rama
git merge --no-ff nombre-rama  # Crear commit de merge
git merge --abort            # Abortar merge
```

## ⚔️ Resolución de Conflictos

Cuando dos ramas modifican las mismas líneas, Git marca los conflictos:

```
<<<<<<< HEAD
Contenido de la rama actual
=======
Contenido de la rama que intentas fusionar
>>>>>>> nombre-rama
```

**Proceso de resolución:**

1. Edita manualmente los archivos
2. Añade archivos resueltos: `git add archivo-resuelto.txt`
3. Completa el merge: `git commit -m "Resuelve conflictos"`

**Herramientas útiles:**

```bash
git status      # Ver archivos con conflictos
git mergetool   # Herramienta visual
```

## 📦 Git Stash

Guarda temporalmente cambios sin hacer commit.

```bash
git stash                              # Guardar cambios
git stash save "Mensaje descriptivo"   # Con mensaje
git stash list                         # Listar stashes
git stash pop                          # Aplicar y eliminar
git stash apply                        # Aplicar sin eliminar
git stash apply stash@{0}              # Aplicar específico
git stash drop                         # Eliminar último
git stash drop stash@{0}               # Eliminar específico
git stash clear                        # Eliminar todos
git stash show -p stash@{0}            # Ver contenido
```

**Casos de uso:**
- Cambiar de rama sin commit
- Probar solución alternativa
- Hacer pull sin conflictos

## 🔄 Flujo de Trabajo con Ramas

### Flujo básico de desarrollo

```bash
# 1. Crear rama de funcionalidad
git switch -c feature/nueva-funcionalidad

# 2. Desarrollar y hacer commits
git add .
git commit -m "Implementa funcionalidad X"

# 3. Actualizar con cambios de main
git switch main
git pull
git switch feature/nueva-funcionalidad
git merge main

# 4. Integrar a main
git switch main
git merge feature/nueva-funcionalidad

# 5. Eliminar rama
git branch -d feature/nueva-funcionalidad
```

### 📌 Buenas prácticas con ramas

- ✅ Mantén ramas de corta duración
- ✅ Usa nombres descriptivos: `feature/login`, `bugfix/typo`, `hotfix/security`
- ✅ Haz merge frecuentemente
- ✅ Elimina ramas fusionadas
- ✅ No trabajes directamente en `main`

## 🧹 Comandos de Limpieza

```bash
# Eliminar ramas fusionadas
git branch --merged | grep -v "\*" | xargs -n 1 git branch -d

# Limpiar referencias remotas
git fetch --prune

# Ver espacio usado
git count-objects -vH

# Optimizar repositorio
git gc --aggressive --prune=now
```

## 💡 Consejos y Mejores Prácticas

1. **Commits frecuentes y pequeños** → Facilitan revisión y rollback
2. **Mensajes claros** → Ayudan a entender el historial
3. **Una rama por funcionalidad** → Mantén trabajo organizado
4. **Revisa antes de commit** → Usa `git diff` y `git status`
5. **No commitees archivos sensibles** → Usa `.gitignore`
6. **Mantén main estable** → Prueba antes de fusionar
7. **Documenta el flujo** → Crea `CONTRIBUTING.md`

## 📚 Recursos Adicionales

- [Documentación oficial de Git](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book/es/v2)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Visualizing Git](https://git-school.github.io/visualizing-git/)

---

<div align="center">

**¿Te ha sido útil esta guía?** ⭐ Dale una estrella al repositorio

[Reportar un error](../../issues) · [Sugerir mejora](../../issues)

</div>
