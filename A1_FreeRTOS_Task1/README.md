# Multithreading Example with FreeRTOS on STM32

This project demonstrates a basic multithreading application using FreeRTOS on an STM32 microcontroller. Two tasks are created, each printing a message at regular intervals.

## Overview

The main purpose of this project is to illustrate how to set up and use FreeRTOS on an STM32 microcontroller for multithreading applications. It includes two tasks:

1. **Task1**: Prints "Task1" to the console every second.
2. **Task2**: Prints "Task2" to the console every second.

## Setting up SWV ITM Data Console
Open *syscalls.c* file and paste following code bellow `#include <sys/times.h>`

```c
//Debug Exception and Monitor Control Register base address
#define DEMCR                   *((volatile uint32_t*) 0xE000EDFCU )

/* ITM register addresses */
#define ITM_STIMULUS_PORT0   	*((volatile uint32_t*) 0xE0000000 )
#define ITM_TRACE_EN          	*((volatile uint32_t*) 0xE0000E00 )

void ITM_SendChar(uint8_t ch)
{

	//Enable TRCENA
	DEMCR |= ( 1 << 24);

	//enable stimulus port 0
	ITM_TRACE_EN |= ( 1 << 0);

	// read FIFO status in bit [0]:
	while(!(ITM_STIMULUS_PORT0 & 1));

	//Write to ITM stimulus port0
	ITM_STIMULUS_PORT0 = ch;
}
```

After that find function *_write* and replace `__io_putchar(*ptr++)` with `ITM_SendChar(*ptr++)` like in code snippet below
```c
__attribute__((weak)) int _write(int file, char *ptr, int len)
{
	int DataIdx;

	for (DataIdx = 0; DataIdx < len; DataIdx++)
	{
		//__io_putchar(*ptr++);
		ITM_SendChar(*ptr++);
	}
	return len;
}
```

## Steps to Perform

Step 1:
<kbd>![Explore Photos](https://raw.githubusercontent.com/levietduc0712/NUCLEO_F446RE/master/Screenshot/A1_1.png?raw=true)</kbd>

Step 2:
<kbd>![Explore Photos](https://raw.githubusercontent.com/levietduc0712/NUCLEO_F446RE/master/Screenshot/A1_2.png?raw=true)</kbd>

Step 3:
<kbd>![Explore Photos](https://raw.githubusercontent.com/levietduc0712/NUCLEO_F446RE/master/Screenshot/A1_3.png?raw=true)</kbd>

Step 4:
<kbd>![Explore Photos](https://raw.githubusercontent.com/levietduc0712/NUCLEO_F446RE/master/Screenshot/A1_4.png?raw=true)</kbd>

Step 5:
<kbd>![Explore Photos](https://raw.githubusercontent.com/levietduc0712/NUCLEO_F446RE/master/Screenshot/A1_5.png?raw=true)</kbd>

Step 6:
<kbd>![Explore Photos](https://raw.githubusercontent.com/levietduc0712/NUCLEO_F446RE/master/Screenshot/A1_6.png?raw=true)</kbd>

Step 7:
<kbd>![Explore Photos](https://raw.githubusercontent.com/levietduc0712/NUCLEO_F446RE/master/Screenshot/A1_7.png?raw=true)</kbd>


