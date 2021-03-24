# การทดลองที่ 2 เรื่อง การเขียนโปรแกรมค้นหาไวไฟ

## วัตุประสงค์
1. เพื่อค้นหาไวไฟโดยใช้ไมโครคอนโทรเลอร์(ESP-01)
2. เพื่อศึกษาวิธีการเขียนโปรแกรมค้นหาไวไฟ

## อุปกรณ์ที่ใช้
1. ไมโครคอนโทรเลอร์(ESP-01)
![Image](https://ae01.alicdn.com/kf/HTB1QMy2J9zqK1RjSZFpq6ykSXXac/ESP8266-ESP-01-ESP01-Serial-WIFI-3-3V-5V-Serial.jpg)
2. สายต่ออุปกรณ์ USB 
3. ซีเรียล
4. คอมพิวเตอร์

## ศึกษาข้อมูลเบื้องต้น
### run example 2
 https://youtu.be/yBjab0UNuB8
 
## วิธีการทำการทดลอง
1. ต่อสาย USB เข้ากับซีเรียล 
2. เสียบไมโครคอนโทรเลอร์(ESP-01)เข้ากับซีเรียล
3. เปิด command prompt เเล้วพิมพ์คำสั่ง **cd pattani** เพื่อเข้าโปรแกรมตัวอย่าง
4. เลือกโปรแกรมตัวอย่างโดยใช้คำสั่ง **cd 02_Scan-Wifi**
5. พิมพ์คำสั่ง **vi src/main.cpp** เเล้วกด Enter จะพบข้อมูลต่อไปนี้
```c
#include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	WiFi.mode(WIFI_STA);
	WiFi.disconnect();
	delay(100);
	Serial.println("\n\n\n");
}

void loop()
{
	Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");
	int n = WiFi.scanNetworks();
	if(n == 0) {
		Serial.println("NO NETWORK FOUND");
	} else {
		for(int i=0; i<n; i++) {
			Serial.print(i + 1);
			Serial.print(": ");
			Serial.print(WiFi.SSID(i));
			Serial.print(" (");
			Serial.print(WiFi.RSSI(i));
			Serial.println(")");
			delay(10);
		}
	}
	Serial.println("\n\n");
}
```
6. อัพโหลดโปรแกรมลงในไมโครคอนโทรนเลอร์ โดยพิมพ์คำสั่ง **pio run -t upload** แล้วกด Enter ในขณะที่รับโปรแกรมใหม่เข้าไปให้กดปุ่มสีดำค้างไว้ แล้วกดปุ่มแดง 1 ครั้ง เพื่อเป็นการ reset คำสั่งเก่า
7. เมื่อทำการลงโปรแกรมเสร็จแล้ว พิมพ์คำสั่ง **pio device monitor** แล้วกด Enter เพื่อดูผลลัพธ์ที่ได้บนหน้าจอคอมพิวเตอร์

## การบันทึกผลการทดลอง
จากการทดลอง ไมโครคอนโทรเลอร์ที่เราอัพโหลดโปรแกรมลงไป พบว่า ไมโครคอนโทรเลอร์จะแสดงไวไฟที่หาเจอเรื่อยๆ ซึ่งไวไฟที่หาเจอแต่ครั้งขึ้นอยู่กับความเร็วสัญญาณไวไฟนั้นๆ
![image](https://user-images.githubusercontent.com/80879589/112296437-7e489a80-8cc7-11eb-86d7-f2995c29841e.png)

## อภิปรายผลการทดลอง
จากการทดลองการเขียนโปรแกรมเเละอัพโหลดลงในไมโครคอนโทรเลอร์ พบว่า ไมโครคอนโทรเลอร์นี้สามารถสแกนตรวจจับค้นหาสัญญาณไวไฟรอบ ๆ ได้

## คำถามหลังการทดลอง



















