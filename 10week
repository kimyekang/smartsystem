#include <Adafruit_NeoPixel.h>

#define LED 11
#define POWER  2
#define LIGHT A1
#define SOUND A2
#define IR A3
#define TOUCH A4
#define POT A5

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(1, LED, NEO_GRB + NEO_KHZ800);

int touch_tmp = 1;
int LED_COLOR = 0;
int pot_output = 0;
int brightness = 100;
const int dataPin = 10;
const int latchPin = 8;
const int clockPin = 7;
int k;
boolean state = LOW;

int RcolVal[8] = {
  B00000000,
  B00111110,
  B01100110,
  B01100110,
  B00111110,
  B00111110,
  B01110110,
  B01100110
};
int GcolVal[8] = {
  B00000000,
  B00111100,
  B01100110,
  B00000110,
  B00000110,
  B01110110,
  B01100110,
  B00111100
} ;
int BcolVal[8] = {
  B00000000,
  B00111110,
  B01100110,
  B01100110,
  B00111110,
  B01100110,
  B01100110,
  B00111110
} ;
int PcolVal[8] = {
  B00000000,
  B00111110,
  B01100110,
  B01100110,
  B01100110,
  B00111110,
  B00000110,
  B00000110
} ; 

int colValemp[8] = {
  B00000000,
  B00000000,
  B00000000,
  B00000000,
  B00000000,
  B00000000,
  B00000000,
  B00000000
  };
int rowVal[8] = {
  B01111111,
  B10111111,
  B11011111,
  B11101111,
  B11110111,
  B11111011,
  B11111101,
  B11111110
  };
void setup() {
  pixels.begin();
  pixels.show();
  pinMode(dataPin, OUTPUT);    
  pinMode(latchPin, OUTPUT); 
  
  pinMode(clockPin, OUTPUT); 
  pinMode(POWER, INPUT);
  pinMode(LED, OUTPUT);
  pinMode(TOUCH, INPUT);
  pinMode(LIGHT, INPUT);
  pinMode(SOUND, INPUT);
  pinMode(IR, INPUT);
  Serial.begin(9600);
}
 boolean debounce(boolean previous) {
  boolean current = digitalRead(POWER);
  if (previous != current) {
    current = digitalRead(POWER);
  }
  return current;
 }
void loop() {
int p = 0;
  
 
  if(digitalRead(POWER) == LOW){
    delay(200);
    state = !state;
    Serial.println(state);
  }
   if(state && analogRead(LIGHT) > 1000) {
    state = !state;
   }

  if (touch_tmp != digitalRead(TOUCH)) {
    LED_COLOR++;
    touch_tmp = digitalRead(TOUCH);
  }
//Serial.println(LED_ONOFF);
  pot_output = analogRead(POT);
  brightness = map(pot_output, 0, 1023, 0, 255);


switch(k) {
  
case 1 :
  if (LED_COLOR % 4 == 3) { 
    pixels.setPixelColor(0, brightness, (brightness / 5) , (brightness / 5) * 3);
    pixels.show();
    for(int i = 0; i < 8; i++){
    for(int j = 0; j < 8; j++){
      DotMatrixWrite(rowVal[j],PcolVal[j]);
      }  
      }
  }
  break;
  case 2 :
      pixels.setPixelColor(0, 0, 0, 0);
    pixels.show();
      for(int i = 0; i < 1; i++){
    for(int j = 0; j < 1; j++){

      DotMatrixWrite(rowVal[j],colValemp[j]);
      
    }
    } 
    break;
  }
  
  switch(k) {
    case 1 :
  if (LED_COLOR % 4 == 0) { 
    pixels.setPixelColor(0, brightness, 0, 0);
    pixels.show();
    for(int i = 0; i < 8; i++){
    for(int j = 0; j < 8; j++){
      DotMatrixWrite(rowVal[j],RcolVal[j]);
      }  
      }
  }
  break;
  case 2 :
      pixels.setPixelColor(0, 0, 0, 0);
    pixels.show();
      for(int i = 0; i < 1; i++){
    for(int j = 0; j < 1; j++){

      DotMatrixWrite(rowVal[j],colValemp[j]);
      
    }
    } 
    break;
  }
  
  switch(k){
    
  case 1 :
  if (LED_COLOR % 4 == 1) { 
    pixels.setPixelColor(0, 0, brightness, 0);
    pixels.show();
    for(int i = 0; i < 8; i++){
    for(int j = 0; j < 8; j++){
      DotMatrixWrite(rowVal[j],GcolVal[j]);
      }  
      }
  }
  break;
   case 2 :
      pixels.setPixelColor(0, 0, 0, 0);
    pixels.show();
      for(int i = 0; i < 1; i++){
    for(int j = 0; j < 1; j++){

      DotMatrixWrite(rowVal[j],colValemp[j]);
      
    }
    } 
    break;
  }
  
  switch(k){
    
  case 1 :
  if (LED_COLOR % 4 == 2) { 
    pixels.setPixelColor(0, 0, 0, brightness);
    pixels.show();
   for(int i = 0; i < 8; i++){
    for(int j = 0; j < 8; j++){
      DotMatrixWrite(rowVal[j],BcolVal[j]);
      }  
      }
      break;
  }
   case 2 :
      pixels.setPixelColor(0, 0, 0, 0);
    pixels.show();
      for(int i = 0; i < 1; i++){
    for(int j = 0; j < 1; j++){

      DotMatrixWrite(rowVal[j],colValemp[j]);
      
    }
    } 
    break;
  }

  if(state == 1) {
    
     k = 2;
  }
  if(state == 0) {
     k = 1;
  }
   if (digitalRead(IR) == 0) {
    for (int i = 0; i <= 2000; i += 100) {
      pixels.setPixelColor(0, 0, 0, 255);
      pixels.show();
      delay(50);
      pixels.setPixelColor(0, 0, 0, 0);
      pixels.show();
      delay(50);
    }
  }
   
  if (analogRead(SOUND) > 1000) {
    for (int i = 0; i <= 2000; i += 100) {
      Serial.println(SOUND);
      pixels.setPixelColor(0, 255, 0, 0);
      pixels.show();
      delay(50);
      pixels.setPixelColor(0, 0, 0, 0);
      pixels.show();
      delay(50);
    }
  
}
}
void DotMatrixWrite(int rowVal, int colVal){ 
  digitalWrite(latchPin, LOW); // Pull latch LOW to send data 
  shiftOut(dataPin, clockPin, MSBFIRST, rowVal); // Send the row data byte. Row data should be sent first.
  shiftOut(dataPin, clockPin, MSBFIRST, colVal); // Send the column data byte 
  digitalWrite(latchPin, HIGH); // Pull latch HIGH to finish sending data   
}
