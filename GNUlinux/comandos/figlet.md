### `figlet` 

```
  _____    __    __    ___  _  _     ___   ___   _      ___  _____  ___  ___ 
 |  _  \  |  \  /  |  /   || || |   / _ \ | _ \ | |    |_  ||  _  || __|| _ \
 | |_| |  |   \/   | / /| || || |_ | | | ||  _/ | |__    | || | | || __||  _/
 |  ___/  | |\  /| |/ /_| || ||  _|| | | || |   |____|   | || | | || |_ | |  
 | |      | | \/ | |\___  ||_|| |  | |_| || |    ___     | || |_| || __|| |  
 |_|      |_|    |_|    |_|   |_|   \___/ |_|   |___|   _|_||_____||_|  |_|  
```

### **Definición y Significado**

`figlet` es una herramienta de línea de comandos que convierte texto **en ASCII art**, generando letras grandes con caracteres. Es útil para crear banners, títulos llamativos o decorar terminales.

---

### **Sintaxis Básica**

```bash
figlet [opciones] "texto"
```

---

### **Todas sus Opciones**

Principales opciones (ver más con `man figlet`):  

| Opción          | Descripción                                  |
|-----------------|---------------------------------------------|
| `-f <fuente>`   | Usa una fuente específica (ej: `slant`, `block`). Lista con `figlet -l`. |
| `-d <directorio>`| Directorio alternativo de fuentes.           |
| `-c`            | Centra el texto.                             |
| `-l`            | Alinea a la izquierda (por defecto).         |
| `-r`            | Alinea a la derecha.                         |
| `-w <ancho>`    | Establece ancho de salida (en columnas).     |
| `-k`            | Kerning: ajusta espacio entre caracteres.    |
| `-t`            | Modo terminal: ajusta automáticamente al ancho. |

---

### **Ejemplos**

#### **1. Simple**

```bash
figlet "Hola"
```

Salida:

```
 _   _      _ _    
| | | | ___| | | __
| |_| |/ _ \ | |/ /
|  _  |  __/ |   < 
|_| |_|\___|_|_|\_\
```

#### **2. Con Fuente Personalizada**

```bash
figlet -f slant "Linux"
```
Salida:
```
    __   _ __     _ 
   / /  (_) /____| |
  / /__/ / __/ -_) |
 /____/_/\__/\__/_| 
```

#### **3. Alineación y Ancho**

```bash
figlet -w 40 -c "Bienvenido"
```

---

### **Consejos**  
- **Fuentes disponibles**: Usa `figlet -l` para listar +400 fuentes.  
- **Guardar en archivo**: Redirige la salida:

```bash
figlet "Hola" > salida.txt
```
- **Combina con `cowsay`**: Para crear arte ASCII más divertido.  

---

### **Información Adicional**

- **Instalación**:

  - Debian/Ubuntu: `sudo apt install figlet`  
  - Fedora: `sudo dnf install figlet`  
  - macOS: `brew install figlet`  

- **Alternativas**: `toilet` (similar con más estilos).  

---

## `figlet`, `toilet`, `cowsay` y `boxes`


### **`cowsay`**

**¿Qué hace?**

Genera un **ASCII art de una vaca** (u otro animal/personaje) con un mensaje en un bocadillo de diálogo.

**Características**:

- Mensajes en globos de texto.  
- Varios personajes (vaca, dragón, tux, etc.).  
- Personalización del globo (tamaño, ojos, lengua).  

**Ejemplo**:

```bash
cowsay "Hola, soy una vaca filosófica"
```

Salida:

```
 _________________________________
< Hola, soy una vaca filosófica >
 ---------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

---

### **`boxes`**

**¿Qué hace?**

Envuelve el texto en **marcos decorativos** (como cajas, globos, o diseños artísticos).

**Características**:

- +100 plantillas de marcos (ver con `boxes -l`).  
- Ideal para destacar bloques de texto o código.  
- Soporta personalización avanzada de bordes.  

**Ejemplo**:

```bash
echo "Texto importante" | boxes -d dog
```

Salida:

```
  /-------\  
 < Texto  |
  \ importante /
   \_______/  
```

---

### **`figlet` vs `toilet`**

Ambos generan **texto grande en ASCII**, pero:

- **`figlet`**: Más simple, centrado en fuentes clásicas.  
- **`toilet`**: Incluye colores, efectos y filtros (ej: `--gay`, `--metal`).  

---

### **Tabla Comparativa**

| Comando   | Enfoque Principal         | Personalización          | Color | Interactividad |  
|-----------|---------------------------|--------------------------|-------|----------------|  
| `figlet`  | Texto grande en ASCII     | Fuentes básicas          | No    | No             |  
| `toilet`  | Texto con estilo/color    | Fuentes + filtros + ANSI | Sí    | No             |  
| `cowsay`  | Diálogos con animales     | Personajes y globos      | No*   | No             |  
| `boxes`   | Marcos decorativos        | Plantillas de bordes     | No*   | No             |  


*Nota*: `cowsay` y `boxes` no usan colores por defecto, pero pueden combinarse con `lolcat`.

---

### **¿Cuándo usar cada uno?**

1. **Banners llamativos**: `toilet` (con colores) o `figlet`.  
2. **Mensajes con humor**: `cowsay` (ej: en scripts para errores).  
3. **Documentación o código**: `boxes` para enmarcar textos.  
4. **Efectos psicodélicos**: Combina cualquier comando con `lolcat`.  

---

### **Ejemplo de Combinación**

```bash
toilet -f pagga "Hacked" | boxes -d parchment | lolcat -a
```

*(Un mensaje "Hacked" con fuente artística, marco de pergamino y colores animados)*.

---

### ⚙️ **Instalación**

- **`cowsay`**:

```bash
sudo apt install cowsay
```
  
- **`boxes`**:

```bash
sudo apt install boxes
```




