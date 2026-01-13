## **jq**

### **Definición y Significado**

**jq** es un procesador de línea de comandos especializado en manipular y transformar datos JSON. Su nombre proviene de "JSON Query", aunque su funcionalidad va más allá de consultas, permitiendo operaciones como filtrado, mapeo, modificación y formateo de JSON. Es comparado con herramientas como `sed` o `awk` por su eficiencia en el procesamiento de texto estructurado .  

Su uso principal incluye:

- **Formatear JSON** para mejorar su legibilidad.  
- **Extraer valores específicos** de objetos o arrays.  
- **Transformar estructuras JSON** (renombrar campos, combinar datos, etc.).  
- **Integración en scripts** para automatizar tareas con APIs o archivos JSON .  

---

### **Sintaxis Básica**

La estructura general del comando es:

```bash
jq [opciones] 'filtro' [archivo.json]
```

- **`filtro`**: Define la operación a realizar (ej: `.` para identidad, `.clave` para acceder a un campo).  
- **`archivo.json`**: Archivo de entrada (opcional; si no se especifica, lee desde `stdin`).  

Ejemplo básico:

```bash
jq '.' datos.json  # Formatea el JSON
```  
Si el JSON viene de una tubería:  
```bash
curl https://api.ejemplo.com/datos | jq '.'  
```

---

### **Opciones Principales**

Algunas opciones útiles :

| Opción | Descripción |  
|--------|-------------|  
| `-r`   | Salida en texto plano (sin comillas). |  
| `-c`   | Salida compacta (sin indentación). |  
| `-s`   | Leer todo el input como un solo array. |  
| `--arg nombre valor` | Pasar variables al filtro. |  
| `-S`   | Ordenar claves de objetos. |  
| `-e`   | Establecer código de salida según el resultado. |  

Ejemplo con opciones:

```bash
jq -r '.usuarios[].nombre' datos.json  # Lista nombres sin comillas
```

---

### **Ejemplos**

#### **Simples**

1. **Extraer un campo**:

```bash
jq '.trabajadores[0].Nombre' empleados.json  
# Salida: "Armando Guerra" 
```

2. **Iterar sobre un array**:

```bash
jq '.frutas[].nombre' frutas.json  
# Salida: "manzana", "plátano", "kiwi" 
```

#### **Complejos**

1. **Filtrar elementos con condiciones**:

```bash
jq '.[] | select(.precio > 1)' productos.json  
# Filtra productos con precio mayor a 1 
```

2. **Transformar estructura**:  
```bash
jq 'map({user_id: .id, userDetails: {name: .nombre, email: .correo}})' usuarios.json  
# Crea una nueva estructura combinando campos 
```

3. **Calcular promedio**:

```bash
jq '[.[].edad] | add / length' datos.json  
# Calcula la edad promedio 
```

---

### **Consejos Prácticos**

1. **Usa comillas simples** para evitar conflictos con el shell:

```bash
jq '.clave'  # Correcto  
jq ".clave"  # Incorrecto (en Unix) 
```

2. **Combina con `curl`** para procesar respuestas de APIs:

```bash
curl https://api.github.com/users/octocat/repos | jq '.[].name'  
```

3. **Manejo de errores**:

- Usa `//` para valores por defecto:

```bash
jq '.clave // "valor_faltante"' datos.json  
```

4. **Funciones integradas**:

- `keys`, `length`, `map`, `select`, `has`, etc. .  

---

### **Información Adicional**

- **Recursos**:

  - **Documentación oficial**: [Manual de jq](https://jqlang.org/manual) .  
  - **Playground en línea**: [jqplay.org](https://jqplay.org/) para probar filtros .
  
- **Instalación**:

  - Linux: `sudo apt install jq`  
  - macOS: `brew install jq` .  
- **Comunidad**: Soporte en Stack Overflow (etiqueta `jq`) o Discord .  




