# PUSH-BUTTON-COUNTER

**company** = CODTECH IT SOLUTIONS

**NAME** = SAYALI SANTOSH NIRDHAR 

**INTERN ID** = CT08JED

**DOMAIN** = Embedded Systems

**BATCH DURATION** = January 20th, 2025 to February 20th, 2025 

**MENTOR NAME** = Neela Santhosh 

#include <Wire.h> 
#include <LiquidCrystal_I2C.h> 
LiquidCrystal_I2C lcd(0x27, 16, 2);

const int buttonPin = 2;  
int buttonState = 0;    
int lastButtonState = LOW;
int count = 0;          
unsigned long lastDebounceTime = 0;
unsigned long debounceDelay = 50; 

void setup() {
    pinMode(buttonPin, INPUT_PULLUP); 
    lcd.begin();
    lcd.backlight();
    lcd.setCursor(0, 0);
    lcd.print("Count: 0");
    Serial.begin(9600);
}

void loop() {
    int reading = digitalRead(buttonPin);
    if (reading != lastButtonState) {
        lastDebounceTime = millis();
    }
    if ((millis() - lastDebounceTime) > debounceDelay) {
        if (reading == LOW && lastButtonState == HIGH) { 
            count++;
            lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print("Count: ");
            lcd.print(count);
            Serial.println("Button Pressed! Count: " + String(count));
        }
    }
    lastButtonState = reading; 
}
