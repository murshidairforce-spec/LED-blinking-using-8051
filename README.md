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
The sensor continuously detects the required environmental condition.
The sensor output is given to an STM32 GPIO input pin.
The STM32 processes the sensor signal.
If the programmed condition is satisfied, STM32 sets the LED GPIO HIGH.
Otherwise, it sets the LED GPIO LOW.
Thus, the LED operates automatically without manual switching.



## Program
```
#include "main.h"

void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
    HAL_Init();

    SystemClock_Config();
    MX_GPIO_Init();

    while (1)
    {
        // LED ON
        HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);

        HAL_Delay(1000);

        // LED OFF
        HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET);

        HAL_Delay(1000);
    }
}

static void MX_GPIO_Init(void)
{
    GPIO_InitTypeDef GPIO_InitStruct = {0};

    __HAL_RCC_GPIOA_CLK_ENABLE();

    GPIO_InitStruct.Pin = GPIO_PIN_5;
    GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
    GPIO_InitStruct.Pull = GPIO_NOPULL;
    GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;

    HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);
}
```


## Circuit Diagram
<img width="762" height="637" alt="image" src="https://github.com/user-attachments/assets/1599a148-79d7-438c-a1c7-e43771382753" />



## Result

The digital sensor was successfully interfaced with the STM32 microcontroller. The LED connected to `PA5` turned ON when the sensor input at `PA0` was HIGH and turned OFF when the sensor input was LOW.
