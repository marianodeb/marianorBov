
##  GUÍA : TypeScript en Debian

## Índice de la Nota
1. [¿Qué es cada cosa? (Explicación Simple)](#1-qué-es-cada-cosa-explicación-simple)
2. [¿Qué significa "instalar local/global"?](#2-qué-significa-instalar-localglobal)
3. [Instalación Paso a Paso en Debian](#3-instalación-paso-a-paso-en-debian)
4. [Explicación de Herramientas Adicionales](#4-explicación-de-herramientas-adicionales)
5. [Primer Proyecto TypeScript](#5-primer-proyecto-typescript)
6. [Comandos Esenciales para tu Día a Día](#6-comandos-esenciales-para-tu-día-a-día)
7. [Solución de Problemas Comunes](#7-solución-de-problemas-comunes)



### 1. ¿Qué es cada cosa? (Explicación Simple)

####  **Node.js**

**¿Qué es?** Es un programa que permite ejecutar JavaScript **fuera del navegador** (en tu computadora).

**¿Para qué lo necesitas?** TypeScript se convierte a JavaScript, y luego **Node.js ejecuta** ese JavaScript. Sin Node.js no podrías probar tu código TypeScript.

**Analogía:** Node.js es como el "motor" que hace funcionar tu código JavaScript, igual que un navegador lo hace en internet.



####  **npm (Node Package Manager)**

**¿Qué es?** Es una tienda de herramientas (paquetes) para JavaScript/TypeScript que viene con Node.js.

**¿Para qué lo necesitas?** 

- Para instalar TypeScript
- Para instalar librerías que tu código necesite
- Para gestionar las versiones de las herramientas

**Analogía:** Es como la "tienda de aplicaciones" pero para código.



#### **TypeScript**

**¿Qué es?** Es JavaScript con "superpoderes": puedes decirle qué tipo de datos esperas (números, textos, etc.) y te avisa si cometes errores.

**¿Para qué lo necesitas?** 
- Para escribir código más seguro y con menos errores
- Para que el editor te ayude con autocompletado
- Para trabajar en equipos grandes

**Analogía:** Es como escribir con corrector ortográfico vs escribir sin él.



####  **Relación entre ellos**

```text
Tú escribes → Código TypeScript (.ts)
                  ↓
TypeScript lo convierte → Código JavaScript (.js) 
                  ↓
Node.js lo ejecuta → Resultado en pantalla
```

**npm** es el que te da TypeScript y otras herramientas.

### 2. ¿Qué significa "instalar local/global"?

Esta es una de las dudas más comunes. Te lo explico con ejemplos:

####  **Instalación Global** (`-g`)

**¿Qué significa?** Instalas la herramienta **una sola vez** en tu sistema y está disponible para **todos** tus proyectos.

**¿Cuándo usarla?** Para herramientas que usas en **cualquier proyecto**, como:
- El compilador de TypeScript (`tsc`)
- Herramientas de línea de comandos

**Ejemplo:**

```bash
sudo npm install -g typescript
# Ahora puedes usar "tsc" en cualquier carpeta
```

**Ventaja:** No tienes que instalar TypeScript en cada proyecto.
**Desventaja:** Todos tus proyectos usan la misma versión.

#### **Instalación Local** (sin `-g`)

**¿Qué significa?** Instalas la herramienta **dentro de un proyecto específico** (en la carpeta `node_modules`).

**¿Cuándo usarla?** Para herramientas que **solo usa ese proyecto**:
- Librerías que tu código necesita
- Dependencias específicas

**Ejemplo:**

```bash
npm install express
# Instala express solo para este proyecto
```

**Ventaja:** Cada proyecto puede tener sus propias versiones.
**Desventaja:** Ocupa espacio en cada proyecto.


#### **Regla Práctica:**

| Herramienta | ¿Global o Local? | ¿Por qué? |
|-------------|------------------|-----------|
| `typescript` (tsc) | **Global** | Lo usas en todos los proyectos para compilar |
| Librerías (React, Express) | **Local** | Cada proyecto usa las suyas |
| `ts-node` (ejecutar TS) | **Global** | Útil para probar código rápido |



### 3. Instalación Paso a Paso en Debian

#### Paso 1: Instalar Node.js y npm

##### Opción A: Desde los repositorios oficiales de Debian (Más fácil)

```bash
# Actualizar lista de paquetes
sudo apt update

# Instalar Node.js y npm
sudo apt install nodejs npm

# Verificar que se instaló bien
node --version   # Debería salir algo como v12.22.9
npm --version    # Debería salir algo como 8.5.1
```

**Problema:** Esta versión suele ser **antigua** (2021). Si necesitas versiones modernas, usa la Opción B.


##### Opción B: NodeSource (Versiones más recientes)

**¿Qué es NodeSource?** Es una empresa que mantiene repositorios actualizados de Node.js para Linux. No es más que una **fuente de descarga oficial** con versiones más nuevas.

```bash
# 1. Agregar el repositorio de NodeSource (versión 20.x)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -

# 2. Instalar Node.js (npm viene incluido)
sudo apt install -y nodejs

# 3. Verificar
node --version   # v20.x.x
npm --version    # 10.x.x
```

**Explicación:** `curl` descarga un script, `-E` mantiene tus variables de entorno, y `bash -` ejecuta el script. Este script configura los repositorios de Debian para que `apt` pueda instalar Node.js desde ahí.


##### Opción C: nvm (Node Version Manager)

##### nvm (Node Version Manager)

##### ¿Qué es?

**nvm** es un gestor de versiones de Node.js que permite instalar, administrar y cambiar entre múltiples versiones de Node.js en un mismo sistema.

##### nvm vs npm: ¡No los confundas!

| Característica | **nvm** | **npm** |
|----------------|---------|---------|
| **¿Qué es?** | Gestor de **versiones de Node.js** | Gestor de **paquetes/librerías** |
| **¿Qué instala?** | Diferentes versiones de **Node.js** | **Librerías, frameworks, herramientas** |
| **¿Dónde se instala?** | En el sistema (global) | En tu proyecto (local) o global |
| **Ejemplo** | `nvm install 20` | `npm install express` |
| **¿Para qué sirve?** | Cambiar entre versiones de Node | Gestionar dependencias del proyecto |

**Metáfora para recordar:**

- **nvm** = El "selector de versiones del lenguaje" (como elegir Python 3.8 o 3.11)
- **npm** = El "gestor de librerías" (como instalar pandas, flask, etc.)

**Son complementarios, no competidores.** Usas nvm para elegir la versión de Node, y npm para instalar las librerías que necesitas.


##### ¿Por qué usar nvm?

- **Flexibilidad**: Puedes tener diferentes versiones de Node.js para diferentes proyectos
- **Sin permisos de administrador**: No necesitas `sudo` para instalar paquetes globales
- **Aislamiento**: Cada proyecto puede usar su propia versión sin afectar a otros
- **Pruebas**: Facilita probar tu código en diferentes versiones de Node.js


##### ¿Cómo funciona?

nvm crea un directorio `~/.nvm` donde almacena todas las versiones de Node.js que instalas. Cuando ejecutas `nvm use [versión]`, nvm modifica temporalmente las variables de entorno (`PATH`) para que el sistema use esa versión específica.

##### Instalación de nvm

```bash
# Descargar e instalar nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# Recargar configuración (elegir una opción)
source ~/.bashrc    # Si usas bash
source ~/.zshrc     # Si usas zsh
# O simplemente reiniciar la terminal
```

##### Comandos esenciales de nvm

```bash
# 📋 INFORMACIÓN
nvm list                    # Versiones instaladas localmente
nvm list available          # Todas las versiones disponibles para instalar
nvm current                 # Versión que estás usando ahora mismo

# 📦 INSTALAR
nvm install 20              # Instala Node.js v20.x
nvm install 18              # Instala Node.js v18.x
nvm install --lts          # Instala la última versión LTS (Long Term Support)
nvm install node           # Instala la última versión estable

# 🔄 CAMBIAR DE VERSIÓN
nvm use 20                  # Cambia a Node.js v20.x
nvm use 18                  # Cambia a Node.js v18.x
nvm use                     # Usa la versión especificada en .nvmrc (si existe)

# ⭐ VERSIÓN POR DEFECTO
nvm alias default 20       # Siempre inicia con v20.x al abrir una terminal nueva

# 🗑️ DESINSTALAR
nvm uninstall 14           # Elimina Node.js v14.x
```

##### Flujo de trabajo típico

```bash
# 1️⃣ Instalar nvm (una sola vez)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
source ~/.bashrc

# 2️⃣ Instalar las versiones que necesitas
nvm install 20
nvm install 18

# 3️⃣ Usar la versión específica para tu proyecto
cd mi-proyecto
nvm use 20

# 4️⃣ (Opcional) Especificar versión para el proyecto
echo "20" > .nvmrc    # Crea un archivo con la versión
nvm use               # Lee automáticamente la versión del .nvmrc
```

##### Ventajas vs Otras formas de instalación

| Característica          | **nvm**        | **NodeSource**    | **Repositorios Ubuntu** |
| ----------------------- | -------------- | ----------------- | ----------------------- |
| **Múltiples versiones** | ✅ Sí           | ❌ No              | ❌ No                    |
| **Cambio rápido**       | ✅ Sí           | ❌ No (reinstalar) | ❌ No (reinstalar)       |
| **Requiere sudo**       | ❌ No           | ✅ Sí              | ✅ Sí                    |
| **Actualizaciones**     | ✅ Rápidas      | ✅ Rápidas         | ❌ Muy lentas            |
| **Ideal para**          | **Desarrollo** | **Producción**    | ❌ No recomendado        |


##### Cuándo usar nvm
- ✅ Proyectos de desarrollo local
- ✅ Trabajar con múltiples proyectos con diferentes requisitos
- ✅ Probar compatibilidad en diferentes versiones de Node
- ✅ Equipos de desarrollo donde cada miembro usa diferentes versiones

##### Cuándo NO usar nvm (usar NodeSource)
- ❌ Servidores de producción
- ❌ Entornos CI/CD (integración continua)
- ❌ Cuando solo necesitas una versión fija
- ❌ Sistemas multi-usuario donde necesitas una versión global

#### Las 3 formas de instalar Node.js (Resumen)

```bash
# FORMA 1: Repositorios Ubuntu (NO RECOMENDADO)
sudo apt update
sudo apt install nodejs npm
# ⚠️ Versión muy antigua (normalmente)

# FORMA 2: NodeSource (RECOMENDADO PARA PRODUCCIÓN)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
# ✅ Versión específica, estable, para servidores

# FORMA 3: nvm (RECOMENDADO PARA DESARROLLO)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
source ~/.bashrc
nvm install 20
# ✅ Múltiples versiones, flexible, para desarrollo
```

##### Nota importante

**nvm solo gestiona versiones de Node.js.** Para instalar librerías, frameworks o herramientas (como Express, React, Mongoose, etc.) **siempre se usa npm** (o yarn, pnpm, etc.). 

```bash
# EJEMPLO COMPLETO DE USO:
nvm use 20              # Eliges la versión de Node
npm init -y             # Inicias un proyecto
npm install express     # Instalas una librería con npm
npm install mongoose    # Instalas otra librería con npm
```

#### Paso 2: Instalar TypeScript Globalmente

```bash
# Instalar TypeScript de forma global
sudo npm install -g typescript

# Verificar instalación
tsc --version   # Debería salir Version 5.x.x
```

**¿Por qué global?** Porque usarás `tsc` para compilar en **todos** tus proyectos.

#### Paso 3: Configurar npm para evitar usar `sudo` (Opcional pero recomendado)

**Problema:** Cada vez que instales algo global con `npm install -g` necesitas `sudo`, lo que puede dar problemas de permisos.

**Solución:** Configurar npm para que instale en tu carpeta personal.

```bash
# 1. Crear carpeta para paquetes globales
mkdir ~/.npm-global

# 2. Decirle a npm que use esa carpeta
npm config set prefix '~/.npm-global'

# 3. Agregar esa carpeta al PATH (para que encuentre los comandos)
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc

# 4. Recargar configuración
source ~/.bashrc

# 5. Ahora puedes instalar sin sudo
npm install -g typescript   # Sin sudo
```

**Explicación:** El `PATH` es una lista de carpetas donde Linux busca programas. Al agregar `~/.npm-global/bin` ahí, los comandos instalados ahí serán ejecutables desde cualquier lugar.


### 4. Explicación de Herramientas Adicionales

Estas herramientas no son obligatorias, pero te facilitarán la vida:

####  **ts-node**

**¿Qué es?** Ejecuta código TypeScript **sin compilarlo** primero a JavaScript.

**¿Para qué sirve?** Para probar código rápido, hacer scripts pequeños, o ejecutar un archivo `.ts` directamente.

**Instalación:**

```bash
npm install -g ts-node   # Global para usarlo en cualquier lado
```

**Uso:**

```bash
# En lugar de:
tsc archivo.ts && node archivo.js

# Haces directamente:
ts-node archivo.ts
```

**Analogía:** Es como tener un intérprete que entiende TypeScript directamente.

####  **nodemon**

**¿Qué es?** Vigila tus archivos y **reinicia automáticamente** el programa cuando cambias algo.

**¿Para qué sirve?** Para desarrollo: editas el código, guardas, y nodemon lo ejecuta de nuevo automáticamente.

**Instalación:**

```bash
npm install -g nodemon
```

**Uso:**

```bash
# Ejecuta y reinicia ante cambios
nodemon --exec ts-node archivo.ts
```

**Analogía:** Es como tener un ayudante que siempre está ejecutando tu código nuevo sin que tengas que escribir el comando cada vez.


####  **ESLint + TypeScript plugins**

**¿Qué es?** Un "corrector de estilo" que te avisa si escribes código feo o con malas prácticas.

**¿Para qué sirve?** Para mantener código limpio, consistente y sin errores tontos.

**Instalación:**

```bash
npm install -g eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

**Analogía:** Es como un profesor que revisa tu código y te dice "esto se puede mejorar".


####  **npx**

**¿Qué es?** Una herramienta que viene con npm para ejecutar paquetes **sin instalarlos globalmente**.

**¿Para qué sirve?** Para usar una herramienta una sola vez sin instalarla.

**Ejemplo:**

```bash
# En lugar de instalar typescript globalmente, usas:
npx tsc --init   # Ejecuta tsc solo esta vez
```

**Analogía:** Es como pedir prestada una herramienta en lugar de comprarla.

### 5. Primer Proyecto TypeScript

#### Paso 1: Crear carpeta del proyecto

```bash
# Crear carpeta
mkdir mi-primer-proyecto-ts

# Entrar a ella
cd mi-primer-proyecto-ts
```


#### Paso 2: Inicializar npm (crea package.json)

```bash
npm init -y
```

**¿Qué hace?** Crea un archivo `package.json` con la configuración básica. Este archivo es el "DNI" de tu proyecto: dice qué herramientas usa, qué scripts tiene, etc.

**¿Qué es `package.json`?** Es un archivo JSON que:

- Lista las dependencias (librerías que usas)
- Define scripts (atajos para comandos)
- Guarda metadatos del proyecto


#### Paso 3: Crear estructura de carpetas

```bash
# Donde escribirás tu código TypeScript
mkdir src

# Donde se guardará el JavaScript compilado
mkdir dist
```

**¿Por qué separar?** Para mantener el código original (src) separado del código compilado (dist). Así no te lías.


#### Paso 4: Crear archivo TypeScript de prueba

```bash
# Crear archivo en src
nano src/index.ts
```

**Contenido:**

```typescript
// src/index.ts
function saludar(nombre: string): string {
    return `¡Hola, ${nombre}! Bienvenido a TypeScript en Debian`;
}

const mensaje = saludar("Estudiante");
console.log(mensaje);

// Esto daría error si lo descomentas porque "numero" no es string
// const error = saludar(123);
```

**¿Qué hace?** Función simple que recibe un `string` y devuelve un `string`.

**El tipo `: string`** es TypeScript diciendo "esta función devuelve texto".


#### Paso 5: Generar configuración de TypeScript

```bash
npx tsc --init
```

**¿Qué hace?** Crea `tsconfig.json` con todas las opciones de compilación.

**Configuración mínima recomendada:**

Abre `tsconfig.json` y modifica estas líneas:

```json
{
  "compilerOptions": {
    "target": "ES2020",          // Versión de JavaScript a generar
    "module": "commonjs",        // Sistema de módulos
    "outDir": "./dist",          // Dónde guardar los .js compilados
    "rootDir": "./src",          // Dónde están tus .ts
    "strict": true,              // Activa todas las verificaciones de tipos
    "esModuleInterop": true      // Permite importar módulos comunes
  },
  "include": ["src/**/*"],       // Qué archivos compilar
  "exclude": ["node_modules"]    // Qué archivos ignorar
}
```

**Explicación de opciones importantes:**
- **`outDir`**: Carpeta donde se guardará el JavaScript. Así no se mezcla con tu código original.
- **`strict`**: Activa todas las comprobaciones de tipo. Más seguridad.
- **`target`**: Versión de JavaScript que generará (ES2020 es moderna).


#### Paso 6: Configurar scripts en package.json

Abre `package.json` y agrega estos scripts en la sección `"scripts"`:

```json
{
  "scripts": {
    "build": "tsc",                     // Compila TypeScript a JavaScript
    "start": "node dist/index.js",      // Ejecuta el JavaScript compilado
    "dev": "ts-node src/index.ts",      // Ejecuta TypeScript directamente
    "watch": "tsc --watch",             // Compila automáticamente al guardar
    "dev:watch": "nodemon --watch src --ext ts --exec ts-node src/index.ts"  // Reinicia automáticamente
  }
}
```

**¿Cómo usarlos?**

```bash
npm run build    # Compila
npm run start    # Ejecuta
npm run dev      # Ejecuta sin compilar
npm run watch    # Compila automáticamente
```


#### Paso 7: Compilar y ejecutar

```bash
# Opción 1: Compilar y luego ejecutar
npm run build
npm run start

# Opción 2: Ejecutar directamente (sin compilar)
npm run dev
```

**Resultado esperado:**

```
¡Hola, Estudiante! Bienvenido a TypeScript en Debian
```


### 6. Comandos Esenciales para tu Día a Día

#### Gestión de Paquetes (npm)

| Comando                             | ¿Qué hace?                     | ¿Cuándo usarlo?                                        |
| ----------------------------------- | ------------------------------ | ------------------------------------------------------ |
| `npm init -y`                       | Crea `package.json`            | Al empezar un proyecto                                 |
| `npm install typescript --save-dev` | Instala TypeScript local       | Para que el proyecto tenga su propia versión           |
| `npm install -g typescript`         | Instala TypeScript global      | Para tener `tsc` en todos lados                        |
| `npm install`                       | Instala todas las dependencias | Cuando clonas un proyecto y necesitas las herramientas |
| `npm update`                        | Actualiza paquetes             | Periódicamente                                         |
| `npm uninstall <paquete>`           | Elimina un paquete             | Cuando ya no lo necesitas                              |



#### 🔷 Compilación TypeScript (tsc)

| Comando | ¿Qué hace? | ¿Cuándo usarlo? |
|---------|------------|-----------------|
| `tsc` | Compila según tsconfig.json | Para generar el JavaScript final |
| `tsc --watch` | Compila automáticamente al guardar | Durante desarrollo |
| `tsc --init` | Crea tsconfig.json | Al empezar un proyecto |
| `tsc archivo.ts` | Compila un archivo específico | Para pruebas rápidas |



####  Ejecución (node/ts-node)

| Comando | ¿Qué hace? | ¿Cuándo usarlo? |
|---------|------------|-----------------|
| `node archivo.js` | Ejecuta JavaScript compilado | Para producción |
| `ts-node archivo.ts` | Ejecuta TypeScript directamente | Para desarrollo/pruebas |
| `nodemon --exec ts-node archivo.ts` | Ejecuta y reinicia al guardar | Desarrollo intensivo |



### 7. Solución de Problemas Comunes

#### ❌ "Command 'tsc' not found"

**Problema:** El sistema no encuentra el comando `tsc`.

**Soluciones:**
1. **Si instalaste global:**

```bash
# Ver si está instalado
npm list -g typescript

# Si no, instalar
npm install -g typescript
```

2. **Si no usaste global:**

```bash
# Usar npx
npx tsc

# O agregar script en package.json
npm run build
```

3. **Problema de PATH:**

```bash
# Ver dónde está instalado
which tsc

# Si no aparece, agregar al PATH
export PATH=$PATH:/usr/local/bin
```


#### ❌ "Cannot find module 'typescript'"

**Problema:** El proyecto no encuentra TypeScript.

**Solución:**

```bash
# Instalar localmente en el proyecto
npm install --save-dev typescript

# Ahora usa:
npx tsc
```


#### ❌ Problemas de permisos con npm

**Problema:** Error EACCES al instalar globalmente.

**Solución 1 (rápida):**

```bash
sudo npm install -g <paquete>
```

**Solución 2 (definitiva):**

```bash
# Configurar npm para usuario
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

# Ya no necesitas sudo
npm install -g typescript
```


#### ❌ TypeScript no reconoce tipos de Node

**Problema:** Error como `Cannot find name 'require'`.

**Solución:**

```bash
# Instalar tipos de Node.js
npm install --save-dev @types/node
```

**¿Qué son `@types`?** Son archivos que le dicen a TypeScript qué tipos tienen las funciones de Node.js (como `require`, `fs`, `path`, etc.).


#### ❌ El código compila pero falla al ejecutar

**Problema:** `tsc` funciona pero `node` da error.

**Soluciones:**
1. **Verificar que el archivo compilado existe:**

```bash
ls dist/
# Debería ver index.js
```

2. **Verificar que ejecutas el archivo correcto:**

```bash
node dist/index.js   # No src/index.ts
```

3. **Verificar que usas la versión correcta de Node:**

```bash
node --version   # Debería ser >= 14
```


#### ❌ El watch no funciona

**Problema:** `tsc --watch` no recompila al guardar.

**Soluciones:**
1. **Verificar que el archivo está en src/**
2. **Usar `nodemon` en lugar de watch:**

```bash
npm install -g nodemon
nodemon --watch src --ext ts --exec ts-node src/index.ts
```


###  Resumen Final para tus Notas

#### Lista de Verificación (Checklist)

- [ ] Node.js instalado (`node --version`)
- [ ] npm instalado (`npm --version`)
- [ ] TypeScript global instalado (`tsc --version`)
- [ ] Carpeta `src/` y `dist/` creadas
- [ ] `tsconfig.json` configurado
- [ ] `package.json` con scripts
- [ ] Primer archivo `.ts` creado y probado

#### Flujo de Trabajo Básico

1. **Crear proyecto:**

```bash
mkdir proyecto && cd proyecto
npm init -y
mkdir src dist
npx tsc --init
```

2. **Escribir código:** en `src/index.ts`

3. **Compilar:**

```bash
npm run build
# o
tsc
```

4. **Ejecutar:**

```bash
npm run start
# o
node dist/index.js
```

5. **Para desarrollo rápido:**

```bash
npm run dev
# o
ts-node src/index.ts
```

#### Conceptos Clave para Recordar

| Concepto | Definición Simple |
|----------|-------------------|
| **Node.js** | El motor que ejecuta JavaScript |
| **npm** | La tienda de herramientas |
| **TypeScript** | JavaScript con tipos (más seguro) |
| **Global** | Instalado una vez para todos los proyectos |
| **Local** | Instalado solo para un proyecto |
| **tsconfig.json** | La configuración de cómo compilar |
| **package.json** | El "DNI" de tu proyecto |


---


### Gestores de Paquetes de Node.js

Los gestores de paquetes son herramientas que permiten instalar, actualizar, configurar y eliminar librerías, frameworks y herramientas en proyectos de Node.js. Facilitan la gestión de dependencias y la colaboración en equipos.

#### 1. npm (Node Package Manager)

##### ¿Qué es?
Es el gestor de paquetes **oficial** y por defecto de Node.js. Viene incluido automáticamente al instalar Node.js.

##### Características principales
- ✅ Gestor **por defecto** de Node.js
- ✅ Más de **2 millones de paquetes** disponibles (el ecosistema más grande)
- ✅ Integración nativa con Node.js
- ✅ Soporte para paquetes locales y globales
- ✅ Actualizaciones frecuentes

##### Comandos básicos

```bash
# Iniciar un proyecto
npm init                    # Inicia proyecto (modo interactivo)
npm init -y                 # Inicia proyecto con valores por defecto

# Instalar paquetes
npm install express         # Instala una dependencia local
npm install -g nodemon      # Instala una dependencia global
npm install                 # Instala TODAS las dependencias del proyecto

# Desinstalar
npm uninstall express       # Elimina una dependencia
npm uninstall -g nodemon    # Elimina una dependencia global

# Actualizar
npm update                  # Actualiza todas las dependencias
npm update express          # Actualiza una dependencia específica

# Información
npm list                    # Muestra las dependencias instaladas
npm outdated                # Muestra paquetes desactualizados
npm view express version    # Muestra la última versión disponible

# Publicar
npm login                   # Inicia sesión en npm
npm publish                 # Publica tu propio paquete

# Otros útiles
npm audit                   # Revisa vulnerabilidades de seguridad
npm audit fix               # Corrige vulnerabilidades automáticamente
npm cache clean             # Limpia la caché de npm
```

##### Archivo `package.json`

```json
{
  "name": "mi-proyecto",
  "version": "1.0.0",
  "description": "Descripción del proyecto",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.0.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.22"
  }
}
```

##### Ventajas
- ✅ Viene instalado por defecto con Node.js
- ✅ Mayor compatibilidad y soporte
- ✅ Ecosistema más grande y maduro
- ✅ Documentación extensa

##### Desventajas
- ❌ Puede ser lento en proyectos grandes
- ❌ Consume más espacio en disco por duplicación
- ❌ Estructura plana puede causar "dependencias fantasmas"

##### Instalación
```bash
# Ya viene incluido con Node.js, no requiere instalación adicional
node --version    # Verifica Node
npm --version     # Verifica npm
```


#### 2. Yarn (Yet Another Resource Negotiator)

##### ¿Qué es?
Yarn es un gestor de paquetes creado por **Facebook (Meta)** en 2016 para mejorar la velocidad, seguridad y consistencia de npm.

##### Características principales
- ✅ **Más rápido** que npm en instalaciones iniciales
- ✅ **Caché eficiente**: Guarda paquetes descargados para usarlos en futuras instalaciones
- ✅ **Offline mode**: Puedes instalar paquetes sin conexión a internet
- ✅ **Lockfile determinista**: Asegura que todos los desarrolladores tengan exactamente las mismas dependencias (`yarn.lock`)
- ✅ **Plug'n'Play (PnP)**: Modo opcional que elimina `node_modules` y mejora el rendimiento
- ✅ **Workspaces**: Soporte nativo para monorepos

##### Comandos básicos
```bash
# Iniciar proyecto
yarn init                    # Inicia proyecto (modo interactivo)
yarn init -y                 # Inicia proyecto con valores por defecto

# Instalar paquetes
yarn add express             # Instala una dependencia
yarn add -D nodemon          # Instala una dependencia de desarrollo
yarn add -g nodemon          # Instala una dependencia global
yarn install                 # Instala TODAS las dependencias

# Desinstalar
yarn remove express          # Elimina una dependencia

# Actualizar
yarn upgrade                 # Actualiza todas las dependencias
yarn upgrade express         # Actualiza una dependencia específica

# Información
yarn list                    # Muestra las dependencias instaladas
yarn outdated                # Muestra paquetes desactualizados

# Otros útiles
yarn audit                   # Revisa vulnerabilidades de seguridad
yarn cache clean             # Limpia la caché
yarn why express             # Explica por qué un paquete está instalado
```

##### Archivos importantes
```
package.json         # Configuración del proyecto
yarn.lock           # Lockfile determinista (similar a package-lock.json)
.yarnrc             # Configuración de Yarn
.yarn/              # Carpeta con caché y datos de Yarn
```

##### Plug'n'Play (PnP) - Modo Avanzado
```bash
# Habilitar PnP
yarn install --pnp

# En lugar de node_modules, genera:
.pnp.cjs            # Mapa de dependencias
.pnp.data.json      # Información adicional
.eslintrc.js        # Configuración para ESLint
```

##### Ventajas

- ✅ Más rápido que npm en instalaciones iniciales
- ✅ Caché global eficiente
- ✅ Instalaciones offline
- ✅ Lockfile determinista y confiable
- ✅ Excelente para monorepos con Workspaces
- ✅ Mejor experiencia en equipos grandes

##### Desventajas

- ❌ Requiere instalación separada (no viene con Node.js)
- ❌ Puede ser más lento que npm en proyectos pequeños
- ❌ PnP puede tener problemas de compatibilidad con algunas herramientas

##### Instalación

```bash
# Opción 1: Con npm (global)
npm install -g yarn

# Opción 2: Con Corepack (recomendado para Node.js >= v16.10)
corepack enable
corepack prepare yarn@stable --activate

# Opción 3: En Linux/macOS (via script)
curl -o- -L https://yarnpkg.com/install.sh | bash

# Verificar instalación
yarn --version
```


#### 3. pnpm (Performant npm)

##### ¿Qué es?
pnpm es un gestor de paquetes moderno y **ultrarrápido** creado por Zoltan Kochan. Su nombre significa "Performant npm" (npm eficiente). Es conocido por su eficiencia en espacio y velocidad.

##### Características principales

- ✅ **Almacenamiento global**: Todas las versiones de paquetes se guardan UNA SOLA VEZ en `~/.pnpm-store`
- ✅ **Enlaces simbólicos**: Cada proyecto usa enlaces al almacenamiento global
- ✅ **Ahorro de espacio**: Puede ahorrar GB de espacio en disco
- ✅ **Instalación ultrarrápida**: Hasta un 50-70% más rápido que npm/yarn
- ✅ **Estructura estricta**: Evita "dependencias fantasmas"
- ✅ **Workspaces**: Soporte nativo para monorepos
- ✅ **Compatible con npm**: Puede leer `package.json` y `package-lock.json`

##### ¿Cómo funciona?

```bash
# pnpm usa un enfoque diferente:
~/.pnpm-store/         # Almacén global centralizado
  ├── express@4.18.2/  # Cada versión guardada UNA VEZ
  ├── mongoose@7.0.0/
  └── ...

mi-proyecto/
  ├── node_modules/
  │   ├── express -> ../../.pnpm-store/express@4.18.2  # Enlace simbólico
  │   └── mongoose -> ../../.pnpm-store/mongoose@7.0.0 # Enlace simbólico
  └── package.json
```

##### Comandos básicos

```bash
# Iniciar proyecto
pnpm init                    # Inicia proyecto (modo interactivo)
pnpm init -y                 # Inicia proyecto con valores por defecto

# Instalar paquetes
pnpm add express             # Instala una dependencia
pnpm add -D nodemon          # Instala una dependencia de desarrollo
pnpm add -g nodemon          # Instala una dependencia global
pnpm install                 # Instala TODAS las dependencias

# Desinstalar
pnpm remove express          # Elimina una dependencia

# Actualizar
pnpm update                  # Actualiza todas las dependencias
pnpm update express          # Actualiza una dependencia específica

# Información
pnpm list                    # Muestra las dependencias instaladas
pnpm outdated                # Muestra paquetes desactualizados

# Otros útiles
pnpm audit                   # Revisa vulnerabilidades de seguridad
pnpm store status            # Ver estado del almacenamiento global
pnpm store prune             # Limpia el almacenamiento global
pnpm why express             # Explica por qué un paquete está instalado
```

##### Archivos importantes

```
package.json         # Configuración del proyecto
pnpm-lock.yaml      # Lockfile de pnpm
.npmrc              # Configuración de pnpm (también)
```

##### Ventajas

- ✅ **ULTRA RÁPIDO**: 50-70% más rápido que npm/yarn
- ✅ **AHORRO DE ESPACIO**: GB de espacio en disco ahorrados
- ✅ **Estructura estricta**: Sin dependencias fantasmas
- ✅ **Instalación simultánea**: Instala múltiples paquetes en paralelo
- ✅ **Excelente para monorepos**: Workspaces nativos
- ✅ **Compatible**: Puede usar `package.json` de npm
- ✅ **Creciente popularidad**: Adoptado por grandes empresas

##### Desventajas

- ❌ Menos popular que npm/yarn (menos documentación)
- ❌ Algunas herramientas pueden no ser compatibles
- ❌ Curva de aprendizaje pequeña (estructura diferente)

##### Instalación

```bash
# Opción 1: Con npm (global)
npm install -g pnpm

# Opción 2: Con Corepack (recomendado para Node.js >= v16.10)
corepack enable
corepack prepare pnpm@latest --activate

# Opción 3: En Linux/macOS (via script)
curl -fsSL https://get.pnpm.io/install.sh | sh -

# Opción 4: En Windows (via PowerShell)
iwr https://get.pnpm.io/install.ps1 -useb | iex

# Verificar instalación
pnpm --version
```


#### 4. Bun (Nuevo Competidor)

##### ¿Qué es?

Bun es un **runtime** y **gestor de paquetes** moderno que está ganando popularidad. Está escrito en Zig y promete ser mucho más rápido que Node.js, npm y yarn combinados.

##### Características principales

- ✅ **Todo en uno**: Runtime + gestor de paquetes + bundler + test runner
- ✅ **ULTRA RÁPIDO**: Hasta 10x más rápido que npm
- ✅ **Compatibilidad con npm**: Puede leer `package.json`
- ✅ **Soporte nativo para TypeScript**: No necesita configuración adicional
- ✅ **Menor consumo de memoria**: Más eficiente que Node.js

##### Comandos básicos

```bash
# Instalar paquetes (compatible con npm)
bun install                 # Instala todas las dependencias
bun add express             # Instala una dependencia
bun add -d nodemon          # Instala una dependencia de desarrollo

# Ejecutar scripts
bun run index.js            # Ejecuta un archivo JS/TS
bun run dev                 # Ejecuta un script del package.json

# Iniciar proyecto
bun init                    # Inicia un proyecto
```

##### Ventajas

- ✅ **Extremadamente rápido**
- ✅ **Soporte nativo TypeScript**: Ejecuta `.ts` directamente
- ✅ **Menor consumo de recursos**
- ✅ **Compatible con el ecosistema npm**
- ✅ **Runtime + gestor de paquetes en uno**

##### Desventajas

- ❌ **Muy nuevo**: Menos maduro y estable
- ❌ **Limitado**: Menos herramientas y soporte
- ❌ **No recomendado para producción**: Aún en desarrollo
- ❌ **Ecosistema pequeño**: Menos documentación

##### Instalación

```bash
# Linux/macOS
curl -fsSL https://bun.sh/install | bash

# Windows (via WSL o PowerShell)
powershell -c "irm bun.sh/install.ps1 | iex"

# Verificar instalación
bun --version
```


#### 5. Comparativa Rápida

| Característica | **npm** | **Yarn** | **pnpm** | **Bun** |
|----------------|---------|----------|----------|---------|
| **Velocidad** | 🟡 Media | 🟢 Rápido | 🟢 Muy Rápido | 🔴 Ultra Rápido |
| **Espacio en disco** | 🔴 Alto | 🟡 Medio | 🟢 Muy Bajo | 🟢 Bajo |
| **Caché global** | ✅ Sí | ✅ Sí | ✅ Sí (centralizado) | ✅ Sí |
| **Lockfile** | `package-lock.json` | `yarn.lock` | `pnpm-lock.yaml` | `bun.lockb` |
| **Workspaces** | ✅ Sí | ✅ Sí | ✅ Sí | 🟡 Limitado |
| **Offline Mode** | ❌ No | ✅ Sí | ✅ Sí | ❌ No |
| **Estructura estricta** | ❌ No | ❌ No | ✅ Sí | ❌ No |
| **Soporte nativo TS** | ❌ No | ❌ No | ❌ No | ✅ Sí |
| **Popularidad** | 🔴 Muy alta | 🟡 Alta | 🟡 Creciente | 🟢 Baja |
| **Madurez** | 🔴 Muy maduro | 🟡 Maduro | 🟡 Madurando | 🟢 Nuevo |


#### 6. ¿Cuál Elegir?

##### Elige **npm** si:

- ✅ Estás **aprendiendo** o empezando con Node.js
- ✅ Quieres la opción **más simple** y por defecto
- ✅ Priorizas **compatibilidad total** con todas las herramientas
- ✅ Trabajas en un proyecto **pequeño o mediano**

##### Elige **Yarn** si:

- ✅ Trabajas en un **proyecto grande** o **empresarial**
- ✅ Necesitas **Workspaces** para monorepos
- ✅ Quieres un lockfile **determinista y confiable**
- ✅ Valoras la **estabilidad** y madurez

##### Elige **pnpm** si:

- ✅ Quieres la **máxima velocidad** y eficiencia
- ✅ Trabajas con **muchas dependencias** (proyectos grandes)
- ✅ Te preocupa el **espacio en disco** (ahorro de GB)
- ✅ Quieres una estructura **estricta y sin errores**
- ✅ Trabajas en **monorepos** complejos
- ✅ Quieres estar a la **vanguardia** (rápida adopción)

##### Elige **Bun** si:

- ✅ Quieres **experimentar** con tecnología nueva
- ✅ Buscas un **runtime + gestor de paquetes** en uno
- ✅ Necesitas **soporte nativo para TypeScript**
- ✅ No te importa que sea **menos maduro** (no producción)
- ✅ Quieres probar la **velocidad extrema**


#### 7. Instalación Global de Gestores

```bash
# npm (ya incluido con Node.js)
node --version
npm --version

# Yarn (3 formas)
npm install -g yarn                # Con npm
corepack enable                    # Con Corepack (Node 16.10+)
curl -o- -L https://yarnpkg.com/install.sh | bash  # Script

# pnpm (3 formas)
npm install -g pnpm                # Con npm
corepack enable                    # Con Corepack (Node 16.10+)
curl -fsSL https://get.pnpm.io/install.sh | sh -   # Script

# Bun (1 forma)
curl -fsSL https://bun.sh/install | bash
```


#### 8. Migrar entre Gestores

##### Migrar de npm a yarn

```bash
# 1. Eliminar node_modules y package-lock.json
rm -rf node_modules package-lock.json

# 2. Instalar con yarn
yarn install
# Se genera yarn.lock automáticamente
```

##### Migrar de npm/yarn a pnpm

```bash
# 1. Eliminar node_modules y lockfile
rm -rf node_modules package-lock.json yarn.lock

# 2. Instalar con pnpm
pnpm install
# Se genera pnpm-lock.yaml automáticamente
```


#### 9. Recomendación Final

Para la mayoría de los desarrolladores hoy en día:

1. **Para aprendizaje y proyectos personales**: Comienza con **npm** (viene por defecto)
2. **Para proyectos profesionales**: Prueba **pnpm** (velocidad y eficiencia) o **Yarn** (estabilidad)
3. **Para monorepos y equipos grandes**: **pnpm** o **Yarn** con Workspaces
4. **Para experimentar**: **Bun** (cuando esté más maduro)


---

## Ejecucion


### 1️⃣ INSTALACIÓN GLOBAL (NO RECOMENDADO)

#### 1.1 ¿Qué es la instalación global?

Instalar TypeScript globalmente significa que el ejecutable `tsc` queda disponible en **TODO** el sistema operativo, como cualquier otro comando del sistema.

#### 1.2 Cómo instalar globalmente

```bash
# En Linux/Mac (necesita sudo por permisos)
sudo npm install -g typescript

# En Windows (sin sudo, pero como administrador)
npm install -g typescript
```

#### 1.3 Verificar instalación global

```bash
# Ver versión instalada
tsc --version

# Ver dónde está instalado
which tsc        # Linux/Mac
where tsc        # Windows
```

**Salida típica:**

```bash
$ tsc --version
Version 5.6.2

$ which tsc
/usr/local/bin/tsc
```

#### 1.4 ¿Dónde se puede ejecutar tsc?

Con instalación global, `tsc` funciona en **CUALQUIER** carpeta del sistema:

```bash
# En el home
cd ~
tsc hola.ts           # ✅ Funciona

# En el escritorio
cd ~/Escritorio
tsc prueba.ts         # ✅ Funciona

# En documentos
cd ~/Documentos/mi-proyecto
tsc index.ts          # ✅ Funciona

# En cualquier lugar
cd /tmp
tsc temporal.ts       # ✅ Funciona
```

#### 1.5 Compilación con instalación global

```bash
# Compilar un archivo (genera .js)
tsc hola.ts

# Compilar y ejecutar en un solo paso
tsc hola.ts && node hola.js

# Compilar en modo watch
tsc --watch hola.ts

# Compilar desde cualquier carpeta con ruta
tsc /home/usuario/proyectos/hola.ts
```

#### 1.6 Ventajas de la instalación global

- ✅ Comando `tsc` disponible en todo el sistema
- ✅ No necesitas `npx` ni estar en la carpeta del proyecto
- ✅ Ideal para scripts rápidos y pruebas sueltas

#### 1.7 Desventajas de la instalación global

- ❌ **Todos los proyectos comparten la misma versión de TypeScript**
- ❌ Si actualizás TS global, podés romper proyectos viejos
- ❌ Problemas de permisos en Linux/Mac (necesita `sudo`)
- ❌ No es la práctica recomendada en equipos de trabajo

---

### 2️⃣ INSTALACIÓN LOCAL (RECOMENDADO)

#### 2.1 ¿Qué es la instalación local?

Instalar TypeScript localmente significa que el paquete se instala **dentro de la carpeta de tu proyecto** en `node_modules/`. El comando `tsc` solo está disponible dentro de ese proyecto específico.

#### 2.2 Cómo instalar localmente

##### Paso 1: Crear la carpeta del proyecto

```bash
# Crear carpeta
mkdir mi-proyecto-ts
cd mi-proyecto-ts
```

##### Paso 2: Inicializar package.json

```bash
# Crear package.json (necesario para instalar paquetes locales)
npm init -y
```

**¿Qué es package.json?**

- Es el archivo de configuración del proyecto
- Guarda las dependencias instaladas
- Permite que otros desarrolladores instalen las mismas versiones

**Contenido de package.json:**

```json
{
  "name": "mi-proyecto-ts",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

##### Paso 3: Instalar TypeScript localmente

```bash
# Instalar como dependencia de desarrollo (--save-dev)
npm install typescript --save-dev
```

**¿Qué pasa cuando ejecutás este comando?**

1. npm descarga TypeScript de internet
2. Lo guarda en `node_modules/typescript/`
3. Agrega la dependencia al `package.json`:
   ```json
   "devDependencies": {
     "typescript": "^5.6.2"
   }
   ```
4. Crea `package-lock.json` (bloquea las versiones exactas)

#### 2.3 Estructura de carpetas después de instalar localmente

```
mi-proyecto-ts/
├── node_modules/           # Todas las dependencias instaladas
│   └── typescript/         # TypeScript instalado aquí
│       └── bin/
│           └── tsc         # El ejecutable está acá
├── package.json            # Configuración del proyecto
├── package-lock.json       # Versiones exactas de dependencias
└── (tus archivos .ts van acá)
```

#### 2.4 Verificar instalación local

```bash
# Ver si está instalado localmente
npm list typescript

# Ver versión local
npx tsc --version

# Ver la ruta del ejecutable local
ls -la node_modules/.bin/tsc
```

**Salida típica:**

```bash
$ npx tsc --version
Version 5.6.2

$ ls -la node_modules/.bin/tsc
lrwxrwxrwx 1 usuario usuario 22 ago 31 10:00 node_modules/.bin/tsc -> ../typescript/bin/tsc
```

#### 2.5 ¿Dónde se puede ejecutar tsc con instalación local?

##### Opción A: En la carpeta del proyecto (recomendado)

```bash
# Parado en la carpeta del proyecto
cd /home/usuario/mi-proyecto-ts
npx tsc hola.ts           # ✅ Funciona (usa el local)
```

##### Opción B: Desde cualquier carpeta con ruta absoluta

```bash
# Desde otra carpeta usando ruta completa
cd /home/usuario
npx tsc /home/usuario/mi-proyecto-ts/hola.ts   # ✅ Funciona
```

##### Opción C: Desde cualquier carpeta con ruta relativa

```bash
# Desde otra carpeta usando ruta relativa
cd /home/usuario
npx tsc ./mi-proyecto-ts/hola.ts               # ✅ Funciona
```

##### Opción D: Usando la ruta completa del ejecutable

```bash
# Llamar directamente al ejecutable (sin npx)
cd /home/usuario/otra-carpeta
/home/usuario/mi-proyecto-ts/node_modules/.bin/tsc hola.ts   # ✅ Funciona
```

#### 2.6 Compilación con instalación local


```bash
# Compilar un archivo (genera .js)
npx tsc hola.ts

# Compilar y ejecutar en un solo paso
npx tsc hola.ts && node hola.js

# Compilar en modo watch
npx tsc --watch hola.ts

# Compilar desde otra carpeta (con ruta completa)
npx tsc /home/usuario/mi-proyecto-ts/hola.ts

# Compilar todos los .ts de la carpeta
npx tsc *.ts
```

#### 2.7 NPX explicado en detalle

**NPX** es un ejecutador de paquetes que viene con npm.

Cuando ejecutás `npx tsc`, NPX hace esto:

1. Busca `tsc` en `node_modules/.bin/` del proyecto actual
2. Si no encuentra, busca en los paquetes globales
3. Si no existe en ningún lado, te pregunta si querés descargarlo

```bash
# npx busca en este orden:
# 1. ./node_modules/.bin/tsc        ← Local del proyecto
# 2. /usr/local/bin/tsc             ← Global del sistema
# 3. Te pregunta si descargarlo
```

**Ejemplo visual:**
```bash
# Sin npx (busca solo global)
$ tsc hola.ts
bash: tsc: command not found        # ❌ Error

# Con npx (busca local y global)
$ npx tsc hola.ts
[10:00:01] Found 0 errors           # ✅ Funciona
```

#### 2.8 Scripts en package.json (alternativa a npx)

Podés crear scripts en `package.json` para no escribir `npx` siempre:

```json
{
  "name": "mi-proyecto-ts",
  "version": "1.0.0",
  "scripts": {
    "build": "tsc hola.ts",
    "watch": "tsc --watch hola.ts",
    "start": "node hola.js"
  },
  "devDependencies": {
    "typescript": "^5.6.2"
  }
}
```

Luego ejecutás:

```bash
npm run build    # Compila
npm run watch    # Modo watch
npm start        # Ejecuta (start es especial, no necesita run)
```

**Ventaja:** npm ejecuta los scripts usando el `tsc` local automáticamente.

#### 2.9 Ventajas de la instalación local

- ✅ Cada proyecto tiene su propia versión de TypeScript
- ✅ No necesitas permisos de administrador (sudo)
- ✅ Fácil de compartir con otros desarrolladores
- ✅ No afecta a otros proyectos cuando actualizás
- ✅ Es la práctica estándar en desarrollo profesional

#### 2.10 Desventajas de la instalación local

- ❌ Necesitás `npx` o scripts en `package.json` para ejecutar
- ❌ Ocupa espacio en cada proyecto (duplicado)
- ❌ Solo funciona en la carpeta del proyecto (o con rutas completas)

---

### 3️⃣ COMPARACIÓN RÁPIDA: GLOBAL vs LOCAL

| Característica | GLOBAL | LOCAL |
|----------------|--------|-------|
| Comando | `tsc` | `npx tsc` |
| Permisos | Necesita sudo | No necesita |
| Funciona en | Cualquier carpeta | Solo en el proyecto |
| Versión | Una para todo el sistema | Una por proyecto |
| Dependencias | No se guardan | Se guardan en package.json |
| Recomendado | ❌ No | ✅ Sí |

---

### 4️⃣ FLUJO DE TRABAJO RECOMENDADO

#### Para pruebas pequeñas (Hola Mundo):

```bash
# 1. Crear carpeta
mkdir pruebas-ts
cd pruebas-ts

# 2. Inicializar e instalar TS local
npm init -y
npm install typescript --save-dev

# 3. Crear archivo .ts
echo 'console.log("Hola Mundo!")' > hola.ts

# 4. Compilar y ejecutar
npx tsc hola.ts
node hola.js

# 5. O en modo watch (dejar corriendo)
npx tsc --watch hola.ts &
node hola.js
```

#### Para proyectos grandes:

```bash
# 1. Estructura de carpetas
mkdir mi-app
cd mi-app
npm init -y
npm install typescript --save-dev

# 2. Crear estructura
mkdir src dist
touch src/index.ts

# 3. Configurar tsconfig.json (opcional)
npx tsc --init

# 4. Compilar todo el proyecto
npx tsc

# 5. En modo watch
npx tsc --watch
```

---

### 5️⃣ EJEMPLOS PRÁCTICOS DE EJECUCIÓN

#### Escenario 1: Tenés instalación local en `/home/usuario/mi-proyecto`

```bash
# Estás en la carpeta del proyecto
cd /home/usuario/mi-proyecto
npx tsc hola.ts          # ✅ Compila
node hola.js             # ✅ Ejecuta

# Estás en el home
cd /home/usuario
npx tsc ./mi-proyecto/hola.ts     # ✅ Compila (ruta relativa)
node ./mi-proyecto/hola.js        # ✅ Ejecuta

# Estás en cualquier carpeta
cd /tmp
npx tsc /home/usuario/mi-proyecto/hola.ts   # ✅ Compila (ruta absoluta)
node /home/usuario/mi-proyecto/hola.js      # ✅ Ejecuta
```

#### Escenario 2: Tenés instalación global

```bash
# Estás en cualquier carpeta
cd ~/Escritorio
tsc hola.ts          # ✅ Compila
node hola.js         # ✅ Ejecuta

cd /tmp
tsc prueba.ts        # ✅ Compila
node prueba.js       # ✅ Ejecuta

cd /home/usuario/Documentos
tsc index.ts         # ✅ Compila
node index.js        # ✅ Ejecuta
```

#### Escenario 3: Usando --watch

```bash
# Con instalación LOCAL
cd /home/usuario/mi-proyecto
npx tsc --watch hola.ts
# [10:00:01] Starting compilation in watch mode...
# [10:00:01] Found 0 errors. Watching for file changes.
# ... editás hola.ts y guardás ...
# [10:05:23] File change detected. Starting incremental compilation...
# [10:05:23] Found 0 errors. Watching for file changes.
# Ctrl+C para detener

# Con instalación GLOBAL
cd /home/usuario/mi-proyecto
tsc --watch hola.ts    # Mismo comportamiento, sin npx
```

---

### 6️⃣ COMMAND CHEATSHEET PARA TUS NOTAS

#### Con instalación LOCAL:

```bash
# Compilación
npx tsc archivo.ts                    # Compila un archivo
npx tsc *.ts                          # Compila todos los .ts
npx tsc archivo1.ts archivo2.ts      # Compila varios archivos

# Watch mode
npx tsc --watch archivo.ts            # Vigila cambios
npx tsc --watch *.ts                  # Vigila todos

# Ejecutar
node archivo.js                       # Ejecuta el JS generado

# Desde otra carpeta (ruta relativa)
npx tsc ../mi-proyecto/archivo.ts

# Desde otra carpeta (ruta absoluta)
npx tsc /home/usuario/mi-proyecto/archivo.ts

# Ver versión
npx tsc --version

# Usando scripts de package.json
npm run build                         # Si definiste "build": "tsc archivo.ts"
npm run watch                         # Si definiste "watch": "tsc --watch archivo.ts"
```

#### Con instalación GLOBAL:

```bash
# Compilación
tsc archivo.ts                        # Compila un archivo
tsc *.ts                              # Compila todos los .ts
tsc archivo1.ts archivo2.ts          # Compila varios archivos

# Watch mode
tsc --watch archivo.ts                # Vigila cambios

# Ejecutar
node archivo.js                       # Ejecuta el JS generado

# Desde cualquier carpeta
tsc /ruta/completa/archivo.ts        # Usando ruta absoluta

# Ver versión
tsc --version
```

---

### 7️⃣ PREGUNTAS FRECUENTES

**¿Puedo tener instalación global Y local al mismo tiempo?**

Sí, y de hecho es común. El local sobreescribe al global cuando usás `npx`.

**¿Cómo sé cuál estoy usando?**

```bash
tsc --version          # Usa el global
npx tsc --version      # Usa el local (si existe)
```

**¿Puedo instalar TS local sin package.json?**

Sí, pero no es recomendado porque npm no va a guardar la dependencia. Mejor siempre usar `npm init -y` primero.

**¿Qué pasa si ejecuto tsc sin npx teniendo TS local?**

Te va a dar error "command not found" porque el sistema no encuentra `tsc` en el PATH.

**¿node_modules/ ocupa mucho espacio?**

Sí, TypeScript pesa ~50MB. Pero es normal en desarrollo. Lo importante es que NO subas `node_modules/` a GitHub (usá `.gitignore`).

---







