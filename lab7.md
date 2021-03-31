# การทดลองที่ 3 เรื่อง การเขียนโปรแกรมลงบนไมโครคอนโทรลเลอร์เพื่อนำไปประยุกต์ใช้ในชีวิตประจำวัน

## วัตุประสงค์
1. เพื่อศึกษาการรันโปรแกรมในไมโครคอนโทรเลอร์ไปเชื่อมต่อกับอุปกรณ์อื่นๆ
2. เพื่อนำความรู้ที่ได้จากการทดลองที่ 1-6 มาประยุกต์ออกแบบเพิ่มเติมเพื่อประโยชน์แก่การนำไมโครคอนโทรเลอร์ไปประยุกต์ใช้ในชีวิตประจำวัน

## อุปกรณ์ที่ใช้
1. ไมโครคอนโทรเลอร์(ESP-01)
![Image](https://ae01.alicdn.com/kf/HTB1QMy2J9zqK1RjSZFpq6ykSXXac/ESP8266-ESP-01-ESP01-Serial-WIFI-3-3V-5V-Serial.jpg)
2. สายต่ออุปกรณ์ USB 
3. ซีเรียล
4. Adapter
5. หลอดไฟ LED
6. sensors DS18B20
![image](https://user-images.githubusercontent.com/80879589/113092556-68336080-9218-11eb-8d98-67c79a6db3a8.png)
7. คอมพิวเตอร์















































```c
#include <Arduino.h>
#include <OneWire.h>
#include <DallasTemperature.h>
#define ONE_WIRE_BUS 2
OneWire oneWire(ONE_WIRE_BUS);
DallasTemperature sensors(&oneWire);

float Celsius = 0;
float Fahrenheit = 0;

void setup() 
{
  sensors.begin();
  Serial.begin(9600);
}

void loop() 
{
  sensors.requestTemperatures();
  Celsius = sensors.getTempCByIndex(0);
  Fahrenheit = sensors.toFahrenheit(Celsius);
  
  Serial.print(Celsius);
  Serial.print(" C  ");
  Serial.print(Fahrenheit);
  Serial.println(" F");

  delay(2000);
  
  if (Celsius>=30){
                Serial.println("==== ON ====");
                digitalWrite(0, HIGH);
	} else (Celsius<30){
		Serial.println("==== OFF ====");
		digitalWrite(0, LOW);
	}
	
}
```

