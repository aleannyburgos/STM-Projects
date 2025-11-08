# 🧭 MPU6050 Data Reader

A lightweight STM32 HAL-based driver for the **MPU6050** 6-axis accelerometer and gyroscope.

This project demonstrates how to initialize the sensor over I²C, read accelerometer, gyroscope, and temperature data, and send the values over UART to a serial terminal.

---

## ⚙️ Hardware

- **STM32 Nucleo-L476RG** development board  
- **MPU6050 IMU Sensor** (I²C interface)  
- **USB connection** for power and serial communication  

### 🔌 Pin Connections
| MPU6050 | STM32 Nucleo-L476RG |
|----------|---------------------|
| VCC      | 3.3V               |
| GND      | GND                |
| SCL      | PB8 (I2C1_SCL)     |
| SDA      | PB9 (I2C1_SDA)     |
| AD0      | GND *(I2C address = 0x68)* |

---

## 💻 Software

- **STM32CubeIDE**  
- **STM32 HAL drivers** enabled (`I2C1`, `USART2`)  
- Build configuration: *Debug / Release*  
- UART baud rate: **115200, 8N1**

### 🧱 Building
1. Clone this repository.  
2. Open the `.ioc` file in STM32CubeIDE.  
3. Generate code and build the project.  
4. Flash it to the Nucleo board.

### 🖥️ Serial Monitor
Use any terminal at 115200 baud:
```bash
screen /dev/ttyACM0 115200
