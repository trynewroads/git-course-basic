---
marp: true
theme: default
title: Git Básico
paginate: true
size: 16:9
backgroundColor: #2E2052;
color: #ffffff;
footer: Git Básico
header: |
  <div class="logo-start">
    <img src="../../images/git_logo_white.png" alt="Logo Git"  class="logo"/>
  </div>
  <div class="logo-end">
    <img src="../../images/logo_white.png" alt="Logo TNR" class="logo" />
  </div>

style: |
  section {
    display:flex;
  }

  section > h2, h3, h4, h5{
    border-bottom: 2px solid #2D6BFA;
    padding-bottom: .3rem;
  }

  section::after, header, footer {
    font-weight: 700;
    color: white;
  }

  section > header {
    display: flex;
    top: 0;
    width: calc(100% - 60px);
    background: radial-gradient(30% 100% at 50% 0%, #2D6BFA 0%, rgba(46, 32, 82, 0.00) 100%);
  }

  .logo-start{
    flex:1;
  }

  .logo-end{
    flex:1;
    text-align:end;
    width: auto;
    height: 30px;
  }

  .logo {
    width: auto;
    height: 30px;
  }

  .front {
    display: flex;
    flex-direction: column;
  }

  .title{
    font-size:2.5em;
    margin-bottom:0;
    padding-bottom:0;
    
  }

  .line{
    width:100%;
    background-color: #2D6BFA
  }

  .author{
    font-size:1.3em;
    font-weight: 700;
    margin-bottom: 0;
  }

  .company{
    font-size:.9em;
    margin-top: .1em;
  }

  blockquote{
    color:white;
    font-size: 16px;
    border-color:#2D6BFA;
    bottom: 70px;
    left: 30px;
    position: absolute;
  }

  a{
    background-color: rgb(45 107 250 / 30%);
    color: white;
    font-weight: bold;
    text-decoration: none;
  }

  a > code {
    background-color: rgb(45 107 250 / 30%);
  }


  code {
    background-color: rgb(255 255 255 / 30%);
  }


  tr {
    background: transparent!important;
  }

  .container-center {
    display: flex;
    place-content: center;
  }

  .container-image-col {
    display: flex;
    gap: 1rem;
    place-content: center;
    height: 100%;
    width: 100%;
  }

  .image-col {
    display: flex;
    width: 100%;
    place-content: center;    
  }

  .image-col > img {
    object-fit: contain;
  }

  .container-image {
    display: flex;
    place-content: center;
    max-height: 80%;
  }

  .summary{
    padding: 1rem;
    margin: 1rem;
    border-radius: 25px;
    background-color: rgb(255 255 255 / 10%);
  }

  .summary p {
    font-size: 18px;
    padding-bottom: 4px;
  }

  .resolve{
    padding: 1rem 1rem .5rem 1rem;
    margin: 1rem;
    border-radius: 25px;
    background-color: rgb(255 255 255 / 10%);
    font-size: 22px;
  }

  .small {
    font-size: 14px;
  }
---

  <!-- _paginate: skip -->

  <div class="front">
    <h1 class="title"> Git Básico </h1>
    <hr class="line"/>
    <p class="author">Arturo Silvelo</p>
    <p class="company">Try New Roads</p>
  </div>

---


# Ejercicio: Práctica de Merges en Git

---

## Objetivo
Practicar los tres tipos principales de merge en Git: Fast-forward, No Fast-forward y Squash.

---

# Merge

---

## Preparación

```bash
# Descomprimir y entrar al directorio
unzip git-merge-practice-ff.zip
cd git-merge-practice

# Verificar estado inicial
git log --oneline --graph --all
git branch -a
```

- Ejercicio 1: Fast Forward Merge
- ercicio 2: No Fast Forward Merge
- Ejercicio 3: Squash Merge


---

# Rebase Interactivo con Conflictos

---

## Preparación

```bash
unzip git-rebase-complete-practice.zip
cd git-rebase-complete-practice

```


## Estado inicial esperado:
```bash
abc123f F5: Add password validation function
def456g F4: Fix typo in console message  
ghi789h F3: Add user registration
jkl012i F2: Implement user login functionality
mno345j F1: WIP - Start login implementation
```

---

### Objetivo
Limpiar el historial de commits usando todas las operaciones de rebase interactivo.


### Resultado esperado:
- F1 eliminado (WIP)
- F2 y F3 combinados en un solo commit
- F4 eliminado (typo fix innecesario)
- F5 con mensaje mejorado

---

## Ejercicio 1: Realizar el rebase de main en feature

```
git branch
git switch feature/user-authentication
git log --oneline
```

---


## Ejercicio 2: Resolver Conflictos Durante Rebase

**CONFLICTOS ESPERADOS**

Durante el rebase aparecerán conflictos en `user-manager.js` porque:
- **Main** modificó la función
- **Feature** también tiene cambios en el mismo archivo

> Tip: Mover la funcion login dentro de la clase

---


## Ejercicio 3: Operaciones Específicas

**Squash - Combinar F2 y F3**
Cuando selecciones `squash` para F3, Git abrirá un editor para el mensaje:

**Mensaje sugerido:**
```
Implement complete user authentication system
```

---

### Reword - Mejorar mensaje de F5
Cambiar el mensaje de:
```
F5: Add password validation function
```

A algo más descriptivo:
```
Add comprehensive password validation
```

---

## Ejercicio 4: Verificación Final

### Comandos de verificación:
```bash
# Ver el historial final
git log --oneline --graph

```


### Resultado esperado final:
```bash
xyz789a Add comprehensive password validation
abc123b Implement complete user authentication system  
def456c (main) C4: Add user form styles
ghi789d C3: Improve email validation and add initialization
```

---

## Ejercicio 5: Integrar con Main

Llevar los cambios de la rama `feature/user-authentication` a `main` y limpiar el repositorio.

