

## `cal`

### **1. Instalación**  
- **Por defecto**: Viene preinstalado en sistemas Unix/Linux (parte del paquete `util-linux`).  
- **Si no está instalado**:  
  - **Debian/Ubuntu**:
  
```bash
sudo apt update && sudo apt install ncal  # Incluye cal y ncal
```
  - **Otras distribuciones**:
  
```bash
sudo dnf install util-linux  # Red Hat/Fedora
```

### **2. Definición y significado** 
 
- **Nombre**: `cal` = *calendar*.  
- **Propósito**: Muestra calendarios en la terminal usando el calendario gregoriano (predeterminado) o juliano.  
- **Historia**: Creado en 1975 (Unix V6) para consultas rápidas de fechas.

### **3. Sintaxis**  

```bash
cal [OPCIONES] [[[DÍA] MES] AÑO]
```

Ejemplo:  

```bash
cal 12 2025      # Diciembre 2025
cal --reform 1752 9  # Septiembre 1752 (cambio histórico)
```

### **4. Todas las opciones**  

| **Opción**      | **Descripción**                                                                 |
|------------------|---------------------------------------------------------------------------------|
| `-1`             | Muestra un solo mes (predeterminado).                                          |
| `-3`             | Muestra mes actual, anterior y siguiente.                                      |
| `-j`             | Formato juliano (días numerados del 1 al 365/366).                             |
| `-m`             | Lunes como primer día de la semana.                                            |
| `-s`             | Domingo como primer día (predeterminado).                                      |
| `-y`             | Muestra el calendario de todo el año actual.                                   |
| `--iso`          | Usa calendario ISO 8601 (semana 1 contiene el 4 de enero).                     |
| `-w`             | Muestra números de semana (solo en `ncal`).                                    |
| `--reform [AÑO]` | Define el año de adopción del calendario gregoriano (ejemplo: `--reform 1752`).|


### **5. Ejemplos**  

#### **Simples**: 
 
```bash
cal          # Mes actual
cal -3       # Tres meses (pasado, actual, futuro)
cal -y 2030  # Año completo 2030
cal -j 2     # Febrero actual en días julianos
```

#### **Complejos**: 
 
- **Resaltar un día específico**:  

```bash
cal | sed "s/$(date +%e)/\033[1;31m&\033[0m/"  # Día actual en rojo
```

- **Verificar año bisiesto**:  

```bash
cal 2 2024 | grep -q "29" && echo "Bisiesto" || echo "No bisiesto"
```

- **Calendario histórico**:  

```bash
cal 9 1752  # Septiembre 1752 (11 días eliminados)
```

### **6. Consejos**  

- **Usa `ncal`**: Para formato vertical y opciones extendidas:  

```bash
ncal -wM  # Semanas numeradas y lunes como inicio
```

- **Integra en scripts**: Ejemplo para obtener el último día del mes:  

```bash
ultimo_dia=$(cal 12 2023 | awk 'NF {print $NF}' | tail -1)
```

- **Combina con `grep` o `awk`**: Para filtrar fechas o días específicos.

### **7. Información adicional**  

- **Curiosidad histórica**: En 1752, Gran Bretaña eliminó 11 días (del 3 al 13 de septiembre) al adoptar el calendario gregoriano.  
- **Alternativas modernas**:  
  - **`gcal`**: Calendario con soporte para festivos y eventos.  
  - **`khal`/`calcurse`**: Gestores interactivos de eventos y tareas.  
- **Comandos relacionados**:  
  - `date`: Muestra o establece la fecha/hora.  
  - `ncal`: Versión alternativa con formato vertical.  

### **8. Detalles técnicos**  

- **Formato de salida**: Por defecto, `cal` ajusta el calendario al ancho de la terminal.  
- **Límites de años**: Soporta años desde 1 hasta 9999, pero puede variar por implementación.  
- **Soporte para calendario juliano**: Usa `-j` para días numerados desde el 1 de enero.

### **9. Errores comunes** 
 
- **Orden incorrecto**: 
 
```bash
cal 2025 12  # Error: debe ser cal [mes] [año]
cal 12 2025  # Correcto
```

- **Años fuera de rango**: Algunas versiones no aceptan años < 1 o > 9999.

### **10. Sustitutos y herramientas avanzadas**  

| **Herramienta** | **Uso**                                                                 |
|------------------|-------------------------------------------------------------------------|
| **`gcal`**       | Calendario con festivos, eventos y soporte multi-idioma.               |
| **`khal`**       | Gestor de calendarios (CLI) compatible con CalDAV.                     |
| **`calcurse`**   | Calendario interactivo con recordatorios y tareas.                     |



