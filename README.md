# 🚀 Entornos Docker para ROS/ROS2

Repositorio con entornos Docker preconfigurados para diferentes versiones de ROS/ROS2.

## 🌟 Versiones Disponibles

| Versión   | Rama          | Estado     | Carpeta       |
|-----------|---------------|------------|---------------|
| ROS Noetic| `ros-noetic`  | ✅ Estable | docker/ros-noetic |
| ROS2 Humble| `ros-humble` | ✅ Estable | docker/ros-humble |
| ROS2 Iron | `ros-iron`    | ✅ Estable | docker/ros-iron |
| ROS2 Jazzy| `ros-jazzy`   | ✅ Estable | docker/ros-jazzy |

## 🛠️ Configuración


1. **Configuración general**
   - [Configuración general](docs/general-setup.md)

2. **Selecciona si estas usando windows o linux**:
   - [Configuración para Linux](docs/linux-guide.md#gui-config)
   - [Configuración para Windows](docs/windows-guide.md#gui-config)

## 🚀 Cómo Usar

1. Clona el repositorio:
   ```bash
   git clone https://github.com/morg1207/RS-Docker-ROS.git
   ```

2. Elige tu versión:
   ```bash
   cd ros-docker/docker/ros-humble  # Por ejemplo, para Humble
   ```

3. Sigue las instrucciones específicas en el README.md de cada versión.

## 📚 Documentación Detallada

- [Configuración para Windows](docs/windows-guide.md)
- [Configuración para Linux](docs/linux-guide.md)
- [Preguntas Frecuentes](docs/faq.md)

## 🤝 Contribuciones

¡Bienvenidas las contribuciones! Por favor sigue nuestra [guía de contribución](CONTRIBUTING.md).
```

### 2. README Específico por Versión (ej. docker/ros-humble/README.md)

```markdown
# 🐋 ROS2 Humble Docker Environment

**Versión:** Humble Hawksbill  
**Estado:** ✅ Estable  
**Docker Tag:** `ros_humble`  
**Workspace:** `/ros_ws`

## 📦 Características Especiales

- Gazebo Fortress incluido
- RViz2 preconfigurado
- Entorno de desarrollo VSCode integrado

## 🚀 Inicio Rápido

1. Construir la imagen:
   ```bash
   docker-compose build
   ```

2. Ejecutar el contenedor:
   ```bash
   docker-compose up -d
   ```

3. Acceder al contenedor:
   ```bash
   docker exec -it cont_ros_humble bash
   ```

## 🔧 Configuración Avanzada

Consulta la documentación general para:
- [Configuración de GUI](docs/linux-guide.md#gui-config)
- [Uso con VSCode](docs/general-setup.md#vscode-integration)

## ⚠️ Notas Específicas para esta Versión

- Requiere NVIDIA Docker para aceleración GPU
- Incluye paquetes adicionales: 
  - `ros-humble-navigation2`
  - `ros-humble-turtlebot3*`
```

### 3. Documentación Modularizada (en /docs/)

#### general-setup.md
```markdown
# Configuración General

## 🔌 Integración con VSCode

1. Instalar la extensión "Remote - Containers"
2. Abrir el proyecto en VSCode
3. Presionar Ctrl+Shift+P → "Reopen in Container"

## 🔄 Flujo de Trabajo con Bind Mounts

- Tu código en `./proyecto_ros/` se sincroniza con `/ros_ws/src` en el contenedor
- Los cambios son inmediatos en ambos lados
```

#### windows-guide.md
```markdown
# Configuración para Windows

## 📋 Requisitos Específicos

- WSL2 habilitado
- Xming Server para GUI
- Docker Desktop con integración WSL2

## 🖥️ Configuración X11 {#gui-config}

1. Instalar Xming
2. Ejecutar XLaunch con configuración:
   - Multiple windows
   - Display number: 0
   - Start no client
3. Exportar variable:
   ```bash
   export DISPLAY_VALUE=host.docker.internal:0.0
   ```
```

#### linux-guide.md
```markdown
# Configuración para Linux

## 📋 Requisitos Específicos

- Docker Engine instalado
- Nvidia Docker Toolkit (para GPU)

## 🖥️ Configuración X11 {#gui-config}

1. Permitir conexiones X11:
   ```bash
   xhost +local:docker
   ```
2. Ejecutar con:
   ```bash
   export DISPLAY_VALUE=:0
   docker-compose up
   ```
```

## 💡 Ventajas de Esta Estructura

1. **Minimiza duplicación**:
   - Las instrucciones comunes están centralizadas
   - Cada versión solo documenta sus particularidades

2. **Mantenimiento más fácil**:
   - Cambios en configuración general se actualizan en un solo lugar
   - Las versiones específicas pueden evolucionar independientemente

3. **Mejor experiencia de usuario**:
   - Documentación clara y bien organizada
   - Fácil de encontrar información específica
   - Se evita la redundancia de información

4. **Escalable**:
   - Fácil añadir nuevas versiones de ROS
   - Se pueden añadir nuevos sistemas operativos (Mac) sin afectar estructura

## 🔄 Flujo de Actualización

1. Cuando cambie algo en la configuración general:
   - Actualizar los archivos en `/docs/`
   
2. Cuando cambie algo específico de una versión:
   - Actualizar el README.md en la carpeta correspondiente

3. Para añadir una nueva versión:
   - Crear nueva carpeta en `/docker/`
   - Crear README.md específico
   - Añadir entrada en la tabla del README principal

Esta estructura mantiene tu documentación DRY (Don't Repeat Yourself) mientras provee toda la información necesaria de forma organizada y accesible.

