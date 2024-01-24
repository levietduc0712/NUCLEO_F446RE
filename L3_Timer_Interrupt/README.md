# NUCLEO-F446RE Timer-6 LED Toggle

This example demonstrates how to use Timer 6 on the NUCLEO-F446RE development 
board to toggle the Green LED every 1000 milliseconds.

## Hardware Requirements

- NUCLEO-F446RE development board
- Green LED connected to Pin PA05

## Timer
The Nucleo F446RE board has a microcontroller that supports several types of timers, such as basic (Timer 6 & Timer 7), general-purpose (16-bit: Timer 9 to Timer 14, 32-bit: Timer 2 to Timer 5), advanced (Timer 1 & Timer 8), and low-power timers. Each timer has different features and capabilities, such as output compare, input capture, pulse width modulation, etc. One of the basic timers in the Nucleo F446RE is TIM6, which has a 16-bit counter and a prescaler. A prescaler is a value that divides the main clock frequency to set the timer speed. 

For example, based on page 59 of the manual TIM6 on the APB1 bus, if the bus clock is 16MHz and the prescaler is 16000, the timer will tick at 1 kHz (16 MHz / 16000).

CNTx_CLK = TIMx_CLK/(PRESCALER + 1)

So, Frequency = 1kHz => Time for one tick of timer = 1 second / 1kHz = 1ms 
That means in 1 second, the timer will count 1000 counts.

## Software Requirements

- STM32CubeIDE or any STM32 development environment
