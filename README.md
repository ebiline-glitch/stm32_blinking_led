# Automatic Sensor-Based LED Control System Using STM32

## Aim

To interface a digital sensor with an STM32 microcontroller and automatically control an LED according to the sensor output.

## Apparatus Required

| S. No. | Component | Quantity |
|---:|---|---:|
| 1 | STM32 development board | 1 |
| 2 | Digital sensor or push button | 1 |
| 3 | LED | 1 |
| 4 | 220–330 Ω resistor | 1 |
| 5 | Breadboard | 1 |
| 6 | Jumper wires | As required |
| 7 | USB cable | 1 |

## Algorithm

1.Open STM32 software (e.g., STM32CubeIDE).

2.Create a new project for your STM32 board.

3.Enable GPIO clock for the pins you’ll use.

4.Configure sensor pin as digital input.

5.Configure LED pin as digital output.

6.Write main loop to read sensor input.

7.If sensor = HIGH → LED ON.

8.Else → LED OFF.

9.Build and upload code to STM32 board.

10.Observe LED turning ON/OFF automatically based on sensor.


## Program
    #include "stm32f4xx_hal.h"

    int main(void)
    {
    HAL_Init();
    __HAL_RCC_GPIOA_CLK_ENABLE();   // Enable clock for GPIOA

    GPIO_InitTypeDef GPIO_InitStruct = {0};

    // Configure sensor pin (PA0) as input
    GPIO_InitStruct.Pin = GPIO_PIN_0;
    GPIO_InitStruct.Mode = GPIO_MODE_INPUT;
    GPIO_InitStruct.Pull = GPIO_NOPULL;
    HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

    // Configure LED pin (PA5) as output
    GPIO_InitStruct.Pin = GPIO_PIN_5;
    GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
    GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
    HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

    while (1)
    {
        // Read sensor state
        GPIO_PinState sensorState = HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_0);

        if (sensorState == GPIO_PIN_SET)
        {
            // Sensor active → LED ON
            HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);
        }
        else
        {
            // Sensor inactive → LED OFF
            HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET);
        }
    }
    }



## Result

The digital sensor was successfully interfaced with the STM32 microcontroller. The LED connected to `PA5` turned ON when the sensor input at `PA0` was HIGH and turned OFF when the sensor input was LOW.
