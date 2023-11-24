# Administración de Servidores Web: Instalación y Configuración de Apache en Ubuntu 22.04.3 LTS en Azure

## Objetivo de la Práctica

El objetivo de esta práctica es completar la instalación y configuración del servidor web Apache en una máquina virtual (MV) con Ubuntu 22.04.3 LTS en Azure. Posteriormente, se realizará una breve exposición que abordará aspectos clave del proceso, desde los requisitos iniciales hasta la presentación y defensa del trabajo.

## Requisitos Iniciales

1. **Creación de la Máquina Virtual (MV) en Azure:**
   - Sistema Operativo: Ubuntu 22.04.3 LTS
   - Tipo de MV: Standard DS1 v2 (1 vcpu, 3.5 GiB memory)
   - Activación de conexión SSH en el Dashboard de Azure.
   - Activación de conexión HTTP en el Dashboard de Azure (dando acceso al puerto 80)

2. **Configuración de Conexión SSH:**
   - Generación de clave privada mediante `ssh-keygen`.
   - Vinculación de la clave privada con la Terminal (ej. Warp).
   - Agregar la clave pública en Azure Dashboard para la conexión SSH.
   - Nota: se puede crear una clave privada y enviarla por correo usando `ssh-keygen -t rsa -b 4096 -C "[email]"`

## Entorno de Configuración

- **Tipo de Entorno:** Local (para propósitos de esta práctica)
- **Conexión SSH:** Realizada desde la Terminal local a la MV en Azure.

## Proceso de Configuración y Demo

1. **Conexión a la Máquina Virtual:**
   ```
   ssh -i <KEY_PATH> <Azure_User>@<VM_IP>
   Nota: datos para la demo: ssh -i ~/.ssh/nuevakey.pem azureuser@20.199.83.190
2. **Actualización del Sistema:**
    ```
   sudo apt update
   sudo apt upgrade
3. **Instalación de Apache 2:**
   ```
   sudo apt install apache2
4. **Verificación del Estado de Apache:**
   ```
   systemctl status apache2
5. **Exploración del Directorio www:**
   ```
   cd /var/www
6. **Despliegue de un Proyecto Web:**
   ```
   # Crear una nueva carpeta para el proyecto
   sudo mkdir my_web_project
   # Copiar archivos del proyecto a la carpeta
   cp -r /path/to/your/web/project/* /var/www/project/
## Pruebas de Carga y Benchmark

Utilizar herramientas como Apache Benchmark (ab) para realizar pruebas de carga en el servidor web recién instalado y evaluar su rendimiento bajo diferentes condiciones.

## Documentación Generada

### Se deberá generar documentación que incluya:

#### Capturas de Pantalla: Muestra de la conexión SSH, instalación de Apache, y verificación del estado.

![Daemons](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/01.png?raw=true)<br>
![Keygen](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/02.png?raw=true)<br>
![Conecction](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/03.png?raw=true)<br>
![Update](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/04.png?raw=true)<br>
![Actualización](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/05.png?raw=true)<br>
![Apache2](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/07.png?raw=true)<br>
![Apache2-Status](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/06.png?raw=true)<br>
![Ir-A-Carpeta](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/08.png?raw=true)<br>
![HTMLBase](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/09.png?raw=true)<br>
![Despliegue-Web](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/10.png?raw=true)<br>

#### Archivos de Configuración: Si se realizaron modificaciones en archivos de configuración de Apache.

- **Mostrar estadísticas de uso de recursos:**

Nota: para ello se debe instalar el navegador de texto Lynx y ajustar la variable APACHE_LYNX

    sudo apt-get update
    sudo apt-get install lynx
    sudo nano /etc/apache2/envvars
    export APACHE_LYNX='/usr/bin/lynx'

Localizar la línea de definición de la variable y cambiar a:

    export APACHE_LYNX='usr/bin/lynx'

#### Resultados de Pruebas de Carga: Capturas de pantalla de las pruebas de carga y resultados obtenidos.

### Pruebas de carga:

    ab -n 10 -c 5 http://20.199.83.190:80/html
- -n 10: Realiza 10 solicitudes en total.
- -c 5: Mantiene un máximo de 5 conexiones simultáneas.<br>

![Prueba-Carga-Simultánea](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/12.png?raw=true)

### Utilizar la herramienta de benchmarking Wrk para medir el rendimiento del servidor web bajo una carga de trabajo sostenida.

    wrk -t 10 -c 10 -d 15s http://20.199.83.190:80/html
- -t 10: Utiliza 10 hilos de trabajo.
- -c 100: Mantiene un máximo de 10 conexiones simultáneas.
- -d 30s: Ejecuta la prueba durante 15 segundos.
- Nota: hay que instalar primero la aplicación con:
  
  sudo apt install wrk

![Prueba-Wrk](https://github.com/jousemarquez/Administracion-Servidores-Web/blob/master/Screenshots/13.png?raw=true)

### Comandos útiles para la gestión de un Apache2 en una máquina virtual en Azure

# Comandos Útiles para Apache2 en una Máquina Virtual

## 1. Iniciar, Detener y Reiniciar Apache2:

- **Iniciar Apache2:**

sudo service apache2 start

- **Detener Apache2:**
  
sudo service apache2 stop

- **Reiniciar Apache2:**

sudo service apache2 restart

- **Recargar Configuración sin Reiniciar:**

sudo service apache2 reload

- **Mostrar Configuración de Apache2:**

apache2ctl -S

- **Verificar Configuración de Archivos:**

sudo apache2ctl configtest

- **Mostrar Accesos y Errores en Tiempo Real:**

sudo tail -f /var/log/apache2/access.log
sudo tail -f /var/log/apache2/error.log

- **Lista de módulos cargados:**
  
apache2ctl -M