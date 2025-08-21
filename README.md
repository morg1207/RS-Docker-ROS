# 🐳 Docker para ROS jazzy
**Rama actual:** `ros-jazzy` con `gazebo Ignition`. 

<img src="./ros-jazzy/images/ros-jazzy.png" alt="Ros_jazzy" width="200"/>
---

## 🖥️ **1. Configuración para Windows**  

### 📋 **1.1 Requisitos de sotfware**  
| Software | Enlace |
|----------|--------|
| WSL2 | [Instalación](https://aka.ms/wsl2-install) |
| Docker Desktop | [Descarga](https://docs.docker.com/desktop/setup/install/windows-install/) |
| Xming Server  | [Descarga](https://sourceforge.net/projects/xming/) |
| Visual Studio Code  | [Descarga](https://code.visualstudio.com/) |

 1. Se necesita que **Docker** Compose este ejecutándose.
 2. Se necesita **xlaunch server** este ejecutándose.

### 📥 **1.2 Clonar Repositorio**  
```bash
# Crear carpeta de trabajo
mkdir -p ~/docker/ros-jazzy
# Clonar repositorio
git clone -b ros-jazzy https://github.com/morg1207/RS-Docker-ROS.git ~/docker/ros-jazzy
```

### 🐋 **1.3 Construcción del Entorno Docker**  

1. 🔨 **Compilar Imagen**  
```bash
#Ir a la carpeta de archivos
cd ~/docker/ros-jazzy
# Construir imagen
sudo docker compose build 
```

2. 🚀 **Ejecutar Contenedor**  
```bash
# Detengo el contendor si esta en ejecución
sudo docker container stop cont_ros_jazzy
# Eliminar contenedor si ya existe
sudo docker container rm cont_ros_jazzy
# Ejecutar docker compose 
sudo docker compose up
```


### 🤖 **1.4. Ejecutar un terminal dentro del contenedor**  

```bash
# Ejecutar un terminal dentro del contenedor
docker exec -it cont_ros_jazzy bash
```
### 🛠 **1.5 Configuración Avanzada con Dev Containers**   

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
sudo docker container stop cont_ros_jazzy
# Eliminar contenedor si ya existe
sudo docker container rm cont_ros_jazzy
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

### 🛠 **1.6 Recomendaciones para trabajar con el contenedor ROS jazzy**   

Para garantizar un flujo de trabajo eficiente con este contenedor, se ha configurado un volumen tipo *bind mount* que sincroniza el espacio de trabajo ROS entre el contenedor y tu sistema host. 

**Estructura clave:**
- **Dentro del contenedor**: Todo el desarrollo debe realizarse en el espacio de trabajo ros2 (`/ros2_ws/src`).
- **En tu sistema host**: El contenido se sincroniza automáticamente con la carpeta local `./proyecto_ros/`.


---

## 🐧 **2. Configuración para Linux**  

### 📋 **2.1 Requisitos**  
| Software | Enlace |
|----------|--------|
| Docker Engine | [Descarga](https://docs.docker.com/engine/install/ubuntu/) |
| Visual Studio Code  | [Descarga](https://code.visualstudio.com/) |

### 🔧 **2.2 Configuración adicional de docker**  

Esta es una configuración adicional para docker, solo es necesario hacerla una vez para todas las versiones de ROS.
1. **Acceso Gráfico para Contenedores**: 
```bash
#Para que los contenedores puedan abrir ventanas gráficas en tu sistema (ej.: RViz, Gazebo, GUIs de ROS), ejecuta:
echo 'xhost +local:docker >/dev/null 2>&1' >> ~/.bashrc && source ~/.bashrc
```
2. Ejecutar Docker sin sudo:
```bash
# Crear un grupo de docker
sudo groupadd docker
# Añadir usuario al grupo de docker
sudo usermod -aG docker $USER
# Activar los cambios sin reiniciar sesión
newgrp docker  
```


### 📥 **2.3 Clonar Repositorio**  
```bash
# Crear carpeta de trabajo
mkdir -p ~/docker/ros-jazzy
# Clonar repositorio
git clone -b ros-jazzy https://github.com/morg1207/RS-Docker-ROS.git ~/docker/ros-jazzy
```

### 🐋 **2.4 Construcción del Entorno Docker**  

1. 🔨 **Compilar Imagen**  
```bash
#Ir a la carpeta de archivos
cd ~/docker/ros-jazzy
# Construir imagen
docker compose build 
```

2. 🚀 **Ejecutar Contenedor**  
```bash
# Eliminar contenedor si ya existe
docker container rm cont_ros_jazzy
# Ejecutar docker compose 
DISPLAY_VALUE=:0 docker compose up
```

### 🤖 **2.5. Ejecutar un terminal dentro del contenedor**  

```bash
# Ejecutar un terminal dentro del contenedor
docker exec -it cont_ros_jazzy bash
```

### 🛠 **2.6 Configuración Avanzada con Dev Containers**   

**Recomendación profesional:** Para un flujo de trabajo integrado en ROS, utiliza **VS Code con Dev Containers** para:  
- 🔄 Desarrollo nativo dentro del contenedor  
- 📁 Acceso completo al filesystem  
- 🐛 Depuración integrada  

#### **Pasos para configuración:** 

1. 🚀 **Elimino el contenedor si ya ha sido creado**  
```bash
# Detengo el contendor si esta en ejecución
docker container stop cont_ros_jazzy
# Eliminar contenedor si ya existe
docker container rm cont_ros_jazzy
```

2. **Instalar requisitos previos:** 
   - [VS Code](https://code.visualstudio.com/)  
   - Extensión [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)  

3. **Abrir el proyecto en un contenedor:**  

    Presiona `Ctrl+Shift+P` → **"Dev Container: Reopen in Container"**  
   *VS Code detectará automáticamente la configuración en `.devcontainer/`*

### 🛠 **2.7 Recomendaciones para trabajar con el contenedor ROS jazzy**   

Para garantizar un flujo de trabajo eficiente con este contenedor, se ha configurado un volumen tipo *bind mount* que sincroniza el espacio de trabajo ROS entre el contenedor y tu sistema host. 

**Estructura clave:**
- **Dentro del contenedor**: Todo el desarrollo debe realizarse en el espacio de trabajo ros2 (`/ros2_ws/src`).
- **En tu sistema host**: El contenido se sincroniza automáticamente con la carpeta local `./proyecto_ros/`.
