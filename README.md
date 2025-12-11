# Portafolio Personal

Portafolio web desarrollado con Vue 3 + Vite y TailwindCSS.

## 🚀 Clonar e Instalar

### 1. Clonar el repositorio
```bash
git clone https://github.com/OrtegaNidddd/OrtegaNidddd.github.io.git
cd OrtegaNidddd.github.io
```

### 2. Instalar dependencias
```bash
npm install
```

### 3. Ejecutar en modo desarrollo
```bash
npm run dev
```

La aplicación estará disponible en `http://localhost:5173`

## 📦 Deploy a GitHub Pages

Este proyecto usa una rama separada (`gh-pages` o similar) para el deployment, donde solo se incluyen los archivos compilados.

### Proceso de Deploy

1. **Compilar el proyecto**
   ```bash
   npm run build
   ```
   Esto genera una carpeta `dist/` con los archivos compilados.

2. **Crear/cambiar a la rama de deploy** (si no existe)
   ```bash
   git checkout -b gh-pages
   ```
   O si ya existe:
   ```bash
   git checkout gh-pages
   ```

3. **Mover archivos de dist a la raíz**
   ```bash
   # En Windows (Git Bash)
   cp -r dist/* .
   
   # O manualmente:
   # - Copia todo el contenido de la carpeta dist/ a la raíz del proyecto
   ```

4. **Eliminar la carpeta dist vacía**
   ```bash
   rm -rf dist
   ```

5. **Agregar archivo CNAME (opcional)**
   Si tienes un dominio personalizado, crea un archivo `CNAME` en la raíz:
   ```bash
   echo "tudominio.com" > CNAME
   ```

6. **Commit y push**
   ```bash
   git add .
   git commit -m "Deploy: Update build"
   git push origin gh-pages
   ```

7. **Configurar GitHub Pages**
   - Ve a Settings > Pages en tu repositorio
   - Selecciona la rama `gh-pages` como fuente
   - Guarda los cambios

### ⚠️ Importante
- La rama `main` contiene el código fuente del proyecto
- La rama `gh-pages` (o la que uses para deploy) solo debe contener los archivos compilados
- No hagas cambios de código en la rama de deploy, siempre trabaja en `main`

## 🛠️ Tecnologías

- Vue 3
- Vite
- TailwindCSS
- EmailJS
