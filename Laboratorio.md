# Atividades de Laboratório - Sistemas Embarcados I

1. O programa disponibilizado na pasta **stm32f411-blackpill** pisca o LED conectado ao pino PC13 no kit STM32F411 Blackpill. Faça um *fork* deste repositório e altere o programa para que, ao se pressionar o botão conectado a PA0 o LED fique aceso e, ao soltar este botão, o LED se apague.

Acender o LED quando o botão conectado a PA0 for pressionado, você pode seguir estas etapas:
1) Identificar o Pino do Botão: verifique qual pino do microcontrolador STM32F411 Blackpill está conectado ao botão PA0. Certifique-se de que o botão esteja conectado corretamente.
2) Configurar o Pino do Botão: no código, configure o pino PA0 como entrada digital. Isso permitirá que você leia o estado do botão.
3) Ler o Estado do Botão: dentro do loop principal, leia o estado do botão (se está pressionado ou solto).
4) Controlar o LED: se o botão estiver pressionado, acenda o LED conectado ao pino PC13.Se o botão estiver solto, apague o LED.

2. Faça um novo *fork* deste repositório e altere o programa para que, ao se pressionar o botão conectado a PA0 o estado do LED seja trocado, ou seja, caso o LED esteja apagado ao se pressionar o LED uma vez o mesmo deve acender ao pressionar o botão o LED deverá apagar.
