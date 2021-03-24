# การทดลองที่ 1 เรื่อง การเขียนโปรแกรมเพื่อรันบนไมโครคอนโทรเลอร์

## วัตุประสงค์
1.เพื่อศึกษาวิธีการทำงานพื้นฐานของไมโครคอนโทรเลอร์
2.เพื่อศึกษาวิธีการใช้งานของไมโครคอนโทรเลอร์
3.เพื่อให้เข้าใจถึงการเขียนโปรแกรมเพื่อรันบนไมโครคอนโทรเลอร์

## อุปกรณ์ที่ใช้
1.ไมโครคอนโทรเลอร์(ESP-01)
![Image](https://ae01.alicdn.com/kf/HTB1QMy2J9zqK1RjSZFpq6ykSXXac/ESP8266-ESP-01-ESP01-Serial-WIFI-3-3V-5V-Serial.jpg)
2.สายต่ออุปกรณ์ USB 
3.ซีเรียล
4.คอมพิวเตอร์
## ศึกษาข้อมูลเบื้องต้น
### run example 1
https://youtu.be/NLIUsWLEpmg
### PlatformIO
https://platformio.org/

## วิธีการทำการทดลอง
1.ต่อสาย USB เข้ากับซีเรียล 
2.เสียบไมโครคอนโทรเลอร์(ESP-01)เข้ากับซีเรียล
3.เปิด command prompt เเล้วพิมพ์คำสั่ง **cd pattani** เพื่อเข้าโปรแกรมตัวอย่าง
4.เลือกโปรแกรมตัวอย่างโดยใช้คำสั่ง **cd 01_Serial-Monitor**
5.พิมพ์คำสั่ง **vi src/main.cpp** เเล้วกด Enter จะพบข้อมูลต่อไปนี้
```c
#include <Arduino.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
}

void loop()
{
	cnt++;
	Serial.printf("PATTANI :%d\n",cnt);
	delay(1000);
}
```
6.พิมพ์คำสั่ง **vi platformio.ini** เเล้วกด Enter จะสามารถเช็คคุณสมบัติของบอร์ดได้ จะเเสดงดังนี้
```
; IOT for KIDS
;
; By Dr.Choompol Boonmee
;

[env:exercise01]
platform = espressif8266
board = esp01_1m
framework = arduino
board_build.flash_mode = dout

upload_port = /dev/cu.usbserial-1420
;up;oad_port = COM3

monitor_port = /dev/cu.usbserial-1420
;monitor_port = COM3
monitor_speed = 115200
```
7.อัพโหลดโปรแกรมลงในไมโครคอนโทรนเลอร์ โดยพิมพ์คำสั่ง **pio run -t upload** แล้วกด Enter ในขณะที่รับโปรแกรมใหม่เข้าไปให้กดปุ่มสีดำค้างไว้ แล้วกดปุ่มแดง 1 ครั้ง เพื่อเป็นการรีเซตคำสั่งเก่า
8.เมื่อทำการลงโปรแกรมเสร็จแล้ว พิมพ์คำสั่ง **pio device monitor** แล้วกด Enter เพื่อดูผลลัพธ์ที่ได้บนหน้าจอคอมพิวเตอร์

## การบันทึกผลการทดลอง
จากการทดลอง ไมโครคอนโทรเลอร์ที่เราอัพโหลดโปรแกรมลงไป พบว่า สามารถนับจำนวนครั้งได้ทุกๆ 1 วินาที จะบวกเพิ่มขึ้นที่ละ 1 (+1) เเละเมื่อกดปุ่มสีเเดงจะสามารถ reset ค่า เเล้วเริ่มนับจากหนึ่งใหม่ไปเรื่อยๆ
![image](https://user-images.githubusercontent.com/80879589/112291448-b4375000-8cc2-11eb-9906-0ba005b59184.png)

## อภิปรายผลการทดลอง

 



















