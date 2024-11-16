# Implementación de Accesorios para Monitorear Signos Vitales IoT LoRaWAN

## Introducción

En la actualidad el "Internet de las cosas" se ha convertido en una tendencia para la comunicación y asistencia operativa de máquina a máquina, entregando un resultado al usuario más acogedor. Esta tecnología tiene la posibilidad de poder comunicarse y controlar diferentes dispositivos como temperatura, distancia, humedad, infrarrojos, entre otros, que trabajan en un área establecida a largas distancias.

Los signos vitales son indicadores que reflejan el estado fisiológico del ser humano, siendo esta un área muy amplia de estudios continuos en diversas aplicaciones que permiten al paciente analizar y medir su salud de varios métodos y formas, con el objetivo de ser más exactos en la toma de muestras de la persona tratante para poder ir tomando decisiones conforme se vayan generando los resultados.

## Objetivos

- Diseñar el dispositivo inteligente con accesorios para una silla de ruedas que permita el monitoreo de signos vitales aplicando redes de sensores.
- Elaborar la topología y direccionamiento que se utilizará en la red de sensores mediante la tecnología LoRaWAN.
- Analizar el funcionamiento de los accesorios que se colocarán en la silla de ruedas.

## Metodología

### Desarrollo e Instalación del Sistema

#### Librerías Core
- Arduino IDE: Entorno de desarrollo principal
- Heltec ESP32 v0.0.7: Librería base para el módulo WiFi LoRa 32 v2
- Librerías de Sensores:
  - MAX30100lib: Sensor de ritmo cardíaco y SpO2
  - Adafruit MLX90614: Sensor de temperatura
  - U8g2: Control de pantalla OLED 0.96"

#### Configuración del Gateway HT-M00
1. Proceso de Inicialización:
   - Conexión vía USB-Type C
   - Configuración mediante botones CFG y RST
   - Acceso a interfaz vía IP 192.168.4.1
   - Credenciales por defecto: heltec.org

2. Parámetros de Configuración:
   - Red WiFi y credenciales
   - Banda de frecuencia: 916.8MHz - 918.2MHz
   - Dirección del servidor IoT-TTS

#### Conexión de Sensores
- Estructura de Conexión:
  - MAX30100: Comunicación vía Arduino Nano (TX-RX)
  - MLX90614: Conexión directa I2C (SCL=22, SDA=21)

## Arquitectura del Sistema

Se diseñó, en base al desarrollo de cada proceso 
anterior especificado en la investigación y experimentación del presente trabajo de 
titulación. Siendo una comunicación punto a punto, con alcance a una comunicación 
multipunto que se origina desde los sensores para finalizar en la visualización de los datos 
en la interfaz de usuario.


<div align="center">
  <h3>Arquitectura</h3>
  <img src="https://i.postimg.cc/q7rsmFp1/image.png" alt="TTN Server Data" width="800"/>
  <p>Arquitectura del sistema de Comunicación IoT LoRaWAN
  </p>
  <br>
</div>

## Descripción del Sistema de Comunicación IoT LoRaWAN

### 1. Sensores
La primera parte de la arquitectura del sistema de comunicación IoT LoRaWAN, denominada sensores. Se realiza un análisis investigativo para seleccionar a los sensores capaces de medir el ritmo cardiaco, SpO2 y temperatura, en el cuerpo humano. Para el ritmo cardiaco y SpO2, se seleccionó el sensor MAX30100, y para la lectura de la temperatura el sensor MLX90614. Por su funcionalidad de trabajo los sensores son capaces de interactuar en el cuerpo humano sin realizar ninguna alteración en la salud de la persona discapacitada. Los sensores seleccionados trabajan por medio de la comunicación I2C, una señal de datos y una señal de reloj.

### 2. Nodo Final
La segunda parte denominada nodo final, se centra en la interpretación y lectura de los sensores, que se utilizan para realizar las mediciones de los signos vitales en el cuerpo humano, por medio de un microcontrolador ESP32 incorporado. A su vez, el módulo Wifi LoRa 32 v2 posee las caracteristicas de procesar la información que los sensores censan, para poder transmitir, atravez de la tecnología LPWAN, protocolo LoRaWAN por medio del chip LoRa SX1276 del módulo que posee bandas de frecuencia de trabajo desde los 863MHz hasta los 928MHz. Logrando una transmisión inalámbrica.

### 3. Gateway
En el tercer apartado, se configura el gateway HT-M00 con la red Wifi y la banda de frecuencias de trabajo de la red LoRaWAN, para que realice la recepción e interpretación de la información que es enviada por el Nodo Final con el protocolo LoRaWAN por medio de enlaces de conexión. Para poder luego ser enviada por medio del internet con la tecnología Wifi hacia la nube o servidor de red. Es decir, es el intermediario para la comunicación entre el nodo final y el servidor de red, comportándose como un repetidor de señal.

### 4. Servidor de Red
El cuarto proceso en el servidor de red, The Things Network se registra y configura el gateway HT-M00 seguido del nodo final Wifi LoRa 32 v2 con la red LoRaWAN y la banda de frecuencias de trabajo, con el objetivo de poder comunicarse con los dispositivos de manera remota y recolectar la información que fueron enviados por los sensores, para poder receptar y visualizarlos, en tiempo real.

### 5. Interfaz de Usuario
En el quinto y último proceso, con la investigación de compatibilidad del servidor de red, se selecciona la interfaz de usuario Node-Red, que es capaz de poder comunicarse con el servidor de red (The Things Network) transmitiendo los datos censados por los sensores, de manera visual y de fácil entendimiento para el usuario final, en tiempo real.

<div align="center">
  <h3>Resultados</h3>
  <img src="https://i.postimg.cc/QNJR0Lsy/image.png" alt="Arquitectura del Sistema" width="800"/>
  <p>
  </p>
  <br>
</div>

### Componentes Principales:

1. **Sensores**
   - Comunicación I2C para temperatura
   - Conexión RX-TX para ritmo cardíaco y SpO2
   - Diseño modular integrado

2. **Nodo Final**
   - Módulo WiFi LoRa 32 v2
   - Protocolos de comunicación múltiple
   - Procesamiento y transmisión LoRaWAN

3. **Gateway**
   - Modelo HT-M00
   - Puente de comunicación
   - Gestión LoRaWAN y conexión internet

4. **Servidor de Red**
   - The Things Stack
   - Administración LoRaWAN
   - Gestión de seguridad y datos

5. **Interfaz de Usuario**
   - Desarrollada en Node-RED
   - Visualización en tiempo real
   - Monitoreo remoto

## Resultados y Pruebas

<div align="center">
  <h3>Prueba del Dispositivo en Protoboard</h3>
  <img src="https://i.postimg.cc/4dTSQP0G/image.png" alt="Prueba en Protoboard" width="800"/>
  <p>
    Implementación inicial del sistema en protoboard mostrando la integración de los sensores con el módulo WiFi LoRa 32 v2.
  </p>
  <br>
</div>

Los resultados obtenidos demuestran la correcta comunicación entre el nodo y el servidor The Things Stack mediante el Gateway LoRaWAN. El sistema realiza la autenticación a través de JoinEUI y DevEUI, estableciendo una conexión segura para la transmisión de datos.

<div align="center">
  <h3>Interfaz de Monitoreo en Node-RED</h3>
  <img src="https://i.postimg.cc/W4cnB3w6/image.png" alt="Interfaz Node-RED" width="800"/>
  <p>
    Visualización en tiempo real de los signos vitales mostrando:
    - Frecuencia Cardíaca (85.45 bpm)
    - Nivel de Saturación de Oxígeno - SpO2 (92%)
    - Temperatura Corporal (36.6°C)
  </p>
  <br>
</div>

## Contacto

Si necesitas ayuda o estás interesado en este proyecto, no dudes en contactarme. Con gusto puedo proporcionar más información y asistencia.



