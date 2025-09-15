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
    <img src="../../images/git-logo-white.png" alt="Logo Git"  class="logo"/>
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

# Trucos

---

## Git Cherry-pick

**Git Cherry-pick** permite aplicar un commit específico de otra rama a la rama actual, sin necesidad de fusionar toda la rama. Es útil para incorporar cambios puntuales sin mezclar todas las modificaciones de una rama.

**Uso básico:**

- Identifica el hash del commit que quieres aplicar (usualmente con `git log`).
- Ejecuta el comando:

```bash
git cherry-pick <commit-hash>
```

**Ejemplo:**
Si quieres aplicar el commit con el hash `abc1234` de una rama `feature` a tu rama actual, usarías:

```bash
git cherry-pick abc1234
```

**Nota:** Si hay conflictos durante el cherry-pick, tendrás que resolverlos manualmente antes de continuar con el proceso.

---

## Git Bisect - Introducción

**Git Bisect** es una herramienta que permite encontrar un commit específico que introdujo un error en el código utilizando una búsqueda binaria.

**Uso básico:**

- Inicia el bisecting con el comando:

```bash
git bisect start
```

- Marca un commit bueno y uno malo:

```bash
git bisect good <commit-hash>
git bisect bad <commit-hash>
```

Git hará una búsqueda binaria y te pedirá que marques cada commit como bueno o malo hasta encontrar el commit defectuoso.

---

## Git Bisect - Ejemplo y Finalización

**Ejemplo de uso:**
Si sabes que el último commit estaba funcionando y el actual no, puedes usar:

```bash
git bisect start
git bisect good <last-good-commit>
git bisect bad <current-commit>
```

**Finaliza el bisecting:**
Para salir del modo bisecting y volver al estado original:

```bash
git bisect reset
```

---

## Volver a la rama previa

En Git, para volver a la rama en la que estuviste trabajando antes de la rama actual, puedes utilizar dos métodos:

- **Usar el comando `git switch -`:**

```bash
git switch -
```

- **Usar `@{-1}` para la misma funcionalidad:**

```bash
git switch @{-1}
```

Ambos comandos permiten cambiar de vuelta a la rama donde estabas antes de hacer el último cambio, sin necesidad de recordar su nombre.

---

## Auto corrector

En Git, puedes habilitar una funcionalidad de auto-corrección para evitar errores tipográficos en los comandos. Esto se puede lograr con el siguiente comando:

- **Habilitar el auto-corrector:**

```bash
git config --global help.autocorrect 20
```

El valor `20` indica el número de décimas de segundo que Git esperará antes de intentar corregir automáticamente un error de comando. Si se introduce un comando incorrecto, Git lo corregirá automáticamente después de este tiempo. Puedes ajustar el valor según tus necesidades.

---

# Bibliografía

---

## Recomendaciones

Para profundizar en el uso de Git, recomendamos los siguientes recursos:

- **Aprendiendo Git: ¡Domina y comprende Git de una vez por todas!**  
  Un recurso práctico y completo para entender y dominar Git. Disponible en:  
  [https://leanpub.com/aprendiendo-git](https://leanpub.com/aprendiendo-git)

- **Pro Git (oficial):**  
  Libro oficial de Git, disponible de forma gratuita en múltiples idiomas.  
  [https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)
