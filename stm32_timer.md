IC – stm32h735zgt6

Configure timer 14 for 1 ms

Timer 14 connected to APB1

APB1 timer clock is 275MHz

Prescaler:

	275 MHz / 275 = 1MHz

275000000 / 275 = 1000000

ps  = 275-1

Counter period (Auto reload register):

	1000000 / 1000 = 1000 (1KHz)

	CP = 1000-1

	It will give 1ms delay

We can have callback to do some operation once 1ms completed

```
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim)
{
	if (htim == &htim14) {
		One_MS_Completed = true;
		HAL_GPIO_TogglePin(GPIOE, GPIO_PIN_4);	//this pin we can toggle and check
	}
}
```


For 10 ms delay

Prescaler:

275000000 / 27500 = 10000

ps = 27500-1

Counter period (Auto reload register):

	10000 / 100 = 1 (1Hz)

	CP = 100-1



For 1s delay

Prescaler:

275000000 / 27500 = 10000

ps = 27500-1

Counter period (Auto reload register):

	10000 / 10000 = 1 (1Hz)

	CP = 10000-1

