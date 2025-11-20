![Logo Institucional](https://github.com/JonatanBogadoUNLZ/PPS-Jonatan-Bogado/blob/9952aac097aca83a1aadfc26679fc7ec57369d82/LOGO%20AZUL%20HORIZONTAL%20-%20fondo%20transparente.png)

# Universidad Nacional de Lomas de Zamora - Facultad de Ingeniería

## Puesta a Punto y Mejora del Brazo Robótico SCORBOT EX IX

---

## Introducción / Objetivo

Este proyecto corresponde a la **Práctica Profesional Supervisada (PPS)** realizada en el **Laboratorio CIM Robótica** de la Facultad de Ingeniería – UNLZ.

El objetivo principal fue efectuar la **puesta a punto**, **mejora**, **programación**, **documentación operativa** y **calibración** del brazo robótico **SCORBOT EX IX**, junto con su controlador, su entorno físico y la integración con el sistema automatizado supervisado por el tablero central **“Manager”**.

El trabajo incluyó:

* Programación en **ACL**  
* Configuración y testeo de entradas/salidas digitales  
* Creación de rutinas GETXX, PUTXX, PR1-PR4  
* Implementación del programa principal **LOBBY**  
* Ajustes mecánicos y eléctricos  
* Documentación técnica completa para su uso futuro  

---

## Índice

* Descripción
* Instrucciones de Uso
* Tecnologías Utilizadas
* Listado de Componentes
* Esquemáticos
* Fotos / Videos
* Autor
* Carpetas del Proyecto

---

## Descripción

La práctica se desarrolló en el **CIM Robótica**, donde se encuentra una línea de producción automatizada provista por **ESHED Robotics**, compuesta por:

* Brazo robótico **SCORBOT EX IX**  
* Base lineal **Slidebase**  
* Cinta transportadora  
* Estaciones automáticas de proceso  
* Tablero central **Manager**

Se desarrolló un sistema completo de automatización para la Estación de Trabajo Nº2, que incluyó:

* Lectura de entradas digitales provenientes del Manager  
* Ejecución de rutinas según el pulso recibido  
* Movimientos articulares y cartesianos  
* Recolección (GETXX) y depósito (PUTXX) de bandejas  
* Ejecución de rutinas específicas (ENSAM, PRCAJ, TORN, TORN2)  
* Envío del pulso ACK al finalizar cada trabajo  

El controlador recibe un pulso en los puertos 9, 10, 11 o 12. Según la entrada activa, se ejecuta el PR correspondiente y luego la rutina asociada.

---

## Instrucciones de Uso

### 1. **Encendido del sistema**

* Encender controlador y PC con **ATS (Advanced Terminal Software)**.  
* Ejecutar `RUN HOMES` para realizar homing.  
* Si el controlador indica bloqueo, ejecutar `RUN SHUTD`.

### 2. **Activación de ejes con Teach Pendant**

1. Colocar el selector en **TEACH**.  
2. Presionar **CONTROL ON/OFF** hasta que aparezca *Con ALL*.  
3. Confirmar con **ENTER**.

### 3. **Ejecución de programas**

* Programa principal:  
  `RUN LOBBY`
* El sistema queda a la espera de pulsos del Manager.  
* Cada PR ejecuta GETXX → rutina → PUTXX.

### 4. **Apagado**

* Ejecutar `RUN SHUTD`.  
* Esperar finalización antes de apagar motores y controlador.

---

## Tecnologías Utilizadas

* **Robótica:** SCORBOT EX IX, Slidebase, estaciones CIM  
* **Control:** Teach Pendant, controlador ESHED ROBOTEC  
* **Programación:** Lenguaje **ACL** en ATS  
* **Electrónica:** I/O digitales, electroválvulas, gripper neumático  
* **Automatización:** Secuencias con PR1–PR4, ACK, lectura DIN/DOUT  

---

## Listado de Componentes

* Brazo robótico **SCORBOT EX IX**  
* Base lineal **Slidebase**  
* Teach Pendant  
* Tablero **Manager**  
* Cinta transportadora  
* Electroválvula del gripper  
* PC con software **ATS**  
* Cableado I/O entre Manager y controlador  

---

## Esquemáticos

Incluye:

* Cableado del gripper  
* Entradas y salidas conectadas al controlador  
* Conexiones entre Manager y controlador  
* Diagrama de plataformas y estaciones


---

## Fotos / Videos

Incluye:

* Brazo SCORBOT  
* Controlador y Teach Pendant  
* Cinta y estaciones  
* Bandejas PR1, PR2, PR3 y PR4  
* Circuito eléctrico

---

## Autor

Proyecto realizado por:

* **Audisio, Juan Pablo** – 43.671.648  
* **Gomez Franco Gabriel** – 41.451.020  
* **Reyna, Valentín** – 43.798.677  

Como parte de la **Práctica Profesional Supervisada** de Ingeniería Mecatrónica.

---

## Carpetas del Proyecto

* **INFORMES:** Informe PPS en PDF / Word  

---


