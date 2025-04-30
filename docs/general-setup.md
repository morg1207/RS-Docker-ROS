# CONFIGURACIÓN GENERAL


### 🔧 **1 Configuración adicional de docker**  

Esta es una configuración adicional para docker, solo es necesario hacerla una vez para todas las versiones de ROS.

1. Ejecutar Docker sin sudo:
```bash
# Crear un grupo de docker
sudo groupadd docker
# Añadir usuario al grupo de docker
sudo usermod -aG docker $USER
# Activar los cambios sin reiniciar sesión
newgrp docker  
```


### 🛠 1.5 Configuración Avanzada con Dev Containers {#vscode-integration}   

**Recomendación profesional:** Para un flujo de trabajo integrado en ROS, utiliza **VS Code con Dev Containers** para:  
- 🔄 Desarrollo nativo dentro del contenedor  
- 📁 Acceso completo al filesystem  
- 🐛 Depuración integrada  
-  Extensiones de VS Code integradas y configuradas

#### **Pasos para configuración:**  

1. **Instalar requisitos previos:** 
   - [VS Code](https://code.visualstudio.com/)  
   - Extensión [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)  

2. 🚀 **Eliminar contenedores remanentes**  
```bash
# Detengo el contendor si esta en ejecución
sudo docker container stop cont_ros_humble
# Eliminar contenedor si ya existe
sudo docker container rm cont_ros_humble
```

3. **Abrir el proyecto en un contenedor:**  
```bash
# Ir a la carpeta de archivos
cd ~/docker/ros-conceptos
# Abro VS Code desde este carpeta
code ./
```
    Presiona `Ctrl+Shift+P` → **"Dev Container: Reopen in Container"**  
   *VS Code detectará automáticamente la configuración en `.devcontainer/`*

---


### 🛠 **1.6 Recomendaciones para trabajar con el contenedor ROS humble**   

Para garantizar un flujo de trabajo eficiente con este contenedor, se ha configurado un volumen tipo *bind mount* que sincroniza el espacio de trabajo ROS entre el contenedor y tu sistema host. 

**Estructura clave:**
- **Dentro del contenedor**: Todo el desarrollo debe realizarse en el espacio de trabajo ros2 (`/ros2_ws/src`).
- **En tu sistema host**: El contenido se sincroniza automáticamente con la carpeta local `./proyecto_ros/`.
