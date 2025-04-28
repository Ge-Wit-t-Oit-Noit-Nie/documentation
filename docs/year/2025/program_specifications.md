# Programnma specificaties

## Pins & Functies

* *USART3*: Serial port voor sturen van informatie
* *SYS*: Debug: Serial wire, Timebase Source: TIM1
* *RCC*: High speed clock and low speed clock based on cristals build in  
* *SPI1*: SD Card writer over SPI
* *EXTI line 1*: Voor interrupt
* *EXTI line 15*: Voor interrupt

### PINS

| PIN  | Assignment  |
| ---- | ----------- |
| PA4  | SPI1_CS     |
| PA5  | SPI1_SCK    |
| PA6  | SPI1_MISO   |
| PA7  | SPI1_MOSI   |
| PA13 | SYS_JTMS-SWDIO |
| PA14 | SYS_JTMS-SWCLK |
| PB0  | LED 1 [Green] - DefaultTask running |
| PB1  | GPIO External Interrupt mode with Rise Edge trigger detection - Emergency button |
| PB3  | SYT_JTDO-SWO |
| PB7  | LED 2 [Blue] |
| PB14 | LED 3 [Red] - HardFault_Handler entered |
| PC14 | RCC_OSC32 |
| PC15 | RCC_OSC32_OUT |
| PD8  | UART3_TX |
| PD9  | UART3_RX |
| PH0  | RCC_OSC_IN |
| PH1  | RCC_OSC_OUT |
