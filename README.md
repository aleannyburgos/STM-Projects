# MPU6050 Data Reader

A lightweight STM32 HAL-based driver for the **MPU6050** 6-axis accelerometer and gyroscope.

This project demonstrates how to initialize the sensor over I²C, read accelerometer, gyroscope, and temperature data, and send the values over UART to a serial terminal.

---

## Hardware
- **STM32 Nucleo-L476RG** development board  
- **MPU6050 IMU Sensor** (I²C interface)  
- **USB connection** for power and serial communication  

### Pin Connections
| MPU6050 | STM32 Nucleo-L476RG |
|----------|---------------------|
| VCC      | 3.3V               |
| GND      | GND                |
| SCL      | PB8 (I2C1_SCL)     |
| SDA      | PB9 (I2C1_SDA)     |
| AD0      | GND *(I2C address = 0x68)* |

---

## Software
- **STM32CubeIDE**  
- **STM32 HAL drivers** enabled (`I2C1`, `USART2`)  
- Build configuration: *Debug / Release*  
- UART baud rate: **115200, 8N1**

### Building
1. Clone this repository.  
2. Open the `.ioc` file in STM32CubeIDE.  
3. Generate code and build the project.  
4. Flash it to the Nucleo board.

### Serial Monitor
Use any terminal at 115200 baud:
bash
screen /dev/ttyACM0 115200

## Functions
MPU6050_Init()
- Initializes the MPU6050 module.
- Verifies device ID (WHO_AM_I register = 0x68).
- Wakes the device from sleep mode.
- Configures:
    Gyroscope → ±250°/s, Accelerometer → ±2g, Sample rate → 8 kHz
  
MPU6050_Read_Accel()
- Reads data from the six accelerometer registers and converts them into the corresponding X, Y, Z acceleration values (g).
- Updates global variables:
    Accel_X_RAW, Accel_Y_RAW, Accel_Z_RAW, and Ax, Ay, Az.

MPU6050_Read_Gyro()
- Reads data from the six gyroscope registers and converts them into the corresponding X, Y, Z angular velocity values (°/s).
- Updates:
    Gyro_X_RAW, Gyro_Y_RAW, Gyro_Z_RAW, and Gx, Gy, Gz.

MPU6050_Read_Temp()
- Reads data from the two temperature registers and converts it to °C.
- Updates the global variable temp.

## Documentation & References 
- **MPU6050 Datasheet** — [InvenSense MPU-6000/6050 Register Map and Descriptions](https://invensense.tdk.com/download-pdf/mpu-6000-register-map/)
- **STM32 HAL API Reference** — [STMicroelectronics HAL Library Documentation](https://www.st.com/en/embedded-software/stm32cube-mcu-packages.html)
- **NUCLEO-L476RG Board User Manual** — [UM1724 on st.com](https://www.st.com/resource/en/user_manual/dm00105823.pdf)
- **I²C and UART Configuration** — STM32CubeIDE auto-generated code examples
  
**Formula Reference:**
- *Accelerometer scaling:* 1 g = 16384 LSB (for ±2g)
- *Gyroscope scaling:* 1 °/s = 131 LSB (for ±250°/s)
- *Temperature:* Temp(°C) = (Raw / 340) + 36.53
