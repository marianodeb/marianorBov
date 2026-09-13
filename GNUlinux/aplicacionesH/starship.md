
## Instalacion

### 1. Descargamos e instalamos el binario ejecutable oficial de Starship

```bash
curl -sS https://starship.rs/install.sh | sh
```

### 2. Agregamos el arranque automático de Starship al final del archivo de configuración de Bash

```bash
echo 'eval "$(starship init bash)"' >> ~/.bashrc
```

### 3. Creamos el directorio donde vivirá la configuración del tema

```bash
mkdir -p ~/.config
```
# 4. Descargamos e instalamos el preset del tema Gruvbox Rainbow

```bash
starship preset gruvbox-rainbow -o ~/.config/starship.toml
```

# 5. Recargamos la configuración de Bash para activar Starship en la terminal actual

```bash
source ~/.bashrc
```


