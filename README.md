# ESP32 I2C MPU6050 driver for esp-idf

## 简介
* 包含二个版本
  * main_c:C版本,用的是InvenSense
  * main: cpp版本,带卡尔曼滤波,稳定定比较好.
* cpp版本老外的原注解:
  * It uses hardware I2C port. So you can at most connect two sensors on the same chip with different I2C port number. The clock speed is 400khz. In my practice, the maximum data refresh rate is about 250Hz.

## 硬件配置
* 使用的IO:
  * i2c_gpio_sda = (gpio_num_t)1;
  * i2c_gpio_scl = (gpio_num_t)2;

## idf版本
* 4.3.1

## 配置目标芯片
* 默认配置为esp32c3
```
idf.py set-target esp32c3
```
## 编译
```
idf.py build
```
## 烧写
```
idf.py -p comX flash ; idf.py -p  comX monitor
```
## 效果
```
Samples:580  Acc:(0.04,-0.00,-0.84)Gyro:( 0.244,-0.084, 0.069) Pitch:-2.872  Roll: 0.117  FPitch:-2.665  FRoll: 0.077
Samples:580  Acc:(0.04,-0.00,-0.84)Gyro:(-0.099,-0.031, 0.069) Pitch:-2.781  Roll: 0.033  FPitch:-2.737  FRoll: 0.019
Samples:579  Acc:(0.00,0.05,-0.86)Gyro:(-2.664,-0.229, 2.656) Pitch:-0.049  Roll:-3.517  FPitch: 0.142  FRoll:-3.099
Samples:577  Acc:(-0.05,0.99,0.09)Gyro:(-1.198,-0.069, 0.282) Pitch:-30.267  Roll:85.037  FPitch:-34.599  FRoll:91.668
Samples:576  Acc:(-0.05,0.99,0.08)Gyro:( 0.183, 0.069, 0.107) Pitch:-30.862  Roll:85.327  FPitch:-30.499  FRoll:85.456
Samples:577  Acc:(-0.12,0.24,-0.40)Gyro:(76.282,11.542, 7.740) Pitch:16.667  Roll:-30.886  FPitch: 5.922  FRoll:-51.361
```
## 注意
* 配置i2c参数时,需要加以下这句,否则很容易引起"i2c clock choice is invalid"
  ``` 
  conf.clk_flags = 0;
  ```
