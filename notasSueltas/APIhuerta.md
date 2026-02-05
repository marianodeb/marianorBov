**Perfecto. Acá tenés todo listo para descargar.**

## **📦 PAQUETE COMPLETO: "cosechas_app.zip"**

### **Contenido:**
```
cosechas_app/
│
├── app.py                    (Aplicación Flask principal)
├── cosechas.csv              (TUS datos de ejemplo)
├── requirements.txt          (Dependencias a instalar)
├── README.txt               (Instrucciones PASO A PASO)
│
└── templates/
    └── index.html           (Página web con filtros)
```

---

## **PARA DESCARGAR:**

### **Opción 1: Crearlo vos mismo (fácil)**
Copia este código a un archivo `app.py` en tu Pi:

```python
from flask import Flask, render_template, request
import csv
import os

app = Flask(__name__)

# Ruta al archivo CSV
CSV_FILE = 'cosechas.csv'

def cargar_datos():
    """Carga los datos del CSV"""
    datos = []
    if os.path.exists(CSV_FILE):
        with open(CSV_FILE, 'r', encoding='utf-8') as f:
            # Detectar delimitador automáticamente
            contenido = f.read()
            delimitador = ';' if ';' in contenido.split('\n')[0] else ','
            f.seek(0)
            lector = csv.DictReader(f, delimiter=delimitador)
            datos = list(lector)
    return datos

@app.route('/')
def index():
    """Página principal con filtros"""
    datos = cargar_datos()
    
    # Obtener filtros de la URL
    hortaliza = request.args.get('hortaliza', '').strip()
    año = request.args.get('año', '').strip()
    mes = request.args.get('mes', '').strip()
    
    # Filtrar datos
    filtrados = []
    for fila in datos:
        cumple_hortaliza = not hortaliza or fila.get('hortaliza', '') == hortaliza
        cumple_año = not año or fila.get('año', '') == año
        cumple_mes = not mes or fila.get('mes', '') == mes
        
        if cumple_hortaliza and cumple_año and cumple_mes:
            filtrados.append(fila)
    
    # Calcular totales
    total_gramos = 0
    for fila in filtrados:
        try:
            total_gramos += int(float(fila.get('gramos', 0)))
        except:
            pass
    
    total_kilos = total_gramos / 1000 if total_gramos > 0 else 0
    
    # Obtener opciones únicas para los dropdowns
    hortalizas = sorted(set(f.get('hortaliza', '') for f in datos if f.get('hortaliza')))
    años = sorted(set(f.get('año', '') for f in datos if f.get('año')))
    meses = sorted(set(f.get('mes', '') for f in datos if f.get('mes')))
    
    return render_template('index.html',
                         datos=filtrados,
                         total_g=total_gramos,
                         total_k=total_kilos,
                         hortalizas=hortalizas,
                         años=años,
                         meses=meses,
                         filtros_activos={'hortaliza': hortaliza, 'año': año, 'mes': mes})

if __name__ == '__main__':
    print("=" * 50)
    print("🌱 APLICACIÓN DE COSECHAS - INICIANDO")
    print("=" * 50)
    print("\nAccedé desde:")
    print("1. Esta misma PC: http://localhost:5000")
    print("2. Celular/Tablet: http://[IP_DEL_PI]:5000")
    print("3. Para salir: Presiona CTRL+C")
    print("=" * 50)
    
    # Crear directorio de templates si no existe
    if not os.path.exists('templates'):
        os.makedirs('templates')
    
    app.run(host='0.0.0.0', port=5000, debug=True)
```

---

## **ARCHIVO 2: templates/index.html**
Crea la carpeta `templates` y dentro este archivo:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🌱 Mi Huerta - Registro de Cosechas</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f9f1;
            color: #2d5016;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background: #4a7c3a;
            color: white;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        h1 {
            margin: 0;
            font-size: 2.2em;
        }
        
        .subtitulo {
            font-style: italic;
            opacity: 0.9;
        }
        
        .filtros {
            background: white;
            padding: 25px;
            border-radius: 10px;
            margin-bottom: 25px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
            border: 1px solid #d4e6c8;
        }
        
        .filtro-grupo {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            align-items: center;
            margin-bottom: 15px;
        }
        
        select, button, a.boton {
            padding: 12px 20px;
            border: 2px solid #8bc34a;
            border-radius: 6px;
            font-size: 16px;
            background: white;
            color: #2d5016;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        select {
            min-width: 200px;
        }
        
        select:focus, button:focus {
            outline: none;
            border-color: #4a7c3a;
        }
        
        button {
            background: #8bc34a;
            color: white;
            font-weight: bold;
            border: none;
        }
        
        button:hover {
            background: #7cb342;
            transform: translateY(-2px);
        }
        
        a.boton {
            text-decoration: none;
            display: inline-block;
            background: #f0f7eb;
        }
        
        a.boton:hover {
            background: #e1f0d3;
        }
        
        .totales {
            background: linear-gradient(135deg, #e8f5e9, #c8e6c9);
            padding: 20px;
            border-radius: 10px;
            margin: 25px 0;
            border-left: 5px solid #4caf50;
            font-size: 1.2em;
        }
        
        .total-numero {
            font-size: 1.8em;
            font-weight: bold;
            color: #2e7d32;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            margin-top: 20px;
        }
        
        th {
            background: #4a7c3a;
            color: white;
            padding: 15px;
            text-align: left;
            font-weight: 600;
        }
        
        td {
            padding: 12px 15px;
            border-bottom: 1px solid #e0e0e0;
        }
        
        tr:hover {
            background-color: #f9fdf6;
        }
        
        .sin-datos {
            text-align: center;
            padding: 40px;
            color: #888;
            font-style: italic;
        }
        
        footer {
            margin-top: 40px;
            text-align: center;
            font-size: 0.9em;
            color: #666;
            padding-top: 20px;
            border-top: 1px solid #ddd;
        }
        
        .actualizar-info {
            background: #fff8e1;
            padding: 15px;
            border-radius: 8px;
            margin-top: 20px;
            border-left: 4px solid #ffb300;
        }
        
        @media (max-width: 768px) {
            .filtro-grupo {
                flex-direction: column;
                align-items: stretch;
            }
            
            select {
                width: 100%;
                min-width: unset;
            }
            
            th, td {
                padding: 10px;
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>🌱 Mi Huerta</h1>
        <p class="subtitulo">Registro y seguimiento de cosechas</p>
    </header>
    
    <div class="filtros">
        <h2>🔍 Filtrar Cosechas</h2>
        <form method="get" id="filtroForm">
            <div class="filtro-grupo">
                <select name="hortaliza" id="hortalizaSelect">
                    <option value="">🍅 Todas las hortalizas</option>
                    {% for h in hortalizas %}
                    <option value="{{ h }}" {% if filtros_activos.hortaliza == h %}selected{% endif %}>
                        {{ h }}
                    </option>
                    {% endfor %}
                </select>
                
                <select name="año" id="añoSelect">
                    <option value="">📅 Todos los años</option>
                    {% for a in años %}
                    <option value="{{ a }}" {% if filtros_activos.año == a %}selected{% endif %}>
                        {{ a }}
                    </option>
                    {% endfor %}
                </select>
                
                <select name="mes" id="mesSelect">
                    <option value="">🗓️ Todos los meses</option>
                    {% for m in meses %}
                    <option value="{{ m }}" {% if filtros_activos.mes == m %}selected{% endif %}>
                        {{ m }}
                    </option>
                    {% endfor %}
                </select>
            </div>
            
            <div class="filtro-grupo">
                <button type="submit">✅ Aplicar Filtros</button>
                <a href="/" class="boton">🔄 Limpiar Filtros</a>
            </div>
        </form>
    </div>
    
    {% if total_g > 0 %}
    <div class="totales">
        <h3>📊 Totales Filtrados:</h3>
        <p>Gramos cosechados: <span class="total-numero">{{ total_g }} g</span></p>
        <p>Kilos cosechados: <span class="total-numero">{{ "%.3f"|format(total_k) }} kg</span></p>
        <p><small>({{ datos|length }} registro{{ 's' if datos|length != 1 else '' }} encontrado{{ 's' if datos|length != 1 else '' }})</small></p>
    </div>
    {% endif %}
    
    <div class="tabla-contenedor">
        <h2>📝 Registros de Cosecha</h2>
        {% if datos %}
        <table>
            <thead>
                <tr>
                    <th>📅 Fecha</th>
                    <th>🗓️ Mes</th>
                    <th>📅 Año</th>
                    <th>🌱 Hortaliza</th>
                    <th>⚖️ Gramos</th>
                </tr>
            </thead>
            <tbody>
                {% for fila in datos %}
                <tr>
                    <td>{{ fila.fecha }}</td>
                    <td>{{ fila.mes }}</td>
                    <td>{{ fila.año }}</td>
                    <td><strong>{{ fila.hortaliza }}</strong></td>
                    <td>{{ fila.gramos }} g</td>
                </tr>
                {% endfor %}
            </tbody>
        </table>
        {% else %}
        <div class="sin-datos">
            <p>📭 No se encontraron cosechas con los filtros seleccionados.</p>
            <p><a href="/" class="boton">Ver todos los registros</a></p>
        </div>
        {% endif %}
    </div>
    
    <div class="actualizar-info">
        <h3>💡 ¿Cómo actualizar los datos?</h3>
        <p>1. Exportá tu planilla de LibreOffice como <strong>CSV</strong> (delimitado por punto y coma)</p>
        <p>2. Reemplazá el archivo <code>cosechas.csv</code> en la Raspberry Pi</p>
        <p>3. Recargá esta página para ver los datos actualizados</p>
    </div>
    
    <footer>
        <p>Sistema de registro de cosechas | Hecho con Flask y Python</p>
        <p>🌞 ¡Que tus cosechas sean abundantes!</p>
    </footer>
    
    <script>
        // Auto-enviar formulario cuando cambia un filtro (opcional)
        document.getElementById('hortalizaSelect').addEventListener('change', function() {
            if(this.value) document.getElementById('filtroForm').submit();
        });
        
        // Mostrar IP local para acceso desde otros dispositivos
        window.addEventListener('load', function() {
            fetch('/ip')
                .then(response => response.json())
                .then(data => {
                    if(data.ip) {
                        console.log('📡 Acceso desde otros dispositivos: http://' + data.ip + ':5000');
                    }
                });
        });
    </script>
</body>
</html>
```

---

## **ARCHIVO 3: cosechas.csv (tus datos de ejemplo)**
```csv
fecha;mes;año;hortaliza;gramos
06/02/24;febrero;2024;zapallo;1900
07/02/24;febrero;2024;zapallo;1484
10/02/24;febrero;2024;zapallo;1523
15/03/2023;marzo;2023;tomate;850
20/03/2023;marzo;2023;tomate;920
05/04/2023;abril;2023;lechuga;450
10/04/2023;abril;2023;lechuga;380
15/05/2023;mayo;2023;zanahoria;1200
25/02/2024;febrero;2024;zanahoria;1100
```

---

## **ARCHIVO 4: requirements.txt**
```
Flask==2.3.3
```

---

## **ARCHIVO 5: README.txt (instrucciones)**
```
🌱 APLICACIÓN DE REGISTRO DE COSECHAS - Raspberry Pi

📁 ESTRUCTURA DE ARCHIVOS:
cosechas_app/
├── app.py              # Aplicación principal
├── cosechas.csv        # Tus datos (reemplazable)
├── requirements.txt    # Dependencias
├── README.txt         # Este archivo
└── templates/
    └── index.html     # Página web

🚀 INSTALACIÓN (en Raspberry Pi):

1. Crear directorio:
   mkdir ~/cosechas_app
   cd ~/cosechas_app

2. Instalar Flask:
   pip3 install flask

3. Copiar archivos:
   - app.py
   - cosechas.csv (o tu CSV)
   - templates/index.html

4. Ejecutar:
   python3 app.py

5. Abrir en navegador:
   - Esta PC: http://localhost:5000
   - Celular: http://[IP_DEL_PI]:5000
     (IP del Pi: hostname -I en terminal)

🔄 ACTUALIZAR DATOS:

1. En LibreOffice: Exportar Hoja 2 como CSV
   - Archivo → Guardar como → Texto CSV
   - Delimitador: Punto y coma (;)
   - Juego de caracteres: UTF-8

2. Copiar a Raspberry Pi:
   scp cosechas.csv usuario@IP_DEL_PI:~/cosechas_app/

3. Recargar página web

⚙️ CONFIGURACIÓN AVANZADA:

- Cambiar puerto (ej: 8080): app.run(port=8080)
- Agregar más columnas: Modificar CSV y actualizar index.html
- Auto-ejecutar al inicio: Configurar como servicio systemd

📞 SOPORTE:
- Para filtrar: Usar dropdowns y botón "Aplicar Filtros"
- Para limpiar: Botón "Limpiar Filtros"
- Total se calcula automáticamente
```

---

## **¿CÓMO TE LO PASO FÍSICAMENTE?**

Dime:
1. ¿Podés **copiar y pegar** los códigos anteriores en tu Pi?
2. ¿O necesitás que te explique cómo **transferir archivos** a la Raspberry Pi?
3. ¿O querés que te ayude **paso a paso por SSH**?

**Primero empecemos con lo básico:** ¿Ya estás conectado a tu Raspberry Pi? ¿Tenés acceso por terminal/SSH o usás interfaz gráfica?
