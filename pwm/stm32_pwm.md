***IC – stm32h735zgt6 - LQFP144***

Configure PA8 with 5KHz PWM

PA8 – TIM1 (16 bit)

Edit CUBE IDE -> ioc -> PA8 -> TIM1_CH1

![image](https://user-images.githubusercontent.com/91674428/208280551-fbe10d2f-4e75-4886-8117-6cf4bdd2d121.png)

 
Timers configuration -> TIM1 -> channel 1 -> PWN Generation CH1
 
![image](https://user-images.githubusercontent.com/91674428/208280554-5a6a6e51-6023-42c7-968e-9954ca345a3f.png)


TIM1 connected to APB2 -> Timer clock is 275 MHz (sys clock is 550MHz)

![image](https://user-images.githubusercontent.com/91674428/208280563-36e8dfa5-be8f-4c53-9eea-abd3c6127900.png)

 
***Parameters:***

***Prescaler setting: for 5KHz***
```
    275 MHz / 275 = 1 MHz

    275000000 / 275 = 1000000

    So the prescaler will be 275
```
***Counter Period:***
```
    We need 5 KHz (5000)

    1 MHz / 200 = 5 KHz

    1000000 / 200 = 5000

    So the Counter period will be 200
```

`Note: If we do like this way the Duty cycle will be like 0-200% not 0-100%, we may need to keep the counter period 100`

So let’s recalculate for 5KHz

***Prescaler setting:***
```
    275 MHz / 550 = 0.5 MHz (500KHz)

    275000000 / 550 = 500000

    So the prescaler will be 550-1
```
***Counter Period: (100 will be nominal if we are going to use 0-100%)***
```
    We need 5 KHz (5000)

    500 KHz / 100 = 5 KHz

    500000 / 100 = 5000

    So the Counter period will be 100-1
```
Now we can change the PWM Duty cycle from 0-100%

***Configuration***

![image](https://user-images.githubusercontent.com/91674428/208280669-50c08d35-8666-4b75-9140-9e5ab0751ee0.png)


![image](https://user-images.githubusercontent.com/91674428/208280815-59aedcf3-1a7d-440d-b25c-657ec04e9a53.png)


![image](https://user-images.githubusercontent.com/91674428/208280816-9d6ba443-7bbc-41d8-87f5-99b2620b777a.png)


![image](https://user-images.githubusercontent.com/91674428/208280818-dc9ded4c-de6c-4324-853c-e695396a651c.png)


![image](https://user-images.githubusercontent.com/91674428/208280820-bd6b4309-3078-4bae-9277-9ce4fe207262.png)


![image](https://user-images.githubusercontent.com/91674428/208280822-57dc24d2-ed7d-49b8-91af-4c7ddf43ac4c.png)



 
 
 
 
 

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
 

![image](https://user-images.githubusercontent.com/91674428/208280825-53fb3613-23fc-4ace-b621-171d7053897b.png)
