# LINUX

## 🐧 **1. Configuración para Linux**  

### 📋 **1.1 Requisitos**  
| Software | Enlace |
|----------|--------|
| Docker Engine | [Descarga](https://docs.docker.com/engine/install/ubuntu/) |
| Visual Studio Code  | [Descarga](https://code.visualstudio.com/) |

### 🔧 **1.2 Configuración adicional de docker**  

Esta es una configuración adicional para docker, solo es necesario hacerla una vez para todas las versiones de ROS.
1. **Acceso Gráfico para Contenedores**: 
```bash
#Para que los contenedores puedan abrir ventanas gráficas en tu sistema (ej.: RViz, Gazebo, GUIs de ROS), ejecuta:
echo 'xhost +local:root >/dev/null 2>&1' >> ~/.bashrc && source ~/.bashrc
```
2. **Continúa con la configuración**

- [Configuración de GUI](docs/general-setup.md)
