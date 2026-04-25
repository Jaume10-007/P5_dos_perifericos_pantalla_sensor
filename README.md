📺🌡️ Monitor OLED con Temperatura y Humedad

Proyecto en ESP32 + PlatformIO que lee un sensor de temperatura y humedad por I2C y muestra los datos en una pantalla OLED.

🚀 Descripción

Este programa combina dos dispositivos I2C en el mismo bus:

🌡️ Sensor AHT10/AHT20 en la dirección 0x38
📺 Pantalla OLED SSD1306 128x64 en la dirección 0x3C

El sistema lee la temperatura y la humedad del sensor y actualiza la pantalla cada 0,5 segundos, mostrando los valores en grande.

⚙️ Hardware necesario
ESP32 / ESP32-S3
Sensor AHT10 o AHT20
Pantalla OLED SSD1306 128x64
Cables Dupont
🔌 Conexiones
Señal	Pin ESP32
SDA	GPIO 8
SCL	GPIO 9
VCC	3.3V
GND	GND
📍 Direcciones I2C
Dispositivo	Dirección
OLED SSD1306	0x3C
Sensor AHT	0x38
🧠 Funcionamiento

El programa inicializa el bus I2C a 400 kHz, comprueba que la OLED y el sensor responden, inicializa ambos dispositivos y después entra en un bucle de lectura continua.

Cada ciclo realiza:

Lectura del sensor AHT.
Conversión de datos RAW a temperatura y humedad.
Impresión de valores por Monitor Serie.
Actualización de la pantalla OLED.
📺 Visualización en pantalla

La OLED muestra:

AHT SENSOR

TEMP: 24.5 C

HUM : 48.2 %

Si ocurre un error, muestra mensajes como:

ERROR
NO SENSOR 0x38

o:

ERROR
ERROR LECTURA
SENSOR 0x38
🧩 Partes principales del código
Configuración I2C
constexpr uint8_t SDA_PIN = 8;
constexpr uint8_t SCL_PIN = 9;
constexpr uint32_t I2C_FREQ = 400000;
Direcciones de dispositivos
constexpr uint8_t OLED_ADDR = 0x3C;
constexpr uint8_t AHT_ADDR  = 0x38;
Lectura del sensor
Wire.write(0xAC);
Wire.write(0x33);
Wire.write(0x00);
Conversión de humedad
humidityRH = (rawHumidity * 100.0f) / 1048576.0f;
Conversión de temperatura
temperatureC = (rawTemp * 200.0f) / 1048576.0f - 50.0f;
🖥️ Salida por Monitor Serie

Ejemplo:

Iniciando sistema I2C...
SDA = GPIO 8
SCL = GPIO 9
Temperatura: 24.5 C | Humedad: 48.2 %
🛠️ Características del proyecto
Comunicación I2C con dos dispositivos.
Driver OLED implementado manualmente.
Uso de framebuffer propio.
Fuente bitmap 5x7 incluida en el código.
Texto escalado para mostrar valores grandes.
Lectura periódica cada 500 ms.
Mensajes de error en Serial y pantalla.
📚 Librerías usadas
Arduino.h
Wire.h

No se utilizan librerías externas para la OLED ni para el sensor.

🎯 Objetivo de la práctica

El objetivo es entender cómo usar el bus I2C para comunicar varios periféricos con el microcontrolador, leyendo datos de un sensor y mostrándolos en una pantalla OLED.
