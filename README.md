![Logo Institucional](https://github.com/JonatanBogadoUNLZ/PPS-Jonatan-Bogado/blob/9952aac097aca83a1aadfc26679fc7ec57369d82/LOGO%20AZUL%20HORIZONTAL%20-%20fondo%20transparente.png)

# Universidad Nacional de Lomas de Zamora - Facultad de Ingeniería

**PUESTA A PUNTO Y MEJORA DEL BRAZO ROBÓTICO SCORBOT EX IX**  
_CIM Robótica - FI-UNLZ – Práctica Profesional Supervisada_

## Introducción / Objetivo

En la Universidad Nacional de Lomas de Zamora, nuestra Facultad de Ingeniería se dedica a la formación de profesionales en diversas ramas de la ingeniería. Este repositorio corresponde al proyecto de **Práctica Profesional Supervisada (PPS)** en el área de **Robótica / Automatización**, desarrollado en el **laboratorio CIM de Robótica** como parte de la carrera de **Ingeniería Mecatrónica**.

El objetivo de este proyecto es **poner a punto, documentar y mejorar el uso del brazo robótico SCORBOT EX IX** de la estación de trabajo N.º 2 del laboratorio CIM.  
Se busca:

- Normalizar el procedimiento de encendido, uso y apagado seguro del sistema.  
- Desarrollar y documentar programas de control (LOBBY, PR1–PR4, GETXX, PUTXX, etc.) que permitan operar la estación de forma automática desde el “Manager”.  
- Facilitar el uso del sistema a futuros estudiantes mediante una guía clara y código reutilizable.

---

## Índice

- [Descripción](#descripción)  
- [Instrucciones de Uso](#instrucciones-de-uso)  
- [Tecnologías Utilizadas](#tecnologías-utilizadas)  
- [Listado de Componentes](#listado-de-componentes)  
- [Esquemáticos](#esquemáticos)  
- [Fotos / Videos](#fotos--videos)  
- [Autor](#autor)  
- [Carpetas del Proyecto](#carpetas-del-proyecto)

---

## Descripción

Este proyecto se basa en la **automatización de la estación de trabajo N.º 2** del laboratorio CIM de Robótica utilizando un **brazo robótico SCORBOT EX IX** montado sobre una **Linear Slidebase** de ESHED ROBOTEC, controlado por su **controlador dedicado** e integrado a la línea CIM mediante un tablero central **“Manager”**.

La línea de producción del CIM cuenta con:

- Una **cinta transportadora**.  
- Un **almacén** de piezas.  
- **Cuatro estaciones de trabajo**, cada una con su robot asociado.

En la estación 2, el SCORBOT recibe bandejas desde la cinta, ejecuta una operación sobre ellas y las devuelve, interactuando mediante **entradas y salidas digitales** con el Manager.  
El proyecto aborda:

- El **cableado y verificación de I/O** entre el Manager y el controlador del robot.  
- La **programación en lenguaje ACL (Advanced Control Language)** a través del software **ATS (Advanced Terminal Software)**.  
- El diseño de una arquitectura de programas que incluye:
  - Programa principal **LOBBY**, que coordina las órdenes de trabajo.  
  - Programas **PR1, PR2, PR3 y PR4**, asociados a tareas en distintas estaciones.  
  - Programas **GETXX** y **PUTXX** para recolección y depósito de bandejas.  
  - Programas auxiliares como **HOMES** (homing) y **SHUTD** (apagado seguro).

El resultado es una estación de trabajo funcional, documentada y lista para ser utilizada, modificada y ampliada por futuros estudiantes.

---

## Instrucciones de Uso

Para utilizar este proyecto en la estación de trabajo N.º 2, se recomienda seguir los siguientes pasos generales:

1. **Encendido del sistema**
   - Encender el controlador del SCORBOT y el tablero “Manager”.  
   - En la PC, ejecutar el software **ATS (Advanced Terminal Software)**.  

2. **Homing del brazo robótico**
   - En ATS, ejecutar el comando:  
     `RUN HOMES`  
   - Verificar que el robot complete la rutina de homing sin errores.  
   - Si aparece el mensaje indicando que no se ejecutó el programa **SHUTD** en el apagado anterior, ejecutar:  
     `RUN SHUTD`  
     y luego volver a ejecutar `RUN HOMES`.  

3. **Activación de ejes (Teach Pendant)**
   - Verificar que el selector esté en posición **“TEACH”**.  
   - Presionar **“CONTROL ON/OFF”** hasta que en el display aparezca **“Con ALL”**.  
   - Presionar **“ENTER”** para confirmar.  

4. **Configuración de velocidades**
   - En los programas se utilizan variables **SPDA** (velocidad articular brazo) y **SPDB** (velocidad base lineal).  
   - Ajustar estos valores en el código si se requiere modificar la velocidad.  
   - La velocidad lineal se ajusta manualmente dentro de cada programa mediante `SPEEDL`.

5. **Ejecución del programa principal**
   - Ejecutar el programa principal:  
     `RUN LOBBY`  
   - Este programa habilita y mantiene en espera los programas **PR1–PR4**, cada uno asociado a una entrada digital específica del controlador.

6. **Recepción de órdenes de trabajo**
   - El Manager enviará un pulso de entrada a los puertos correspondientes (p. ej. 9, 10, 11, 12).  
   - Al detectar el pulso:
     - Se detienen los demás programas (STOP PRx y STOP LOBBY).  
     - Se ejecuta la secuencia GETXX + programa de proceso (ENSAM, PRCAJ, TORN2, TORN) + PUTXX.  
     - Al finalizar, se envía una señal **ACK** de 1 segundo por la salida asignada para informar finalización.

7. **Regulación del gripper**
   - En una pata de la Linear Slidebase se encuentra una **válvula neumática** que ajusta la velocidad de apertura/cierre del gripper.  
   - Regular según la delicadeza de las piezas a manipular.

8. **Apagado seguro**
   - Al finalizar el uso del sistema, ejecutar:  
     `RUN SHUTD`  
   - Esperar a que el programa termine y recién entonces apagar el controlador y el resto del sistema.  
   - No hacerlo puede causar bloqueo de motores en el próximo encendido.

> **Importante:** para detalles, ejemplos de código y diagramas, consultar las carpetas **CODIGO**, **PLANOS** e **INFORMES** de este repositorio.

---

## Tecnologías Utilizadas

Este proyecto fue desarrollado utilizando una variedad de tecnologías, incluyendo:

- **Robótica**
  - Brazo robótico **SCORBOT EX IX** (5 grados de libertad).  
  - **Linear Slidebase** ESHED ROBOTEC (1 grado de libertad adicional).  
  - **Gripper neumático**.  
  - **Teach Pendant** ESHED ROBOTEC.

- **Electrónica / Automatización**
  - **Controlador ESHED ROBOTEC** del SCORBOT.  
  - **Tablero central “Manager”** con entradas/salidas digitales.  
  - **Cinta transportadora** y estaciones de trabajo del CIM.  
  - Cableado de **entradas/salidas (DIN/DOUT)** y alimentación del gripper.

- **Programación**
  - Lenguaje **ACL (Advanced Control Language)**.  
  - Estructuras similares a C: variables, vectores, ciclos `FOR`, condicionales `IF`, subrutinas `GOSUB`, etc.

- **Plataformas**
  - **ATS (Advanced Terminal Software)** para comunicación PC–controlador.  
  - PC con sistema operativo compatible con el software ATS.

- **(Opcional / Futuras mejoras)**
  - Posible incorporación futura de rutinas de **visión** o **colaboración entre estaciones**.

---

## Listado de Componentes

- **SCORBOT EX IX**  
  Brazo robótico de 5 grados de libertad interpolables para manipulación de bandejas en la estación 2.

- **Linear Slidebase ESHED ROBOTEC**  
  Base lineal que agrega un grado de libertad de translación (no interpolable).

- **Controlador ESHED ROBOTEC del SCORBOT**  
  Unidad de control que gestiona los motores del brazo, I/O y comunicación con la PC y el Manager.

- **Teach Pendant ESHED ROBOTEC**  
  Permite el control manual del robot, enseñanza de posiciones y testeo local.

- **Tablero central “Manager”**  
  Tablero que coordina la línea CIM, genera y recibe señales digitales de las estaciones y de la cinta.

- **Cinta transportadora y carros de transporte**  
  Distribuyen las bandejas entre el almacén y las estaciones de trabajo.

- **Plataformas de trabajo (4)**  
  Posiciones definidas donde el robot toma y deposita las bandejas.

- **PC con software ATS**  
  Interfaz para la programación en ACL, ejecución de programas y monitoreo del sistema.

- **Cableado y elementos de conexión**
  - Cableado de entradas/salidas digitales.  
  - Cable del gripper y válvula de regulación neumática.  

---

## Esquemáticos

A continuación se presentan los esquemáticos y diagramas de diseño que explican cómo se ensamblan y operan los sistemas del proyecto (los archivos se encuentran en la carpeta **PLANOS**):

- **Esquemático 1: Circuito eléctrico del controlador**
  - Diagrama del cableado entre el tablero “Manager”, el controlador del SCORBOT y el gripper.  
  - Archivo sugerido: `PLANOS/circuito_controlador_cim2.pdf`

- **Esquemático 2: Layout de la estación de trabajo 2**
  - Ubicación del brazo, Linear Slidebase, cinta transportadora y plataformas de trabajo.  
  - Archivo sugerido: `PLANOS/layout_estacion2.png`

- **Esquemático 3: Diagrama de I/O (DIN/DOUT)**
  - Asignación de entradas y salidas utilizadas por los programas LOBBY, PR1–PR4, GETXX, PUTXX.  
  - Archivo sugerido: `PLANOS/mapa_io_scorbot_cim2.pdf`

*(En esta sección puedes subir imágenes o enlaces a los archivos relevantes en la carpeta `PLANOS`.)*

---

## Fotos / Videos

Aquí puedes visualizar imágenes y videos que muestran el proceso de desarrollo y la implementación final del proyecto (archivos en la carpeta **MULTIMEDIA**):

- **Foto 1:** Brazo robótico SCORBOT EX IX con la Linear Slidebase en la estación 2.  
  - `MULTIMEDIA/scorbot_estacion2.jpg`

- **Foto 2:** Teach Pendant y controlador ESHED ROBOTEC.  
  - `MULTIMEDIA/teach_y_controlador.jpg`

- **Foto 3:** Tablero “Manager” y línea CIM completa.  
  - `MULTIMEDIA/manager_linea_cim.jpg`

- **Foto 4:** Bandejas utilizadas en los programas PR1, PR2, PR3 y PR4 antes de la ejecución.  
  - `MULTIMEDIA/bandejas_pr1_pr4.jpg`

- **Video 1:** Ejecución del programa LOBBY y respuesta del sistema ante una orden de trabajo.  
  - `MULTIMEDIA/video_lobby_estacion2.mp4`

*(Actualiza las rutas según los nombres reales de tus archivos en `MULTIMEDIA`.)*

---

## Autor

Este proyecto fue realizado por los estudiantes de **Ingeniería Mecatrónica** de la Facultad de Ingeniería de la Universidad Nacional de Lomas de Zamora, en el marco de la **Práctica Profesional Supervisada**:

- **Audisio, Juan Pablo** – DNI 43.671.648  
- **Gomez Franco, Gabriel** – DNI 41.451.020  
- **Reyna, Valentín** – DNI 43.798.677  

---

## Carpetas del Proyecto

A continuación se detallan las carpetas que estructuran este repositorio:

- **CODIGO**  
  Contiene el código fuente utilizado en este proyecto: programas ACL (LOBBY, PR1–PR4, GETXX, PUTXX, HOMES, SHUTD, subrutinas de trabajo, etc.).

- **MULTIMEDIA**  
  Imágenes y videos del desarrollo y funcionamiento del proyecto, incluyendo fotos de la estación, del SCORBOT y demostraciones de los programas.

- **PLANOS**  
  Esquemáticos y diagramas de los sistemas implementados: circuito eléctrico del controlador, mapa de I/O, layout de la estación de trabajo, etc.

- **DATASHEET**  
  Hojas de datos y especificaciones de los componentes utilizados (SCORBOT EX IX, Linear Slidebase, controlador, gripper, etc.).

- **INFORMES**  
  Archivos relacionados con la planificación y documentación del proyecto: informe de PPS en PDF, cronogramas, diagramas de Gantt, manual de uso de la estación, documentación técnica adicional.

