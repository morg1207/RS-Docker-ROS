# Argumento para usarlo a lo largo del dockerfile 
ARG ROS_DISTRO=noetic  # Valor por defecto

# Imagen base
FROM osrf/ros:noetic-desktop-full

# Asegurar de estar en la raiz del directorio de archivos
WORKDIR /

# Crear tres espacios de trabajos
RUN mkdir -p /catkin_ws/src

# Configurar el shell por defecto
SHELL ["/bin/bash", "-c"]

# Instalar herramientas adicionales
RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-turtlesim \
    ros-${ROS_DISTRO}-teleop-twist-keyboard \
    nano \
    git \
    python3-rosdep \
    python3-catkin-tools && \
    rm -rf /var/lib/apt/lists/*

# Argumento para evitar el caché y siempre tener actualizado mi repositorio
ARG CACHEBUST=1

# Clonar el repositorio del simulador de warehouse
RUN git clone -b ros-${ROS_DISTRO} https://github.com/morg1207/RS-Turtlebot3.git /simulation_ws/src/RS-Turtlebot3


# Posicionar el terminal en mi espacio de trabajo
WORKDIR /catkin_ws

# Crear el espacio de trabajo
RUN catkin_make

# Configurar el entorno para ROS en todos los shells
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc && \
    echo "source /catkin_ws/devel/setup.bash" >> ~/.bashrc

# Copiar el script de entrada
COPY ./ros_entrypoint.sh /ros_entrypoint.sh

# Establecer el punto de entrada
ENTRYPOINT ["/bin/bash", "-c", "source /ros_entrypoint.sh"]