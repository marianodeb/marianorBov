## **Comando `bg`**

`bg` es un comando integrado en shells como Bash o Zsh que **reanuda trabajos (jobs) detenidos** en segundo plano (*background*). Permite continuar la ejecución de procesos que fueron pausados (por ejemplo, con `Ctrl + Z`), liberando la terminal para seguir trabajando.  

**Ejemplo básico:** 
 
Si detienes un proceso con `Ctrl + Z`, `bg` lo reanudará en segundo plano sin bloquear la terminal.

---

#### **¿Cómo utilizarlo?**  

- **Propósito principal:**  
  - Reanudar procesos detenidos para que se ejecuten en segundo plano.  
  - Gestionar múltiples trabajos en una misma sesión de terminal.  
- **Casos de uso:**  
  - Continuar un proceso largo (ej: descargas o compilaciones) sin perder control de la terminal.  
  - Alternar entre trabajos con `fg` (primer plano) y `bg` (segundo plano).  

---

#### **Sintaxis**  

```bash
bg [%job_id]
```

#### **Parámetros clave**  
| Parámetro | Descripción                                                                 |
|-----------|-----------------------------------------------------------------------------|
| `%job_id` | Identificador del trabajo a reanudar (ej: `%1`). Si se omite, usa el último trabajo detenido. |  

---

#### **Ejemplos**  

1. **Reanudar el último trabajo detenido**  

```bash
# Paso 1: Iniciar un proceso (ej: sleep 100).
# Paso 2: Presionar Ctrl + Z para detenerlo.
bg
```
   
**Salida:**  
   
```
[1]+ sleep 100 &
```

2. **Reanudar un trabajo específico por ID**  

```bash
# Listar trabajos detenidos:
jobs
# Salida: [1]-  Detenido          ping google.com
#         [2]+  Detenido          sleep 500

bg %1  # Reanuda el trabajo 1 (ping google.com).
```

**Salida:**  

```
[1]- ping google.com &
```

3. **Reanudar múltiples trabajos**  

```bash
bg %1 %2  # Reanuda los trabajos 1 y 2.
```

4. **Usar `bg` en un script**  

```bash
sleep 300 &
sleep 400
# Presionar Ctrl + Z para detener sleep 400.
bg  # Reanuda sleep 400 en segundo plano.
```

---

#### **Notas importantes**  

- **Trabajos vs. procesos:**  

  - Los "trabajos" son procesos asociados a la sesión actual de la terminal.  
  - Si cierras la terminal, los trabajos en segundo plano se terminan.  
  
- **Comandos relacionados:**  

  - `jobs`: Lista trabajos activos o detenidos.  
  - `fg`: Mueve un trabajo a primer plano.  
  - `kill %n`: Termina un trabajo (ej: `kill %1`).  

---

#### **Consejos**  

- **Verificar el estado de trabajos:**  

```bash
jobs -l  # Muestra IDs y estados (detenidos, en segundo plano, etc.).
```
  
- **Evitar bloqueos:**  

  Si un trabajo en segundo plano intenta leer entrada, se pausará automáticamente. Usa `fg` para traerlo a primer plano y completar la acción.  
  
- **Desvincular trabajos de la terminal:**  

  Usa `disown` o `nohup` para que sigan ejecutándose incluso al cerrar la terminal:  
  
```bash
bg %1
disown %1
```

---

### **Flujo de trabajo típico**  

1. Inicias un proceso largo (ej: `tar -czf backup.tar.gz /datos`).  
2. Lo detienes con `Ctrl + Z`.  
3. Ejecutas `bg` para reanudarlo en segundo plano.  
4. Usas `jobs` para verificar su estado.  
5. Si necesitas interactuar con él, usas `fg %n`.  

```bash
# Ejemplo completo:
tar -czf backup.tar.gz /datos  # Inicia compresión.
^Z                             # Detener con Ctrl + Z.
bg                             # Reanudar en segundo plano.
jobs                           # Verificar estado.
```
