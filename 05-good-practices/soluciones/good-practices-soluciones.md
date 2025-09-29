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

## Ejercicio 1

**Pre-commit hook:**
- Debe fallar si hay archivos muy grandes

<div class=small>

```bash
#!/bin/sh
# .git/hooks/pre-commit

echo "🔍 Ejecutando validaciones pre-commit..."

# Verificar que no hay archivos grandes
for file in $(git diff --cached --name-only); do
    if [ -f "$file" ]; then
        size=$(wc -c < "$file")
        if [ $size -gt 1048576 ]; then  # 1MB
            echo "❌ Archivo muy grande: $file ($size bytes)"
            echo "   Los archivos no pueden superar 1MB"
            exit 1
        fi
    fi
done

echo "✅ Validaciones pre-commit completadas"
exit 0
```

</div>

---

**Commit-msg hook:**
- Debe aceptar un formato especifico

<div class=small>

```bash
#!/bin/sh
# .git/hooks/commit-msg

commit_file="$1"
commit_msg=$(cat "$commit_file")

echo "📝 Validando mensaje de commit..."

# Verificar formato: tipo(scope): descripción
commit_pattern="^(feat|fix|docs|style|refactor|test|chore)(\(.+\))?: .{1,50}"

if ! echo "$commit_msg" | grep -qE "$commit_pattern"; then
    echo "❌ Formato de commit inválido"
    echo ""
    echo "Formato correcto:"
    echo "  tipo(scope): descripción"
    echo ""
    echo "Tipos válidos:"
    echo "  feat, fix, docs, style, refactor, test, chore"
    echo ""
    echo "Ejemplos:"
    echo "  feat(auth): add login functionality"
    echo "  fix: resolve memory leak in parser"
    echo ""
    exit 1
fi

echo "✅ Formato de commit válido"
exit 0
```

</div>

**Pre-push hook:**
- Debe rechazar push directo a main/master


<div class=small>

```bash
#!/bin/sh
# .git/hooks/pre-push

echo "🚀 Ejecutando validaciones pre-push..."

# Obtener rama actual
current_branch=$(git rev-parse --abbrev-ref HEAD)
echo "📍 Rama actual: $current_branch"

# Prevenir push directo a main/master
protected_branches="main master"
for branch in $protected_branches; do
    if [ "$current_branch" = "$branch" ]; then
        echo "❌ Push directo a '$branch' no permitido"
        echo "   Crea una rama de feature y usa Pull Request"
        exit 1
    fi
done

echo "✅ Push autorizado desde rama: $current_branch"
exit 0
```

</div>