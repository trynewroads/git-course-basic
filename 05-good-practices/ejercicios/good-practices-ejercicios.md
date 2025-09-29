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

# Ejercicios Prácticos
## Git Hooks y CI/CD

---

## Objetivos

Al finalizar estos ejercicios serás capaz de:

- Entender el problema de los hooks nativos de Git
- Configurar hooks nativos en `.git/hooks/`
- Implementar hooks con Husky
- Comparar ambas soluciones
- Configurar GitHub Actions para CI/CD

---

## Ejercicio 1: Hooks Nativos
### Explorando el problema

**Archivos necesarios:** `hooks.zip`

1. **Extraer y explorar:**
```bash
unzip hooks.zip
cd hooks-ejemplo
ls -la .git/hooks/
```

2. **Probar los hooks:**
```bash
# Restaurar permisos (se pierden al comprimir)
chmod +x .git/hooks/*
```

---

## Ejercicio 1: Resultados esperados

**Pre-commit hook:**
- Debe fallar si hay archivos muy grandes


**A. Probar Pre-commit (archivos grandes):**
```bash
# Crear archivo muy grande para probar
dd if=/dev/zero of=archivo-grande.txt bs=2M count=1
git add archivo-grande.txt
git commit -m "add large file"
# ebe fallar por tamaño
```

---

**Commit-msg hook:**
- Debe aceptar un formato especifico

```bash
# Crear cambio pequeño
echo "cambio menor" >> README.md
git add README.md

# Intentar con formato incorrecto
git commit -m "mensaje mal formateado"
# Debe fallar por formato
```

---

**Pre-push hook:**
- Debe rechazar push directo a main/master 
- Obtener la rama actual: `git rev-parse --abbrev-ref HEAD`

```bash
# Asegurar que estamos en main
git switch main

# Crear cambio y commit
echo "cambio en main" >> README.md
git add README.md
git commit -m "feat: change in main"

# Intentar push directo a main
git push origin main
```

---

## Ejercicio 2: Hooks con Husky

**Archivos necesarios:** `hooks-husky.zip`

1. **Extraer y configurar:**
```bash
unzip hooks-husky.zip
cd hooks-husky-ejemplo
npm install  # Instala Husky automáticamente
```

2. **Explorar configuración:**
```bash
# Ver configuración en package.json
cat package.json

# Ver hooks instalados
ls -la .husky/
```