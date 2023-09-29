# OLED屏幕(本笔记基于0.96OLED显示屏)
## 注：需要接触到的工具：IIC通信、汉字和图片取模
### 1. OLED屏基本情况
分辨率：128*64（128列，64行），分为8页（128列，8行）  
如何控制小灯的亮灭？用十六进制数控制每一页某一列八个像素点的亮灭
### 2. cubeMX设置
打开I2C1，更改Fast Mode  
RCC打开外部晶振，并设置时钟  
### 3. 编辑器
#### （1）oled.h
`#include "i2c.h"
void OLED_NewFrame()；
void OLED_ShowFrame();`
#### （2）oled.c
`void OLED_NewFrame() {
  memset(OLED_GRAM, 0, sizeof(OLED_GRAM));
}//清空显存，绘制新的一帧画面`
`void OLED_ShowFrame() {
  static uint8_t sendBuffer[OLED_COLUMN + 1];
  sendBuffer[0] = 0x40;
  for (uint8_t i = 0; i < OLED_PAGE; i++) {
    OLED_SendCmd(0xB0 + i); // 设置页地址
    OLED_SendCmd(0x02);     // 设置列地址低4位
    OLED_SendCmd(0x10);     // 设置列地址高4位
    memcpy(sendBuffer + 1, OLED_GRAM[i], OLED_COLUMN);
    OLED_Send(sendBuffer, OLED_COLUMN + 1);
  }
}//将显存显示到屏幕上`
 
#### （3）main.c
`
HAL_Delay(20);//oled屏幕的启动比单片机的启动晚20ms  
OLED_Init();
OLED_NewFrame();
OLED_ShowFrame();
`
#### （4）图片和汉字取模
在波特律动助手网页端取模后，将生成的图模数据放到font.c的最后，并在font.h中extern导出  
选择阴码，将生成的图模数据放到font.c的最后，并在font.h中extern导出，在font.c中更改ASCII的大小
再在main.c中利用OLED_DrawImage(x, y, 图模的指针， 颜色(OLED_COLOR_NORMAL))；或OLED_PrintString(x, y, "字符串", 字体（默认为&font16x16，即为font.h中extern的字体），颜色(OLED_COLOR_NORMAL));

