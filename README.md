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
# output of task 1
![Image](https://github.com/user-attachments/assets/b5a0acfa-616d-4482-bb76-e0d7b0c629fa)

![Image](https://github.com/user-attachments/assets/717498e1-7771-4c6c-8f72-4309d7cd0398)
