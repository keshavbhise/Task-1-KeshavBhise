# Task-1-KeshavBhise
# Repository For Smart Environment Monitor-Code
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHTesp.h>

#define DHTPIN 15

DHTesp dht;

LiquidCrystal_I2C lcd(0x27,16,2);

void setup() {

  Serial.begin(115200);

  dht.setup(DHTPIN,DHTesp::DHT22);

  lcd.init();

  lcd.backlight();

  lcd.clear();

}

void loop() {

  TempAndHumidity data = dht.getTempAndHumidity();

  float temp = data.temperature;

  float hum = data.humidity;

  Serial.print("Temperature: ");

  Serial.print(temp);

  Serial.print(" °C   ");

  Serial.print("Humidity: ");

  Serial.print(hum);

  Serial.println(" %");

  lcd.clear();

  lcd.setCursor(0,0);

  lcd.print("Temp:");

  lcd.print(temp);

  lcd.print(" C");

  lcd.setCursor(0,1);

  lcd.print("Hum:");

  lcd.print(hum);

  lcd.print("%");

  delay(2000);

}
