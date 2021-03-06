Azure MQTT Demo
===============

This demo application connects to 
[Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/) 
through MQTT, sends messages and checks for receive confirmation.

It requires a registered [device](https://www2.keil.com/iot/microsoft) in the Azure IoT hub.

The following describes the various components and the configuration settings.

Once the application is configured you can:
 - Build the application
 - Connect the debugger
 - Run the application and view messages in a debug printf or terminal window


Azure IoT Client
----------------
The file `iothub_ll_telemetry_sample_mdk.c` configures the connection to 
Azure IoT Hub with these settings:
 - connectionString: Connection string - primary key

Note: These settings need to be configured by the user!


FreeRTOS Real-Time Operating System
-----------------------------------
The [FreeRTOS RTOS](https://github.com/ARM-software/CMSIS-FreeRTOS) 
implements the resource management. It is configured with the following settings:

- Global Dynamic Memory size: 24000 bytes
- Default Thread Stack size: 3072 bytes


WiFi IoT Socket
---------------
This implementation uses an IoT socket layer that connects to a 
[CMSIS-Driver WiFi](https://arm-software.github.io/CMSIS_5/Driver/html/index.html).

The file `socket_startup.c` configures the WiFi connection with these settings:
 - SSID:          network identifier
 - PASSWORD:      network password
 - SECURITY_TYPE: network security

Note: These settings need to be configured by the user!


ESP8266 WiFi Module
-------------------
The [ESP8266 WiFi Module](https://www2.keil.com/iot/shields/wrl13287) 
is connected via an Arduino connector using a USART interface.
It exposes a **CMSIS-Driver WiFi**.


STMicroelectronics 32F746GDISCOVERY Target Board
------------------------------------------------
The Board layer contains the following configured interface drivers:

**CMSIS-Driver USART6** routed to Arduino UNO R3 connector (CN4):
 - RX: D0 USART6_RX (PC7)
 - TX: D1 USART6_TX (PC6)

**CMSIS-Driver MCI0** routed to memory card socket (CN3):
 - DATA0: SDMMC_D0 (PC8)
 - DATA1: SDMMC_D1 (PC9)
 - DATA2: SDMMC_D2 (PC10)
 - DATA3: SDMMC_D3 (PC11)
 - CMD:   SDMMC_CMD (PD2)
 - CLK:   SDMMC_CK (PC12)
 - CD:    MicroSDcard_detect (PC13)

**STDOUT** routed to ITM

The board configuration can be modified using 
[STM32CubeMX](https://www.keil.com/stmicroelectronics-stm32) 
and is stored in the file `STCubeGenerated.ioc`.
