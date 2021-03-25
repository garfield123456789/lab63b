# การทดลองที่ 6 เรื่อง การเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP)

## วัตุประสงค์
1. เพื่อศึกษาการเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP)

## อุปกรณ์ที่ใช้
1. ไมโครคอนโทรเลอร์(ESP-01)
![Image](https://ae01.alicdn.com/kf/HTB1QMy2J9zqK1RjSZFpq6ykSXXac/ESP8266-ESP-01-ESP01-Serial-WIFI-3-3V-5V-Serial.jpg)
2. สายต่ออุปกรณ์ USB 
3. ซีเรียล
4. คอมพิวเตอร์

## ศึกษาข้อมูลเบื้องต้น
### run example 6
 https://youtu.be/T26DVHePlTs
 
## วิธีการทำการทดลอง
1. ต่อสาย USB เข้ากับซีเรียล 
2. เสียบไมโครคอนโทรเลอร์(ESP-01)เข้ากับซีเรียล
3. เปิด command prompt เเล้วพิมพ์คำสั่ง **cd lab63b** เพื่อเข้าโปรแกรมตัวอย่าง
4. เลือกโปรแกรมตัวอย่างโดยใช้คำสั่ง **cd 06_Wifi-AP-Web-Server**
5. พิมพ์คำสั่ง **vi src/main.cpp** เเล้วกด Enter จะพบข้อมูลต่อไปนี้
```c
#include <ESP8266WiFi.h>
#include <ESP8266WebServer.h>

const char* ssid = "TUENG-ESP-WIFI";
const char* password = "choompol";

IPAddress local_ip(192, 168, 1, 1);
IPAddress gateway(192, 168, 1, 1);
IPAddress subnet(255, 255, 255, 0);

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
	Serial.begin(115200);

	WiFi.softAP(ssid, password);
	WiFi.softAPConfig(local_ip, geteway, subnet);
	delay(100);

	server.onNotFound([]() {
		server.send(404, "text/plain", "Path Not Found");
	});

	server.on("/", []() {
		cnt++;
		String msg = "Hello cnt: ";
		msg += cnt;
		server.send(200, "text/plain",msg);
	});

	server.begin();
	Serial.println("HTTP server started");
}

void loop(void){
	server.handleClient();
```

6. อัพโหลดโปรแกรมลงในไมโครคอนโทรนเลอร์ โดยพิมพ์คำสั่ง **pio run -t upload** แล้วกด Enter ในขณะที่รับโปรแกรมใหม่เข้าไปให้กดปุ่มสีดำค้างไว้ แล้วกดปุ่มแดง 1 ครั้ง เพื่อเป็นการ reset คำสั่งเก่า
![image](https://user-images.githubusercontent.com/80879589/112310561-4f3a2500-8cd7-11eb-9e45-0c608be9a583.png)

7. เมื่อทำการลงโปรแกรมเสร็จแล้ว พิมพ์คำสั่ง **pio device monitor** แล้วกด Enter เพื่อดูผลลัพธ์ที่ได้บนหน้าจอคอมพิวเตอร์
![image](https://user-images.githubusercontent.com/80879589/112310693-72fd6b00-8cd7-11eb-9b8a-bcf84e655227.png)

## การบันทึกผลการทดลอง
จากการทดลอง เมื่อรันโปรแกรมเข้าไปในไมโครคอนโทรเลอร์พบว่าสามารถสร้างไวไฟใหม่ขึ้นมาได้ โดยสามารถตั้งชื่อที่เราต้องการได้ และสามารถสร้างรหัสที่เราต้องการได้ โดยสามารถเช็คไวไฟได้จากการเชื่อมต่อไวไฟจากโทรศัพท์

## อภิปรายผลการทดลอง
จากการทดลอง พบว่าเมื่อรันโปรแกรมเข้าไปในไมโครคอนโทรเลอร์ สามารถสร้างไวไฟขึ้นมาได้และพบว่าสามารถใช้งานได้จริง

## คำถามหลังการทดลอง
* **ถาม** ถ้าเราเปลี่ยน password หลังจากที่เราเชื่อมต่อ WiFi เเล้วเราต้องเชื่อมต่อ WiFi ใหม่หรือไม่
* **ตอบ** ต้องเชื่อมต่อใหม่เพราะฐานข้อมูลที่เราใช้อันใหม่ไม่รองรับฐานข้อมูลเก่า

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
