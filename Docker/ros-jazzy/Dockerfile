# Argumento para la distribución ROS (valor por defecto: 'humble')
ARG ROS_DISTRO=jazzy

# Imagen base dinámica
FROM osrf/ros:${ROS_DISTRO}-desktop-full

# Asegurar de estar en la raíz del directorio de archivos
WORKDIR /

# Crear espacio de trabajo (nombre genérico)
RUN mkdir -p /root/leonardo/src

# Configurar el shell por defecto
SHELL ["/bin/bash", "-c"]

# Instalar herramientas básicas (comunes a todas versiones)
RUN apt-get update && apt-get install -y \
    build-essential \
    python3-colcon-common-extensions \
    nano \
    git \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Instalar paquetes específicos de ROS (usando la variable)
RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-turtlesim \
    ros-${ROS_DISTRO}-teleop-twist-keyboard \
    ros-${ROS_DISTRO}-demo-nodes-cpp \
    && rm -rf /var/lib/apt/lists/*

# Install libraries gz sim
RUN apt-get update && apt-get install -y \
    lsb-release \
    gnupg \
    && rm -rf /var/lib/apt/lists/*

# Configura el repositorio de Gazebo Harmonic
RUN curl -sSL https://packages.osrfoundation.org/gazebo.gpg --output /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" > /etc/apt/sources.list.d/gazebo-stable.list

# Instala Gazebo Harmonic
RUN apt-get update && apt-get install -y \
    gz-harmonic \
    && rm -rf /var/lib/apt/lists/*
# Posicionar en el workspace
WORKDIR /root/leonardo_ws

# Configuración del entorno ROS (compatible con todas versiones)
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc && \
    echo "source /root/leonardo_ws/install/setup.bash" >> ~/.bashrc && \
    echo "export ROS_DISTRO=${ROS_DISTRO}" >> ~/.bashrc

# Copiar script de entrada (debe ser genérico)
COPY ./ros_entrypoint.sh /ros_entrypoint.sh
RUN chmod +x /ros_entrypoint.sh

# Punto de entrada estándar para ROS2
ENTRYPOINT ["/bin/bash", "-c", "source /ros_entrypoint.sh"]
