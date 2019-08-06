# Bebop2_ROS

## Descripción general
Tutorial de como instalar y usar los drones BeBop2 dentro de ROS con la intensión de facilitar el trabajo a los nuevos programadores.

## Pre-requisitos
Se considera que la computadora del usuario ya tiene correctamente instalado ROS, GIT y que ya tiene la carpeta de `catkin_ws` correctamente inicializada.

También se necesita haber instalado los paquetes: ```build-esstential```, ```python-rosdep``` y  ```python-catkin-tools```. En caso que aun no los haya instalado ejecutar el siguiente commando en una Terminal: ```sudo apt-get install build-essential python-rosdep python-catkin-tools```.

Deberá contar con un drone BeBop1 o BeBop2 de Parrot [http://www.parrot.com/].
<p align="center">
  <img width="280" height="180" src="http://wiki.ros.org/bebop_autonomy?action=AttachFile&do=get&target=bebop_1.jpg">
  <img width="300" height="200" src="https://www.parrot.com/files/s3fs-public/styles/product_teaser_display/public/ps/3495-large-parrot-3495jpg.jpg?itok=TGE8SI4T">
</p>

## Proceso de instalación
Asegúrese de estar conectado a Internet. En una Terminal ejecutar las siguientes instrucciones una por una:
```
cd ~/catkin_ws
git clone https://github.com/AutonomyLab/bebop_autonomy.git src/bebop_autonomy
git clone https://github.com/AutonomyLab/parrot_arsdk.git src/parrot_arsdk
rosdep update
rosdep install --from-paths src -i
catkin build
source devel/setup.bash
```
En esta secuencias de comandos, deberá oprimir ```Y``` al menos unas cinco veces para continuar el proceso. Esto tomará algunos minutos. Aparecerán varios Warnings pero debe terminar sin errores.

## Conectarse al dron mediante un nodo de ROS
Primero se debe encender el drone Bebop. Después de unos segundos, el drone levantará una mini-red WiFi con el nombre de ```Bebop``` seguido de un número (ejemplo: BeBop2-097345). Con la computadora conéctarse a dicha red del dron. No necesitará password. Una vez conectado verifique la dirección IP de su computadora (para un Bebop2, la dirección de la computadora es la 192.168.42.60. El dron tendrá la dirección 192.168.42.1). En una Terminal ejecute:
```
ping 192.168.42.1
```
Debe responder con un mensaje del tiempo de respuesta. Terminar el proceso con la combinación de teclas ```Ctrl+C```.

Para lanzar el nodo que conecta la coputadora con el drone, ejecutar el siguiente comando en una Terminal:
```
roslaunch bebop_driver bebop_node.launch
```
En su lugar, también se puede ejecutar el nodelet:
```
roslaunch bebop_tools bebop_nodelet_iv.launch
```
Para ambos casos, se sugiere subscribirse al tópico ```bebop/image_raw``` para observar en tiempo-real la imágen de la cámara del Bebop. En una nueva Terminal ejecute:
```
rosrun image_view image_view image:=/bebop/image_raw
``` 
Debe observar la imagen de la cámara frontal del BeBop.

## Enviar comandos al Bebop
Se puede enviar un comando directamente a los tópicos del drone. Por ejemplo:

| Descripción | Comando |
| --- | --- |
| Takeoff: | ``` rostopic pub --once bebop/takeoff std_msgs/Empty ```|
| Land: | ``` rostopic pub --once bebop/land std_msgs/Empty```|

Otros comandos más complejos se pueden ejecutar siguiendo los pasos explicados en [2] en la sección "Sending Commands to Bebop".

Se puede controlador el Bebop usando el teclado. Para ello, instale el siguiente paquete:
```
cd ~/catkin_ws/src
git clone https://github.com/yakovkor/keyboard-control-for-bebop-2-drone.git
cd keyboard-control-for-bebop-2-drone
chmod +x teleop_twist_keyboard.py
cd ~/catkin_ws
catkin build
source devel/setup.bash
```
Luego, ejecute lo sigueinte en una Terminal:
```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```
Mayores detalles se podrán encontrar en [7].
    
Otros comandos útiles son:
```
rqt
```
    
Para grabar lo que sucede con el drone en un rosbag:
```
cd ~/catkin_ws
mkdir datos
cd datos
rosbag record /bebop/image_raw
rosbag play -l namefile.bag
```


Esta información se pueden usar como base para programas más complejos, pero eso requiere de mayor conocimiento del uso de los tópicos de BeBop. Se sugiere leer las referencias [1-5] para mayores detalles.

## Autores y colaboradores
Ese paquete fue desarrollado en base al material originalmente publicado en [1] y [2] por Mani Monajjemi de Autonomy Lab, pero fue ajustado ligeramente por el Dr. Alejandro Aceves-López para que sea más comprensible a los programadores nuevos de ROS.

## Referencias
1.  Mani Monajjemi, "Bebop autonomy - ROS driver for Parrot Bebop Drones 1.0 & 2.0", from Autonomy Lab, Simon Fraser University, [Online], Available: https://github.com/AutonomyLab/bebop_autonomy, [Accessed: 03-Aug-2019].
2. Mani Monajjemi, "Bebop autonomy - ROS driver manual", from Autonomy Lab, Simon Fraser University 2015, [Online], Available: https://bebop-autonomy.readthedocs.io, [Accessed: 03-Aug-2019].
3. Mani Monajjemi, "Ardrone autonomy -ROS driver for Parrot AR-Drone 1.0 and 2.0 quadrocopters", from Autonomy Lab, Simon Fraser University, [Online], Available: https://github.com/AutonomyLab/ardrone_autonomy, [Accessed: 03-Aug-2019].
4. Stack OverFlow, "How to fly a Parrot bebop drone in tum simulator?", [Online]. Available: https://stackoverflow.com/questions/41326090/how-to-fly-a-parrot-bebop-drone-in-tum-simulator, [Accessed: 03-Aug-2019].
5. Giuseppe Silano, "BebopS simulator for Parrot Bebop 2", University of Sannio in Benevento, [Online]. Available: https://github.com/gsilano/BebopS, [Accessed: 03-Aug-2019].
6. Thomas Bamford, "BeBop2 update installation", [Online]. Available: https://github.com/AutonomyLab/bebop_autonomy/blob/8392f055b7ef0205b357f0c2d4088389910a1151/docs/installation.rst, [Accessed: 03-Aug-2019].
7. Yakovkor, "Generic Keyboard Teleop for ROS for BeBop", [Online]. Available: https://github.com/yakovkor/keyboard-control-for-bebop-2-drone, [Accessed: 03-Aug-2019].
