# การทดลองที่ 4 เรื่อง การเขียนโปรแกรมอินพุทสัญญาณดิจิทัล

## วัตุประสงค์
1. เพื่อศึกษาการใช้ไมโครคอนโทรเลอร์เป็นอินพุทศัญญาณดิจิทัล
2. เพื่อศึกษาการเขียนโปรแกรมอินพุทสัญญาณดิจิทัลเพื่อรันลงบนไมโครคอนโทรเลอร์

## อุปกรณ์ที่ใช้
1. 1. ไมโครคอนโทรเลอร์(ESP-01)
![Image](https://ae01.alicdn.com/kf/HTB1QMy2J9zqK1RjSZFpq6ykSXXac/ESP8266-ESP-01-ESP01-Serial-WIFI-3-3V-5V-Serial.jpg)
2. สายต่ออุปกรณ์ USB 
3. ซีเรียล
4. Adapter
5. หลอดไฟ LED
6. ตัวเซนเซอร์รับแสงต่อกับตัวต้านทาน
7. คอมพิวเตอร์

## ศึกษาข้อมูลเบื้องต้น
### run example 4
https://youtu.be/nFqoZT26U5k

## วิธีการทำการทดลอง
1. ต่อสาย USB เข้ากับซีเรียล 
2. เสียบ Adapter เข้ากับซีเรียล
3. เสียบไมโครคอนโทรเลอร์(ESP-01)เข้ากับ Adapter
4. เปิด command prompt เเล้วพิมพ์คำสั่ง **cd pattani** เพื่อเข้าโปรแกรมตัวอย่าง
5. เลือกโปรแกรมตัวอย่างโดยใช้คำสั่ง **cd 04_Input-Port**
6. พิมพ์คำสั่ง **vi src/main.cpp** เเล้วกด Enter จะพบข้อมูลต่อไปนี้
(port 0 สีขาว, port 2 สีเหลือง)
```c
#include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	pinMode(0, INPUT);
	pinMode(2, OUTPUT);
	Serial.println("\n\n\n");
}

void loop()
{
	int val = digitalRead(0);
	Serial.printf("======= read %d\n", val);
	if(val==1) {
		digitalWrite(2, LOW);
	} else {
		digitalWrite(2, HIGH);
	}
	delay(100);
}
```
7. อัพโหลดโปรแกรมลงในไมโครคอนโทรนเลอร์ โดยพิมพ์คำสั่ง **pio run -t upload** แล้วกด Enter ในขณะที่รับโปรแกรมใหม่เข้าไปให้กดปุ่มสีดำค้างไว้ แล้วกดปุ่มแดง 1 ครั้ง เพื่อเป็นการ reset คำสั่งเก่า
8. เมื่อทำการลงโปรแกรมเสร็จแล้ว พิมพ์คำสั่ง **pio device monitor** แล้วกด Enter เพื่อดูผลลัพธ์ที่ได้บนหน้าจอคอมพิวเตอร์
![image](https://user-images.githubusercontent.com/80879589/112304173-c1a70700-8ccf-11eb-9169-f84e649474ac.png)
9. นำสายไฟเส้นสีขาวไปจิ้มตรงสายสีดำ (0 V) หลอดไฟ LED จะติดสว่าง
![image](https://user-images.githubusercontent.com/80879589/112304892-a12b7c80-8cd0-11eb-9d68-fc921e99c864.png)
10. กดปุ่มสีดำจะทำให้หลอด LED ติดสว่าง เนื่องจากไมโครคอนโทรเลอร์เชื่อมกับพอร์ท 0 อยู๋
![image](https://user-images.githubusercontent.com/80879589/112305754-a89f5580-8cd1-11eb-80fc-f8b8521d2b17.png)
11. ต่อขาตัวเซนเซอร์รับแสงกับเส้นสีเเดง 5V เเละต่อขาตัวต้านทานกับเส้นสีดำ 0V
![image](https://user-images.githubusercontent.com/80879589/112306519-75a99180-8cd2-11eb-9d18-fccc573d0eab.png)

## การบันทึกผลการทดลอง
 กรณีที่ 1 นำสายสีขาวจิ้ม
 * จิ้มไปในช่องสีดำ  ไฟติด
 * จิ้มไปในช่องสีแดง ไฟไม่ติด
 
 กรณีที่ 2 กดปุ่มสีดำ
 * เมื่อยังไม่กด ไฟไม่ติด
 * เมื่อกด     ไฟติด
   
 กรณีที่ 3 นำมือมาบังแสงที่เซนเซอร์รับแสง
 * เมื่อนำมือไปบัง ไฟดับ
 * เมื่อมือไม่บัง   ไฟติด

## อภิปรายผลการทดลอง
จากการทดลอง พบว่า เมื่อรันโปรแกรมเข้าไปในไมโครคอนโทรเลอร์ จะพบว่าเมื่อนำสายสีขาวจิ้มไปตรงช่องสายสีดำไฟจะติดสว่าง 
แต่ถ้านำไปจิ้มตรงสายสีแดงไฟจะไม่ติด เนื่องจากกระแสไหลไม่เต็มระบบ เมื่อกดปุ่มสีดำที่ไมโครคอนโทรเลอร์ไฟจะติด เมื่อปล่อยไฟจะดับ
และนำตัวเซนเซอร์รับแสงต่อเข้าไป พบว่าเมื่อนำมือไปบังแสงไฟจะดับแต่เมื่อไม่บังแสงไฟจะติด

## คำถามหลังการทดลอง
  
  
 









































