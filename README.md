# Bebop2_ROS

## Descripción general
Tutorial de como instalar y usar los drones BeBop2 dentro de ROS con la intensión de facilitar el trabajo a los nuevos programadores.

## Pre-requisitos
Se considera que la computadora del usuario ya tiene correctamente instalado ROS, GIT y que ya tiene la carpeta de `catkin_ws` correctamente inicializada.

Deberá contar con un drone BeBop2 de Parrot:
* Un servomotor [Dynamixel](http://www.robotis.us/dynamixel/) (ejemplo: Mx-28 Mx-106, etc.)

   

## Proceso de instalación
En una Terminal ejecutar las siguientes instrucciones:
```
cd ~
git clone https://github.com/ROBOTIS-GIT/DynamixelSDK.git
```



## Ejemplos de programas de usuario en ROS
Se creó un paquete llamada `example_dynamixel` con algunos programas basados en los ejemplos presentados en sitio de ROBOTIS GIT - Dinamixel SDK [7] dentro de la carpeta `c++/example/protocol1.0/`. Dichos programas utilizan la librería `dynamixel_sdk` previamente creada. 

Para instalar el paquete `example_dynamixel` ejecutar las siguientes instrucciones: 
```
cd ~/catkin_ws/src
git clone https://github.com/aaceves/example_dynamixel.git
cd ~/catkin_ws
catkin build
source devel/setup.bash
```
Se habrán dado de alta los siguientes nodos:

| <node_name> | Descripción | ./src/file |
| --- | --- | --- |
| read_write | Mueve el servo 1 de un lado al otro. El baudrate del servomotor debe ser 57600. | read_write.cpp | 
| ping | Ejecuta el comando ping a los ID = 1, 2 y 3 en un baudrate de 1000000 | ping.cpp | 

En dos Terminales diferentes ejecutar cada una de las siguientes lineas:
```
roscore
rosrun example_dynamixel <node_name>
```
Estos programas se pueden usar como base para programas más complejos, pero eso requiere de mayor conocimiento del uso de los servomotores. Se sugiere leer las referencias [2-5] para mayores detalles.

## Autores y colaboradores
Ese paquete fue desarrollado en base a los programas originalmente publicados por Autonomy Lab en [1] y [2], pero fue ajustado ligeramente por el Dr. Alejandro Aceves-López para que sea más comprensible a los programadores nuevos de ROS.

## Referencias
1.  Mani Monajjemi, "Bebop autonomy - ROS driver for Parrot Bebop Drones 1.0 & 2.0", from Autonomy Lab, Simon Fraser University, [Online], Available: https://github.com/AutonomyLab/bebop_autonomy, [Accessed: 03-Aug-2019].
2. Mani Monajjemi, "Ardrone autonomy -ROS driver for Parrot AR-Drone 1.0 and 2.0 quadrocopters", from Autonomy Lab, Simon Fraser University, [Online], Available: https://github.com/AutonomyLab/ardrone_autonomy, [Accessed: 03-Aug-2019].
3. Stack OverFlow, "How to fly a Parrot bebop drone in tum simulator?", [Online]. Available: https://stackoverflow.com/questions/41326090/how-to-fly-a-parrot-bebop-drone-in-tum-simulator, [Accessed: 03-Aug-2019].
4. Giuseppe Silano, "BebopS simulator for Parrot Bebop 2", University of Sannio in Benevento, [Online]. Available: https://github.com/gsilano/BebopS, [Accessed: 03-Aug-2019].
