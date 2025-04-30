# 🐳 Docker para ROS Noetic
**Rama actual:** `ros-noetic`  

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
mkdir -p ~/docker/ros-noetic
# Clonar repositorio
git clone -b ros-noetic https://github.com/morg1207/RS-Docker-ROS.git ~/docker/ros-noetic
```

### 🐋 **1.3 Construcción del Entorno Docker**  

1. 🔨 **Compilar Imagen**  
```bash
#Ir a la carpeta de archivos
cd ~/docker/ros-noetic
# Construir imagen
sudo docker compose build 
```

2. 🚀 **Ejecutar Contenedor**  
```bash
# Detengo el contendor si esta en ejecución
sudo docker container stop cont_ros_noetic
# Eliminar contenedor si ya existe
sudo docker container rm cont_ros_noetic
# Ejecutar docker compose 
sudo docker compose up
```


### 🤖 **1.4. Ejecutar un terminal dentro del contenedor**  

```bash
# Ejecutar un terminal dentro del contenedor
docker exec -it cont_ros_noetic bash
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
sudo docker container stop cont_ros_noetic
# Eliminar contenedor si ya existe
sudo docker container rm cont_ros_noetic
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

### 🛠 **1.6 Recomendaciones para trabajar con el contenedor ROS Noetic**   

Para garantizar un flujo de trabajo eficiente con este contenedor, se ha configurado un volumen tipo *bind mount* que sincroniza el espacio de trabajo ROS entre el contenedor y tu sistema host. 

**Estructura clave:**
- **Dentro del contenedor**: Todo el desarrollo debe realizarse en el espacio de trabajo Catkin (`/catkin_ws/src`).
- **En tu sistema host**: El contenido se sincroniza automáticamente con la carpeta local `./proyecto_ros/`.




## 🐧 **2. Configuración para Linux**  

### 📋 **2.1 Requisitos**  
| Software | Enlace |
|----------|--------|
| Docker Engine | [Descarga](https://docs.docker.com/engine/install/ubuntu/) |
| Visual Studio Code  | [Descarga](https://code.visualstudio.com/) |


### 📥 **2.2 Clonar Repositorio**  
```bash
# Crear carpeta de trabajo
mkdir -p ~/docker/ros-noetic
# Clonar repositorio
git clone -b ros-noetic https://github.com/morg1207/RS-Docker-ROS.git ~/docker/ros-noetic
```

### 🐋 **2.3 Construcción del Entorno Docker**  

1. 🔨 **Compilar Imagen**  
```bash
#Ir a la carpeta de archivos
cd ~/docker/ros-noetic
# Construir imagen
sudo docker compose build 
```

2. 🚀 **Ejecutar Contenedor**  
```bash
# Eliminar contenedor si ya existe
sudo docker container rm cont_ros_noetic
# Ejecutar docker compose 
DISPLAY_VALUE=:0 docker compose up
```

### 🤖 **1.4. Ejecutar un terminal dentro del contenedor**  

```bash
# Ejecutar un terminal dentro del contenedor
docker exec -it cont_ros_noetic bash
```

### 🛠 **2.5 Configuración Avanzada con Dev Containers**   

**Recomendación profesional:** Para un flujo de trabajo integrado en ROS, utiliza **VS Code con Dev Containers** para:  
- 🔄 Desarrollo nativo dentro del contenedor  
- 📁 Acceso completo al filesystem  
- 🐛 Depuración integrada  

#### **Pasos para configuración:** 

1. 🚀 **Elimino el contenedor si ya ha sido creado**  
```bash
# Detengo el contendor si esta en ejecución
sudo docker container stop cont_ros_noetic
# Eliminar contenedor si ya existe
sudo docker container rm cont_ros_noetic
```

2. **Instalar requisitos previos:** 
   - [VS Code](https://code.visualstudio.com/)  
   - Extensión [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)  

3. **Abrir el proyecto en un contenedor:**  

    Presiona `Ctrl+Shift+P` → **"Dev Container: Reopen in Container"**  
   *VS Code detectará automáticamente la configuración en `.devcontainer/`*

### 🛠 **2.6 Recomendaciones para trabajar con el contenedor ROS Noetic**   

Para garantizar un flujo de trabajo eficiente con este contenedor, se ha configurado un volumen tipo *bind mount* que sincroniza el espacio de trabajo ROS entre el contenedor y tu sistema host. 

**Estructura clave:**
- **Dentro del contenedor**: Todo el desarrollo debe realizarse en el espacio de trabajo Catkin (`/catkin_ws/src`).
- **En tu sistema host**: El contenido se sincroniza automáticamente con la carpeta local `./proyecto_ros/`.
