# การทดลองที่ 5 เรื่อง การเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์

## วัตุประสงค์
1. เพื่อศึกษาวิธีการเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์

## อุปกรณ์ที่ใช้
1. ไมโครคอนโทรเลอร์(ESP-01)
![Image](https://ae01.alicdn.com/kf/HTB1QMy2J9zqK1RjSZFpq6ykSXXac/ESP8266-ESP-01-ESP01-Serial-WIFI-3-3V-5V-Serial.jpg)
2. สายต่ออุปกรณ์ USB 
3. ซีเรียล
4. คอมพิวเตอร์

## ศึกษาข้อมูลเบื้องต้น
### run example 5
 https://youtu.be/VX-QNQcO-b4
 
## วิธีการทำการทดลอง
1. ต่อสาย USB เข้ากับซีเรียล 
2. เสียบไมโครคอนโทรเลอร์(ESP-01)เข้ากับซีเรียล
3. เปิด command prompt เเล้วพิมพ์คำสั่ง **cd lab63b** เพื่อเข้าโปรแกรมตัวอย่าง
4. เลือกโปรแกรมตัวอย่างโดยใช้คำสั่ง **cd 05_Wifi-Web-Server**
5. พิมพ์คำสั่ง **vi src/main.cpp** เเล้วกด Enter จะพบข้อมูลต่อไปนี้
```c
#include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "HI_BMFWIFI_2.4G";   #พิมพ์ชื่อไวไฟและรหัสผ่าน
const char* password = "0819110933";

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
	Serial.begin(115200);

	WiFi.mode(WIFI_STA);
	WiFi.begin(ssid, password);
	while (WiFi.status() != WL_CONNECTED) {
		delay(500);
		Serial.print(".");
	}
	Serial.print("\n\nIP address: ");
	Serial.println(WiFi.localIP());

	server.onNotFound([]() {
		server.send(404, "text/plain", "Path Not Found");
	});

	server.on("/", []() {
		cnt++;
		String msg = "Hello cnt: ";
		msg += cnt;
		server.send(200, "text/plain", msg);
	});

	server.begin();
	Serial.println("HTTP server started");
}

void loop(void){
  server.handleClient();
}
```
6. อัพโหลดโปรแกรมลงในไมโครคอนโทรนเลอร์ โดยพิมพ์คำสั่ง **pio run -t upload** แล้วกด Enter ในขณะที่รับโปรแกรมใหม่เข้าไปให้กดปุ่มสีดำค้างไว้ แล้วกดปุ่มแดง 1 ครั้ง เพื่อเป็นการ reset คำสั่งเก่า
7. เมื่อทำการลงโปรแกรมเสร็จแล้ว พิมพ์คำสั่ง **pio device monitor** แล้วกด Enter เพื่อดูผลลัพธ์ที่ได้บนหน้าจอคอมพิวเตอร์ โดยจะขึ้น ip address
8. ให้ copy ip address ไปที่บราวเซอร์ในการทดสอบ

## การบันทึกผลการทดลอง
**คลิปมีปัญหา**

## อภิปรายผลการทดลอง
**คลิปมีปัญหา**

## คำถามหลังการทดลอง




































