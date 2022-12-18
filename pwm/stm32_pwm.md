***IC – stm32h735zgt6***

Configure PA8 with 5KHz PWM (STM32H735ZGT6 – LQFP144)

PA8 – TIM1 (16 bit)

Edit CUBE IDE -> ioc -> PA8 -> TIM1_CH1
 
Timers configuration -> TIM1 -> channel 1 -> PWN Generation CH1
 


TIM1 connected to APB2 -> Timer clock is 275 MHz (sys clock is 550MHz)
 
***Parameters:***

***Prescaler setting: for 5KHz***

1.	275 MHz / 275 = 1 MHz

275000000 / 275 = 1000000

So the prescaler will be 275

***Counter Period:***

2.	We need 5 KHz (5000)

1 MHz / 200 = 5 KHz

1000000 / 200 = 5000

So the Counter period will be 200

Note: If we do like this way the Duty cycle will be like 0-200% not 0-100%, we may need to keep the counter period 100

So let’s recalculate for 5KHz

***Prescaler setting:***

1.	275 MHz / 550 = 0.5 MHz (500KHz)

275000000 / 550 = 500000

So the prescaler will be 550-1

***Counter Period: (100 will be nominal if we are going to use 0-100%)***

2.	We need 5 KHz (5000)

500 KHz / 100 = 5 KHz

500000 / 100 = 5000

So the Counter period will be 100-1

Now we can change the PWM Duty cycle from 0-100%
 
 
 
 
 
 

Save and proceed
Start the timer
```
    HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_1);
```
To change the PWM values you can change the below register
```
    TIM1->CCR1 = 10;
    TIM1->CCR1 = 25;
    TIM1->CCR1 = 50;
    TIM1->CCR1 = 75;
    TIM1->CCR1 = 100;
```
CCR1 is the determines the Duty cycle

So at starting start the timer and in the runtime we can change the Duty cycle by assigning the values to the TIM1->CCR1 register

```
while (1)
{
    HAL_TIM_PWM_Start(&htim3, TIM_CHANNEL_1);
	TIM3->CCR1 = 30;

    HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_1);
	TIM1->CCR1 = 150;  
      .
      .
      .
```



***Prescaler setting: for 1 KHz***
```
    275000000 / 2750 = 100000
So the prescaler will be 2750-1
```
***Counter Period: (100 will be nominal if we are going to use 0-100%)***
```
    100000 / 100 = 1000
    So the Counter period will be 100-1
```

For some reason TIM3 needed to enable the Clock Source 

But some time it worked without Clock Source too, not sure
 
