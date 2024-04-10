# Atividades de Laboratório - Sistemas Embarcados I

# Ava Soriano Rezende - 11921EBI011

## 1. O programa disponibilizado na pasta **stm32f411-blackpill** pisca o LED conectado ao pino PC13 no kit STM32F411 Blackpill. Faça um *fork* deste repositório e altere o programa para que, ao se pressionar o botão conectado a PA0 o LED fique aceso e, ao soltar este botão, o LED se apague.

R: Acender o LED quando o botão conectado a PA0 for pressionado, você pode seguir estas etapas:
1) Identificar o Pino do Botão: verifique qual pino do microcontrolador STM32F411 Blackpill está conectado ao botão PA0. Certifique-se de que o botão esteja conectado corretamente.
2) Configurar o Pino do Botão: no código, configure o pino PA0 como entrada digital. Isso permitirá que você leia o estado do botão.
3) Ler o Estado do Botão: dentro do loop principal, leia o estado do botão (se está pressionado ou solto).
4) Controlar o LED: se o botão estiver pressionado, acenda o LED conectado ao pino PC13.Se o botão estiver solto, apague o LED.

#include "stm32f4xx.h"

    int main(void)
    {
        // Configurar o pino PA0 como entrada
        RCC->AHB1ENR |= RCC_AHB1ENR_GPIOAEN; GPIOA->MODER &= ~GPIO_MODER_MODER0;
    
        // Configurar o pino PC13 como saída
        RCC->AHB1ENR |= RCC_AHB1ENR_GPIOCEN; GPIOC->MODER |= GPIO_MODER_MODER13_0;
    
        while (1)
        {
            // Ler o estado do botão (PA0)
            if (GPIOA->IDR & GPIO_IDR_IDR_0)
            {
                // Botão pressionado: acender o LED (PC13)
                GPIOC->BSRR = GPIO_BSRR_BS_13;
            }
            else
            {
                // Botão solto: apagar o LED (PC13)
                GPIOC->BSRR = GPIO_BSRR_BR_13;
            }
        }
    }

## 2. Faça um novo *fork* deste repositório e altere o programa para que, ao se pressionar o botão conectado a PA0 o estado do LED seja trocado, ou seja, caso o LED esteja apagado ao se pressionar o LED uma vez o mesmo deve acender ao pressionar o botão o LED deverá apagar.

#include "stm32f4xx.h"

int main(void)
{
    // Configurar o pino PA0 como entrada
    RCC->AHB1ENR |= RCC_AHB1ENR_GPIOAEN; GPIOA->MODER &= ~GPIO_MODER_MODER0;

    // Configurar o pino PC13 como saída
    RCC->AHB1ENR |= RCC_AHB1ENR_GPIOCEN; GPIOC->MODER |= GPIO_MODER_MODER13_0;

    // Variável para controlar o estado do LED
    int ledLigado = 0;

    while (1)
    {
        // Ler o estado do botão (PA0)
        if (GPIOA->IDR & GPIO_IDR_IDR_0)
        {
            // Botão pressionado: alternar o estado do LED
            if (ledLigado)
            {
                GPIOC->BSRR = GPIO_BSRR_BR_13; // Apagar o LED
                ledLigado = 0;
            }
            else
            {
                GPIOC->BSRR = GPIO_BSRR_BS_13; // Acender o LED
                ledLigado = 1;
            }

            // Aguardar um breve intervalo para evitar leituras múltiplas
            for (volatile int i = 0; i < 100000; ++i)
            {
                // Espera
            }
        }
    }
}
