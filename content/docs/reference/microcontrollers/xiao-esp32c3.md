---
title: "Seeed XIAO ESP32C3"
weight: 3
---

The [Seeed XIAO ESP32C3](https://www.seeedstudio.com/Seeed-XIAO-ESP32C3-p-5431.html) is an IoT mini development board based on the Espressif [ESP32-C3](https://www.espressif.com/sites/default/files/documentation/esp32-c3_datasheet_en.pdf) WiFi/Bluetooth dual-mode chip.

## Interfaces

| Interface | Hardware Supported | TinyGo Support |
| --------- | ------------------ | -------------- |
| GPIO      | YES                | YES            |
| UART      | YES                | YES            |
| SPI       | YES                | YES            |
| I2C       | YES                | YES            |
| ADC       | YES                | YES            |
| PWM       | YES                | YES            |
| WiFi      | YES                | Not Yet        |
| Bluetooth | YES                | Not Yet        |

## Pins

| Pin   | Hardware pin | Alternative names | ADC      |
| ----- | ------------ | ----------------- | -------- |
| `D0`  | `GPIO2`      | `A0`              | ADC1_CH1 |
| `D1`  | `GPIO3`      | `A1`              | ADC1_CH2 |
| `D2`  | `GPIO4`      | `A2`              | ADC1_CH3 |
| `D3`  | `GPIO5`      | `A3`              | ADC1_CH4 |
| `D4`  | `GPIO6`      | `SDA_PIN`         | -        |
| `D5`  | `GPIO7`      | `SCL_PIN`         | -        |
| `D6`  | `GPIO21`     | `UART_TX_PIN`     | -        |
| `D7`  | `GPIO20`     | `UART_RX_PIN`     | -        |
| `D8`  | `GPIO8`      | `SPI_SCK_PIN`     | -        |
| `D9`  | `GPIO9`      | `SPI_SDI_PIN`     | -        |
| `D10` | `GPIO10`     | `SPI_SDO_PIN`     | -        |

## Machine Package Docs

[Documentation for the machine package for the Seeed XIAO ESP32C3](../machine/xiao-esp32c3)

## Flashing

### CLI Flashing

- Flash your TinyGo program to the board using this command:
    ```shell
    tinygo flash -target=xiao-esp32c3 [PATH TO YOUR PROGRAM]
    ```
- The XIAO ESP32C3 board should restart and then begin running your program.

非常好的建议。我们可以在文档中添加这个构建命令，并解释一下各个参数的作用。让我们更新一下文档的 Flashing 部分：

## Flashing and Building

### CLI Building

To build your TinyGo program without flashing it to the board, you can use the following command:

```shell
tinygo build -o blinky.elf -size=short -gc=leaking --panic=trap -target=xiao-esp32c3 [PATH TO YOUR PROGRAM]
```

This command compiles your program and creates an ELF file. 

### CLI Flashing

To compile and flash your program to the board in one step, use:

```shell
tinygo flash -port /dev/ttyUSB0 -target=xiao-esp32c3 [PATH TO YOUR PROGRAM]
```

This command is similar to the build command, but it also flashes the program to the board.


## Notes

- The XIAO ESP32C3 supports both WiFi and Bluetooth functionality. However, TinyGo's support for Bluetooth on this board may be limited or in development.
- The USB port on the XIAO ESP32C3 can be used as a serial port for debugging and communication.
- When using WiFi functionality, be mindful of power consumption as it can significantly affect battery life in portable projects.
- The board uses the build tag `xiao_esp32c3` for conditional compilation.
- UART: `UART_TX_PIN` is `GPIO21` (D6) and `UART_RX_PIN` is `GPIO20` (D7).
- I2C: `SDA_PIN` is `GPIO6` (D4) and `SCL_PIN` is `GPIO7` (D5).
- SPI: `SPI_SCK_PIN` is `GPIO8` (D8), `SPI_SDI_PIN` is `GPIO9` (D9), and `SPI_SDO_PIN` is `GPIO10` (D10).
- Analog pins (ADC): A0-A3 correspond to D0-D3 respectively.

## Example Usage

Here's a simple example that demonstrates how to use the UART (serial communication) on the XIAO ESP32C3


```go
package main

import (
    "machine"
    "time"
    "fmt"
)

func main() {
    uart := machine.UART0
    uart.Configure(machine.UARTConfig{
        BaudRate: 115200,
        TX:       machine.D6, // UART_TX_PIN for XIAO ESP32C3
        RX:       machine.D7, // UART_RX_PIN for XIAO ESP32C3
    })

    for {
        fmt.Fprintln(uart, "Hello from Seeedstudio")
        time.Sleep(time.Second)
    }
}

```

To compile and flash this program:

```shell
tinygo flash -port /dev/ttyUSB0 -target=xiao-esp32c3 uart.go
```
