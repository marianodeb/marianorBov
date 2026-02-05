### Uso de `frogmouth` en un sistema Live


### Instalación de `frogmouth` en un sistema Live

`frogmouth` es una herramienta de terminal para visualizar archivos Markdown (`.md`). Para instalarla en un sistema Live, sigue estos pasos:

1. **Asegúrate de tener `pip` instalado**:

   En la mayoría de los sistemas Live, `python3` y `pip` ya están instalados. Verifica si están disponibles ejecutando:
   
```bash
python3 --version
pip --version
```
   Si no están instalados, puedes instalarlos temporalmente (dependiendo de tu distribución).

2. **Instala `frogmouth` usando `pipx`**:

   Si no tienes `pipx` instalado, primero instálalo:
   
```bash
python3 -m pip install --user pipx
python3 -m pipx ensurepath
```
   Luego, instala `frogmouth`:
   
```bash
pipx install frogmouth
```

3. **Ejecuta `frogmouth`**:

   Una vez instalado, puedes abrir un archivo Markdown con:
   
```bash
frogmouth archivo.md
```

---

### Alternativas a `frogmouth`

Si no puedes instalar `frogmouth` o prefieres otras herramientas, aquí tienes algunas alternativas para visualizar archivos Markdown:

#### 1. **`glow`**

   - Es una herramienta de terminal para visualizar y navegar archivos Markdown.
   - Instalación:
   
```bash
pipx install glow
```
   - Uso:
   
```bash
glow archivo.md
```

#### 2. **`mdcat`**

   - Otra herramienta de terminal para visualizar Markdown.
   - Instalación:
   
```bash
pipx install mdcat
```
     
   - Uso:
   
```bash
mdcat archivo.md
```

#### 3. **`pandoc` + `lynx`**
   - `pandoc` convierte Markdown a texto plano, y `lynx` es un navegador de terminal.
   - Instalación:
   
```bash
sudo apt install pandoc lynx
```
     
   - Uso:
   
```bash
pandoc archivo.md | lynx -stdin
```

#### 4. **Editores de texto con soporte Markdown**

   - Algunos editores de texto tienen soporte integrado para Markdown:
     - **`micro`**:
     
```bash
sudo apt install micro
micro archivo.md
```
       
     - **`vim`** con el plugin `vim-markdown`:
     
```bash
sudo apt install vim
vim archivo.md
```

#### 5. **Herramientas gráficas (si estás en un entorno gráfico)**

   - **`ghostwriter`**: Un editor gráfico de Markdown.
   
```bash
sudo apt install ghostwriter
```
     
   - **`typora`**: Un editor de Markdown muy popular (no es de código abierto, pero es gratuito).

---

### Recomendación para sistemas Live

Dado que estás en un sistema Live, te recomiendo usar herramientas que no requieran instalación o que sean fáciles de instalar temporalmente. Por ejemplo:

- **`glow`** o **`mdcat`**: Son ligeras y fáciles de instalar con `pipx`.
- **`micro`**: Es un editor de texto con soporte Markdown que no requiere configuración adicional.


