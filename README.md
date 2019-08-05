# Bebop2_ROS

## Descripción general
Tutorial de como instalar y usar los drones BeBop2 dentro de ROS con la intensión de facilitar el trabajo a los nuevos programadores.

## Pre-requisitos
Se considera que la computadora del usuario ya tiene correctamente instalado ROS, GIT y que ya tiene la carpeta de `catkin_ws` correctamente inicializada.

Haber instalado los paquetes: ```build-esstential```, ```python-rosdep``` y  ```python-catkin-tools```. En caso que aun no los haya instalado ejecutar el siguiente commando:
```
sudo apt-get install build-essential python-rosdep python-catkin-tools
```

Deberá contar con un drone BeBop1 o BeBop2 de Parrot [http://www.parrot.com/].
<p align="center">
  <img width="280" height="180" src="http://wiki.ros.org/bebop_autonomy?action=AttachFile&do=get&target=bebop_1.jpg">
  <img width="300" height="200" src="https://www.parrot.com/files/s3fs-public/styles/product_teaser_display/public/ps/3495-large-parrot-3495jpg.jpg?itok=TGE8SI4T">
</p>

## Proceso de instalación
En una Terminal ejecutar las siguientes instrucciones:
```
cd catkin_ws/src
git clone https://github.com/AutonomyLab/bebop_autonomy.git src/bebop_autonomy
rosdep update
rosdep install --from-paths src -i
catkin build
```
El proceso de compilación debe terminar sin errores.


## Conectarse al dron mediante un nodo de ROS
Primero se debe encender el dron Bebop. Después de uno segundo el drone levantará una mini-red WiFi con el nombre de Bebop seguido de un número (ejemplo: BeBop2-097345). Con la computadora conéctarse a dicha red del dron. No necesitará password. Una vez conectado verifique la dirección IP de su computadora (para un Bebop2, la dirección de la computadora es la 192.168.42.60. El dron tendrá la dirección 192.168.42.1).

En una terminal de la computadora, ejecutar el siguiente nodo
```
roslaunch bebop_driver bebop_node.launch
```
En su lugar, también se puede ejecutar el nodelet:
```
roslaunch bebop_tools bebop_nodelet_iv.launch
```
Para ambos casos, se sugiere subscribirse al tópico ```image_view/image``` para observar en tiemporeal la imágen de la cámara del Bebop.

Estos programas se pueden usar como base para programas más complejos, pero eso requiere de mayor conocimiento del uso de los servomotores. Se sugiere leer las referencias [2-5] para mayores detalles.

## Autores y colaboradores
Ese paquete fue desarrollado en base a los programas originalmente publicados por Autonomy Lab en [1] y [2], pero fue ajustado ligeramente por el Dr. Alejandro Aceves-López para que sea más comprensible a los programadores nuevos de ROS.

## Referencias
1.  Mani Monajjemi, "Bebop autonomy - ROS driver for Parrot Bebop Drones 1.0 & 2.0", from Autonomy Lab, Simon Fraser University, [Online], Available: https://github.com/AutonomyLab/bebop_autonomy, [Accessed: 03-Aug-2019].
2. Mani Monajjemi, "Ardrone autonomy -ROS driver for Parrot AR-Drone 1.0 and 2.0 quadrocopters", from Autonomy Lab, Simon Fraser University, [Online], Available: https://github.com/AutonomyLab/ardrone_autonomy, [Accessed: 03-Aug-2019].
3. Stack OverFlow, "How to fly a Parrot bebop drone in tum simulator?", [Online]. Available: https://stackoverflow.com/questions/41326090/how-to-fly-a-parrot-bebop-drone-in-tum-simulator, [Accessed: 03-Aug-2019].
4. Giuseppe Silano, "BebopS simulator for Parrot Bebop 2", University of Sannio in Benevento, [Online]. Available: https://github.com/gsilano/BebopS, [Accessed: 03-Aug-2019].
