| Function | MCU Pin | Notes |
| --- | --- | --- |
| Motor 1 signal | PA8 | TIM1 CH1, DShot |
| Motor 2 signal | PA9 | TIM1 CH2, DShot (check UART1 conflict) |
| Motor 3 signal | PA10 | TIM1 CH3, DShot (check UART1 conflict) |
| Motor 4 signal | PA11 | TIM1 CH4, DShot |
| IMU SPI | TBD | ICM-20602, SPI, CS/SCK/MISO/MOSI |
| Receiver UART | TBD | ELRS, avoid USART1 if motors use PA9/PA10 |
