

## **Archivos de configuración**  

1. **`.bash_profile`** → Script de inicio de sesión del usuario → **`~/.bash_profile`**  
2. **`.bashrc`** → Configuración del shell Bash para el usuario → **`~/.bashrc`**  
3. **`.gitconfig`** → Configuración de Git (nombre, email, alias) → **`~/.gitconfig`**  
4. **`.profile`** → Alternativa a `.bash_profile` para inicio de sesión → **`~/.profile`**  
5. **`aliases`** → Alias de correo para sendmail/postfix → **`/etc/aliases`**  
6. **`apache2.conf`** → Configuración principal de Apache (Debian) → **`/etc/apache2/apache2.conf`**  
7. **`crontab`** → Tareas programadas del usuario → **`/var/spool/cron/[usuario]`**  
8. **`dhcpd.conf`** → Configuración del servidor DHCP → **`/etc/dhcp/dhcpd.conf`**  
9. **`environment`** → Variables de entorno globales → **`/etc/environment`**  
10. **`fstab`** → Definición de particiones montadas al inicio → **`/etc/fstab`**  
11. **`group`** → Grupos del sistema y sus miembros → **`/etc/group`**  
12. **`grub`** → Configuración del gestor de arranque GRUB → **`/etc/default/grub`**  
13. **`grub.cfg`** → Archivo generado por GRUB (no editar manual) → **`/boot/grub/grub.cfg`**  
14. **`hostname`** → Nombre del equipo → **`/etc/hostname`**  
15. **`hosts`** → Asignación estática de IPs y dominios → **`/etc/hosts`**  
16. **`httpd.conf`** → Configuración principal de Apache (RHEL) → **`/etc/httpd/conf/httpd.conf`**  
17. **`ifcfg-*`** → Configuración de interfaces de red (RHEL) → **`/etc/sysconfig/network-scripts/ifcfg-[interfaz]`**  
18. **`interfaces`** → Configuración de red (Debian) → **`/etc/network/interfaces`**  
19. **`iptables/rules.v4`** → Reglas persistentes de firewall → **`/etc/iptables/rules.v4`**  
20. **`limits.conf`** → Límites de recursos para usuarios → **`/etc/security/limits.conf`**  
21. **`localtime`** → Zona horaria del sistema → **`/etc/localtime`** (enlace a `/usr/share/zoneinfo/...`)  
22. **`modprobe.d/*.conf`** → Configuración de módulos del kernel → **`/etc/modprobe.d/*.conf`**  
23. **`my.cnf`** → Configuración de MySQL/MariaDB → **`/etc/mysql/my.cnf`**  
24. **`netplan/*.yaml`** → Configuración de red (Ubuntu moderno) → **`/etc/netplan/*.yaml`**  
25. **`nginx.conf`** → Configuración principal de Nginx → **`/etc/nginx/nginx.conf`**  
26. **`passwd`** → Información de cuentas de usuario → **`/etc/passwd`**  
27. **`postgresql.conf`** → Configuración de PostgreSQL → **`/etc/postgresql/[versión]/main/postgresql.conf`**  
28. **`resolv.conf`** → Servidores DNS del sistema → **`/etc/resolv.conf`**  
29. **`resolved.conf`** → Configuración de DNS con systemd → **`/etc/systemd/resolved.conf`**  
30. **`shadow`** → Contraseñas cifradas de usuarios → **`/etc/shadow`**  
31. **`smb.conf`** → Configuración de Samba → **`/etc/samba/smb.conf`**  
32. **`ssh/config`** → Configuración personalizada de SSH → **`~/.ssh/config`**  
33. **`sshd_config`** → Configuración del servidor SSH → **`/etc/ssh/sshd_config`**  
34. **`sudoers`** → Permisos de `sudo` (editar con `visudo`) → **`/etc/sudoers`**  
35. **`sysctl.conf`** → Parámetros del kernel → **`/etc/sysctl.conf`**  
36. **`auth.log`** → Registros de autenticación → **`/var/log/auth.log`**  
37. **`syslog`** → Logs generales del sistema → **`/var/log/syslog`**  
38. **`..service`** → Configuración de servicios para systemd → **`/etc/systemd/system/`** 
39. **`.timer`** → Configuración de temporizadores para systemd →  **`/etc/systemd/system/`** 

