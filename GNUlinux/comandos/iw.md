## `iw`

1. **`iw dev`**
   - **Descripción**: Muestra información sobre las interfaces inalámbricas.
   
   - **Ejemplo**:
   
```bash
iw dev
```

2. **`iw dev <interfaz> scan`**

   - **Descripción**: Escanea redes inalámbricas y muestra una lista de redes disponibles.
   - **Opciones**:
   
     - `-a`: Muestra solo redes activas.
     - `-f <archivo>`: Guarda el resultado del escaneo en un archivo.
   - **Ejemplo**:
   
```bash
iw dev wlan0 scan
iw dev wlan0 scan -a
```

3. **`iw dev <interfaz> connect <SSID>`**

   - **Descripción**: Conecta la interfaz inalámbrica al SSID especificado.
   - **Opciones**:
   
     - `key <clave>`: Especifica la clave WEP o WPA.
     - `--auth-alg <algoritmo>`: Define el algoritmo de autenticación (por ejemplo, `open` o `shared`).
     
   - **Ejemplo**:
   
```bash
iw dev wlan0 connect MiRed key s:MiClave
```

4. **`iw dev <interfaz> disconnect`**

   - **Descripción**: Desconecta la interfaz inalámbrica de la red actual.
   - **Ejemplo**:
   
```bash
iw dev wlan0 disconnect
```

5. **`iw dev <interfaz> set type <tipo>`**

   - **Descripción**: Establece el tipo de interfaz inalámbrica (modo).
   - **Tipos**:
   
     - `managed`: Modo cliente (por defecto).
     - `monitor`: Modo monitor (para capturar tráfico).
     - `ap`: Modo punto de acceso.
     
   - **Ejemplo**:
   
```bash
iw dev wlan0 set type monitor
```

6. **`iw dev <interfaz> set power_save <estado>`**

   - **Descripción**: Activa o desactiva el modo de ahorro de energía.
   - **Opciones**:
   
     - `on`: Habilita el ahorro de energía.
     - `off`: Desactiva el ahorro de energía.
     
   - **Ejemplo**:
   
```bash
iw dev wlan0 set power_save on
```

7. **`iw dev <interfaz> set txpower <nivel>`**

   - **Descripción**: Establece el nivel de potencia de transmisión.
   - **Opciones**:
   
     - `<nivel>`: Nivel de potencia en dBm.
     
   - **Ejemplo**:
   
```bash
iw dev wlan0 set txpower fixed 2000
```

8. **`iw dev <interfaz> set channel <canal>`**

   - **Descripción**: Establece el canal de la interfaz inalámbrica.
   - **Opciones**:
   
     - `<canal>`: Número del canal (por ejemplo, 1, 6, 11 para 2.4 GHz).
     
   - **Ejemplo**:
   
```bash
iw dev wlan0 set channel 6
```

9. **`iw dev <interfaz> set rts <tamaño>`**

   - **Descripción**: Establece el tamaño del umbral RTS (Request to Send).
   - **Opciones**:
   
     - `<tamaño>`: Tamaño en bytes.
     
   - **Ejemplo**:
   
```bash
iw dev wlan0 set rts 2347
```

10. **`iw dev <interfaz> set fragment <tamaño>`**

    - **Descripción**: Establece el tamaño del umbral de fragmentación.
    - **Opciones**:
    
      - `<tamaño>`: Tamaño en bytes.
      
    - **Ejemplo**:
    
```bash
iw dev wlan0 set fragment 2346
```

11. **`iw phy <phy>`**

    - **Descripción**: Muestra información sobre el hardware de la radio (phy).
    - **Opciones**:
    
      - `info`: Muestra información sobre el hardware de radio.
      - `channels`: Muestra los canales soportados.
      
    - **Ejemplo**:
    
```bash
iw phy phy0 info
iw phy phy0 channels
```

12. **`iw station <interfaz> info`**

    - **Descripción**: Muestra información sobre una estación (cliente) conectada.
    - **Opciones**:
    
      - `<dirección MAC>`: Dirección MAC de la estación.
      
    - **Ejemplo**:
    
```bash
iw station wlan0 info
```

13. **`iw txpower`**

    - **Descripción**: Muestra y configura el nivel de potencia de transmisión.
    - **Opciones**:
    
      - `info`: Muestra el nivel actual de potencia de transmisión.
      
    - **Ejemplo**:
    
```bash
iw dev wlan0 txpower info
```

14. **`iw config`**

    - **Descripción**: Configura la interfaz inalámbrica (similar a `iwconfig`).
    - **Opciones**:
    
      - `--mode <modo>`: Establece el modo de operación.
      - `--channel <canal>`: Establece el canal.
      
    - **Ejemplo**:
    
```bash
iw config wlan0 --mode managed --channel 6
```




