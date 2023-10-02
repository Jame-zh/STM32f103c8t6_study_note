# GPIO芯片内部电路原理  
## STM32输出模式：推挽输出、开漏输出//HAL_GPIO_WritePin();
### 1. 推挽输出
![image](https://github.com/Jame-zh/STM32f103c8t6_study_note/assets/141942637/de6de266-8923-4f1f-904e-fc8125f2495a)
![image](https://github.com/Jame-zh/STM32f103c8t6_study_note/assets/141942637/c0ed633a-e5fa-4efa-b296-c41873f3eece)

### 2. 开漏输出
![image](https://github.com/Jame-zh/STM32f103c8t6_study_note/assets/141942637/d108cbe2-c93a-4848-a755-8819b811b88e)  

注：推挽输出在低电平时输出0V，在高电平时输出3.3V  
    开漏输出在低电平时输出0V（断路），在高电平时输出电压由外部电路决定

## STM32输入模式：浮空输入、上拉输入、下拉输入//HAL_GPIO_ReadPin();

