# Documentación: Configuración de CI/CD con GitHub Actions

## Descripción del Proyecto

Este proyecto consiste en una página web sencilla de consultoría creada con HTML, CSS y JavaScript. Su objetivo es desplegar automáticamente esta aplicación estática cada vez que se realicen cambios (push) en la rama principal del repositorio de GitHub.

## Requisitos del Reto (Task 4)

- Simular una canalización CI/CD para desplegar una aplicación web básica.
- Usar una plataforma como GitHub Actions.
- Automatizar los pasos: test, build y deploy.
- Documentar el proceso completo, incluyendo scripts y archivos de configuración.

## Estructura del Proyecto

```
consultoria-site/
├── .github/
│   └── workflows/
│       └── deploy.yml          <- Archivo de configuración para GitHub Actions
├── index.html                 <- Página principal en HTML
├── styles.css                 <- Estilos en CSS
├── script.js                  <- Lógica en JavaScript (para este ejercicio no sera requerido)
├── README.md                  <- Descripción general del proyecto
└── documentacion.md           <- Documentación detallada del proceso CI/CD
```

## Plataforma usada

- **GitHub Actions**: herramienta integrada de GitHub que permite automatizar flujos de trabajo como pruebas, construcción y despliegue.


## Paso a Paso: Configuración de CI/CD

### Paso 1: Crear el Repositorio y subir el proyecto

1. Crear un repositorio nuevo en GitHub.
2. Subir los archivos básicos del proyecto (index.html, styles.css, script.js).

### Paso 2: Crear carpeta `.github/workflows`

# En Visual Studio Code:

- Crear una carpeta `.github` (con punto inicial).
- Dentro de esa carpeta, crear otra carpeta llamada `workflows`.

Ruta completa: `.github/workflows/`

### Paso 3: Crear el archivo `deploy.yml`

Este archivo configura el flujo de trabajo que se ejecutará automáticamente cada vez que se haga un push en `main`. Por Ejemplo:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ "main" ]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout código
        uses: actions/checkout@v4

      - name: Setup Pages
        uses: actions/configure-pages@v3

      - name: Subida a Pages
        uses: actions/upload-pages-artifact@v2
        with:
          path: '.'

      - name: Desplegar a GitHub Pages
        uses: actions/deploy-pages@v2
```

### Paso 4: Habilitar GitHub Pages en el repositorio

1. Ir a `Settings > Pages`
2. Seleccionar:
   - **Source**: GitHub Actions
3. Guardar los cambios.

### Paso 5: Realizar un `git push` y verificar el despliegue

Cada vez que se realice un  `git push`, GitHub ejecutará el flujo de trabajo. El sitio se publicará automáticamente y se mostrará la URL en la sección **Pages** del repositorio.


## Paso 6: Simulación de pasos de Test, Build y Deploy

En este punto la aplicación desarrollada es estática y no requiere compilación ni pruebas complejas, pero se simulara con los  pasos para cumplir con el flujo CI/CD completo:

name: Deploy Static Site

on:
  push:
    branches: [ "master" ]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout código fuente
        uses: actions/checkout@v4

      - name: Simular test
        run: echo "Ejecutando tests... (simulado)"

      - name: Simular build
        run: echo "Compilando el sitio... (simulado)"

      - name: Setup Pages
        uses: actions/configure-pages@v3

      - name: Subida de archivos a Pages
        uses: actions/upload-pages-artifact@v2
        with:
          path: '.'

      - name: Despliegue a GitHub Pages
        uses: actions/deploy-pages@v2


