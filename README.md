
LISTA COMPLETA DE COMANDOS UTILIZADOS

--------------------------------------------------------
1. SCRIPT DE BACKUP CON TAR EN FEDORA
--------------------------------------------------------
nano backup.sh

Contenido:
#!/bin/bash
roy=$(whoami)
FECHA=$(date +"%d-%m-%Y:%H:%M")
DESTINO="/home/$roy/backup_$FECHA.tar.gz"
tar -czf "$DESTINO" "/home/$roy"
echo "Backup creado en: $DESTINO"

chmod +x backup.sh
./backup.sh

--------------------------------------------------------
2. SCRIPT PARA COPIAR SALIDA DE IFCONFIG AL ESCRITORIO
--------------------------------------------------------
nano ifconfig_copia.sh

Contenido:
#!/bin/bash
read -p "¿Qué nombre desea para el archivo?: " NOMBRE_ARCHIVO
DESKTOP_DIR=$(xdg-user-dir DESKTOP)
ifconfig > "$DESKTOP_DIR/$NOMBRE_ARCHIVO.txt"
echo "Archivo creado en: $DESKTOP_DIR/$NOMBRE_ARCHIVO.txt"

chmod +x ifconfig_copia.sh
./ifconfig_copia.sh

--------------------------------------------------------
3. CONFIGURACIÓN DE RED EN MODO BRIDGE (GUI)
--------------------------------------------------------
- Apagar la VM.
- Configuración → Red → Modo puente (Bridge Adapter).
- Seleccionar tarjeta de red real (Wi-Fi o Ethernet).

--------------------------------------------------------
4. VERIFICAR IP Y CONEXIÓN DESDE WINDOWS
--------------------------------------------------------
# En Fedora:
ip a

# En Windows (cmd):
ping 192.168.X.X

--------------------------------------------------------
5. INSTALAR Y HABILITAR SSH EN FEDORA
--------------------------------------------------------
sudo dnf install -y openssh-server
sudo systemctl enable sshd
sudo systemctl start sshd
sudo systemctl status sshd

# Permitir SSH en el firewall
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --reload

--------------------------------------------------------
6. GENERAR CLAVES SSH Y CONFIGURAR ACCESO DESDE WINDOWS
--------------------------------------------------------
# En Windows (PowerShell o cmd):
ssh-keygen         # Presionar Enter en todo

# Probar conexión SSH inicial (pedirá contraseña)
ssh tu_usuario@192.168.X.X

# Copiar clave pública al servidor Fedora
type $env:USERPROFILE\.ssh\id_rsa.pub | ssh tu_usuario@192.168.X.X "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys && chmod 700 ~/.ssh"

# Conexión automática sin contraseña
ssh tu_usuario@192.168.X.X
