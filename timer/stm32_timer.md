***IC – stm32h735zgt6***



Configure timer 14 for 1 ms

Timer 14 connected to APB1

APB1 timer clock is 275MHz

***Prescaler:***

```
	275 MHz / 275 = 1MHz

	275000000 / 275 = 1000000

	ps  = 275-1
```

***Counter period (Auto reload register):***
```
	1000000 / 1000 = 1000 (1KHz)

	CP = 1000-1
```

It will give 1ms delay


***Configure Prescalar and Counter Period***

![image](https://user-images.githubusercontent.com/91674428/208249022-e65e35f5-11ef-4ce7-a383-f6e53cc60884.png)

***Enable Gloabl Interrupt***

![image](https://user-images.githubusercontent.com/91674428/208249034-ce2ccd9a-11b2-4080-90b7-48e261732ee8.png)

***Ref clock tree***

![image](https://user-images.githubusercontent.com/91674428/208249040-645823a1-226f-4411-9845-fb3c2d61b8e4.png)

Need to start the timer
```
HAL_TIM_Base_Start_IT (&htim14);
```

We can have callback to do some operation once 1ms completed

```
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim)
{
	if (htim == &htim14) {
		HAL_GPIO_TogglePin(GPIOE, GPIO_PIN_4);	/* We can measuare 1ms delay on this pin*/
	}
}
```


For 10 ms delay

***Prescaler:***
```
	275000000 / 27500 = 10000

	ps = 27500-1
```
***Counter period (Auto reload register):***
```
	10000 / 100 = 1 (1Hz)

	CP = 100-1
```


For 1s delay

***Prescaler:***
```
	275000000 / 27500 = 10000

	ps = 27500-1
```
***Counter period (Auto reload register):***
```
	10000 / 10000 = 1 (1Hz)

	CP = 10000-1
```
