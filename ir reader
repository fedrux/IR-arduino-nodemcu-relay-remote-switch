#ifndef UNIT_TEST
#include <Arduino.h>
#endif
#include <IRremoteESP8266.h>
#include <IRrecv.h>
#include <IRutils.h>
#include <ESP8266WiFi.h>

const int RECV_PIN = D1;
const int relay_pin = D0;
const int led_pin = 2;

IRrecv irrecv(RECV_PIN);

decode_results results;

void setup()
{
  Serial.begin(9600);
  irrecv.enableIRIn(); // Start the receiver

  pinMode(relay_pin, OUTPUT);
  pinMode(led_pin, OUTPUT);
  
  digitalWrite(relay_pin, HIGH);
  digitalWrite(led_pin, HIGH);
  
  WiFi.mode(WIFI_OFF);
}

void loop() {
  if (irrecv.decode(&results)) {
     digitalWrite(led_pin, LOW);
    if (results.decode_type == NEC) {
      Serial.print("NEC: ");
    } else if (results.decode_type == SONY) {
      Serial.print("SONY: ");
    } else if (results.decode_type == RC5) {
      Serial.print("RC5: ");
    } else if (results.decode_type == RC6) {
      Serial.print("RC6: ");
    } else if (results.decode_type == UNKNOWN) {
      Serial.print("UNKNOWN: ");
    }
    serialPrintUint64(results.value, HEX);
    if (results.value == 21225) {
      digitalWrite(relay_pin, HIGH);
    } else if (results.value == 13033)    {
      digitalWrite(relay_pin, LOW);
    }
    irrecv.resume(); // Receive the next value
  }
  digitalWrite(led_pin, HIGH);
}
