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


# Ramas

----


## ¿Qué es una rama?

Una **rama** (branch) en Git es una línea de desarrollo independiente que permite:

- Trabajar en nuevas características sin afectar el código principal
- Experimentar con cambios de forma segura
- Colaborar en paralelo con otros desarrolladores
- Mantener un historial limpio y organizado

---

<div class="container-image">
  <img src="../../images/git_branch.png" alt="Git Branches" />
</div>

---

## Ventajas de usar ramas


- **Aislamiento**: Los cambios en una rama no afectan otras ramas
- **Experimentación**: Puedes probar ideas sin riesgo
- **Colaboración**: Múltiples desarrolladores pueden trabajar simultáneamente
- **Organización**: Cada característica o bug fix tiene su propia rama
- **Historial limpio**: Facilita el seguimiento de cambios



---

## Crear una rama

Para crear una nueva rama se pueden usar diferentes comandos

- Crear solo la rama (sin cambiar a ella)

    ```bash
    git branch feature
    ```
    Para cambiar a la rama creada:

    ```
    git switch feature
    # ó
    git checkout feature
    ```
---

- Crear la rama y cambiar a ella:

    ```bash
    git switch -c feature
    git checkout -b feature
    ```


- Crear rama desde un commit específico:

    ```bash
    git branch feature abc1234
    git switch -c feature abc1234
    ```

---

## Listar ramas

- Ver ramas locales:

    ```bash
    git branch
    ```
    La rama actual tendrá un asterisco al inicio.

- Ver todas las ramas (locales y remotas):

    ```bash
    git branch -a
    ```

---

- Ordenar por fecha de modificación:

    ```bash
    git branch --sort=-committerdate
    ```

- Ver información detallada:
    
    ```bash
    git branch -v
    ```


---

# Trabajando Con Ramas

---


## Escenario inicial

Tu equipo está trabajando en un proyecto y necesitan manejar múltiples tareas simultáneamente.

**Tareas a realizar:**

1. **Nueva característica**: Te asignan desarrollar `feature-1` 
2. **Bug crítico**: Durante el desarrollo encuentras un error que necesita solución inmediata
3. **Desarrollo paralelo**: Un compañero debe crear `feature-2` al mismo tiempo
4. **Segundo bug**: Se reporta otro error en la aplicación principal mientras todos trabajan

---

### Cargar el nivel

1. [Learn Git Branching](https://learngitbranching.js.org/?NODEMO) 
2. Escribimos `import level`
3. Copiamos el fichero `ejercicios_1.json` y lo pegamos.

---

<div class="container-image">
  <img src="../../images/git_branch_ex.png" alt="Git Branches" />
</div>


---

# Fusionar Ramas

---

## ¿Qué es fusionar (merge)?

**Fusionar** es el proceso de **integrar los cambios** de una rama en otra rama.

- Los commits de la rama origen se incorporan a la rama destino
- Se crea un historial unificado
- Permite combinar el trabajo de diferentes desarrolladores
- Mantiene la trazabilidad de los cambios

---

- Comando básico de fusión

    ```
    git merge <rama-origen>
    ```

    Ejemplo:

    ```bash
    # 1. Cambiar a la rama destino
    git switch main

    # 2. Fusionar la rama feature
    git merge feature-1
    ```

<div >
💡 <strong>Importante:</strong> Siempre debes estar en la rama destino antes de hacer merge
</div>

---

## Tipos de merge

---

## Fast-forward

- Cuando no hay commits nuevos en la rama destino
- Simplemente mueve el puntero hacia adelante

``` bash
git merge --ff-only my-branch
```

---

<div class="container-image-col ">

<div class="image-col">
  <img src="../../images/git_merge_ff_1.png" alt="Git Branches" />
</div>

<div class="image-col">


```bash
# Creamos la nueva rama
git switch -c feature

# Añadimos cambios
git commit
git commit
git commit

# Volvemos a la rama principal
git switch main

# Fusionamos las ramas
git merge --ff-only feature 

# ó
git merge feature

```
</div>



<div class="image-col">
  <img class="image-col" src="../../images/git_merge_ff_2.png" alt="Git Branches" />
</div>
</div>

---


## No Fast-forward

- Cuando ambas ramas tienen commits nuevos
- Crea un commit de fusión que une ambas historias
- Preserva la estructura de ramas en el historial

``` bash
git merge --no-ff my-branch
```

---

<div class="container-image-col ">

<div class="image-col">
  <img src="../../images/git_merge_no_ff_1.png" alt="Git Branches" />
</div>

<div class="image-col">


```bash
# Creamos la nueva rama
git switch -c feature

# Añadimos cambios
git commit
git commit
git commit

# Volvemos a la rama principal
git switch main

# Añadimos cambios
git commit
git commit
git commit

# Fusionamos las ramas
git merge --no-ff feature 

# ó
git merge feature

```
</div>



<div class="image-col">
  <img src="../../images/git_merge_no_ff_2.png" alt="Git Branches" />
</div>
</div>

---

## Squash Merge

- Combina todos los commits de una rama en un solo commit
- Crea un historial más limpio y lineal
- Útil cuando la rama tiene muchos commits pequeños o experimentales

```bash
git merge --squash feature
git commit -m "Add complete feature X"
```

---

<div class="container-image-col ">

<div class="image-col">
  <img src="../../images/git_merge_squash_1.png" alt="Git Merge Squash Before" />
</div>

<div class="image-col">

```bash
# Creamos la nueva rama
git switch -c feature

# Añadimos múltiples commits
git commit -m "F1"
git commit -m "F2"
git commit -m "F3"

# Volvemos a main
git switch main

# Squash merge: combina todos en uno
git merge --squash feature
git commit -m "Feature Complete"
git commit -m "C3"
```

</div>

<div class="image-col">
  <img src="../../images/git_merge_squash_2.png" alt="Git Merge Squash After" />
</div>

</div>

---

## Personalizar mensajes de merge

Puedes modificar el mensaje de un merge usando `--edit` y `--no-commit`:

- **`--edit`**: Abre el editor para modificar el mensaje automático
- **`--no-commit`**: Realiza el merge sin crear el commit automáticamente

---

## Comportamiento por tipo de merge

**Fast-forward merge:**
```bash
git merge --edit feature          # ❌ No funciona (no hay commit de merge)
git merge --no-commit feature     # ✅ Evita fast-forward, deja cambios en staging
```
---

**No Fast-forward merge:**
```bash
git merge --edit --no-ff feature     # ✅ Abre editor para mensaje
git merge --no-commit --no-ff feature # ✅ Prepara merge sin commitear
```

---

**Squash merge:**
```bash
git merge --squash feature           # ✅ Siempre requiere commit manual
git merge --squash --edit feature    # ✅ Redundante (ya controlas el mensaje)
```

---

## Ejemplos prácticos


- git merge --edit --no-ff feature

<div class="container-image-col ">

<div class="image-col">
  <img src="../../images/git_merge_edit_no_ff.png" alt="Git Merge Squash Before" />
</div>


<div class="image-col">
  <img src="../../images/git_merge_edit_no_ff_edit.png" alt="Git Merge Squash After" />
</div>

</div>



---

- git merge --no-commit --no-ff feature 




<div class="container-image">
  <img src="../../images/git_merge_no_commit.png" alt="Git Merge Squash Before" />
</div>


---

- git merge --squash feature

<div class="container-image">
  <img src="../../images/git_merge_squash.png" alt="Git Merge Squash Before" />
</div>

---

<div class="container-image">
  <img src="../../images/git_merge_commit_logs.png" alt="Git Merge Squash Before" />
</div>

