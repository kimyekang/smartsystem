#include <Adafruit_NeoPixel.h>

#define LED 11
#define POWER 12
#define LIGHT A1
#define SOUND A2
#define IR A3
#define TOUCH A4
#define POT A5
boolean pastSW = HIGH;
boolean nowSW = HIGH;
boolean previousSW = HIGH;
boolean currentSW = HIGH;
int dataPin = 10;              
int latchPin = 8;            
int clockPin = 7;
const int interruptPin1 = 12;
const int SW = 12;

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(1, LED, NEO_GRB + NEO_KHZ800);

bool onoff = false;
int touch = 1;
int color = 0;
int pot_output = 0;
int brightness = 100;
boolean state1 = false;
int a;

byte letters[][6] = { 
  {0x7F, 0x88, 0x88, 0x88, 0x7F, 0x00}, //  A 
  {0xFF, 0x91, 0x91, 0x91, 0x6E, 0x00}, //  B 
  {0x7E, 0x81, 0x81, 0x81, 0x42, 0x00}, //  C 
  {0xFF, 0x81, 0x81, 0x42, 0x3C, 0x00}, //  D 
  {0xFF, 0x91, 0x91, 0x91, 0x81, 0x00}, //  E 
  {0xFF, 0x90, 0x90, 0x90, 0x80, 0x00}, //  F 
  {0x7E, 0x81, 0x89, 0x89, 0x4E, 0x00}, //  G 
  {0xFF, 0x10, 0x10, 0x10, 0xFF, 0x00}, //  H 
  {0x81, 0x81, 0xFF, 0x81, 0x81, 0x00}, //  I 
  {0x06, 0x01, 0x01, 0x01, 0xFE, 0x00}, //  J 
  {0xFF, 0x18, 0x24, 0x42, 0x81, 0x00}, //  K 
  {0xFF, 0x01, 0x01, 0x01, 0x01, 0x00}, //  L 
  {0xFF, 0x40, 0x30, 0x40, 0xFF, 0x00}, //  M 
  {0xFF, 0x40, 0x30, 0x08, 0xFF, 0x00}, //  N  
  {0x7E, 0x81, 0x81, 0x81, 0x7E, 0x00}, //  O 
  {0xFF, 0x88, 0x88, 0x88, 0x70, 0x00}, //  P 
  {0x7E, 0x81, 0x85, 0x82, 0x7D, 0x00}, //  Q 
  {0xFF, 0x88, 0x8C, 0x8A, 0x71, 0x00}, //  R 
  {0x61, 0x91, 0x91, 0x91, 0x8E, 0x00}, //  S 
  {0x80, 0x80, 0xFF, 0x80, 0x80, 0x00}, //  T 
  {0xFE, 0x01, 0x01, 0x01, 0xFE, 0x00}, //  U 
  {0xF0, 0x0C, 0x03, 0x0C, 0xF0, 0x00}, //  V 
  {0xFF, 0x02, 0x0C, 0x02, 0xFF, 0x00}, //  W 
  {0xC3, 0x24, 0x18, 0x24, 0xC3, 0x00}, //  X 
  {0xE0, 0x10, 0x0F, 0x10, 0xE0, 0x00}, //  Y 
  {0x83, 0x85, 0x99, 0xA1, 0xC1, 0x00}, //  Z 
  {0x06, 0x29, 0x29, 0x29, 0x1F, 0x00}, //  a 
  {0xFF, 0x09, 0x11, 0x11, 0x0E, 0x00}, //  b 
  {0x1E, 0x21, 0x21, 0x21, 0x12, 0x00}, //  c 
  {0x0E, 0x11, 0x11, 0x09, 0xFF, 0x00}, //  d 
  {0x0E, 0x15, 0x15, 0x15, 0x0C, 0x00}, //  e 
  {0x08, 0x7F, 0x88, 0x80, 0x40, 0x00}, //  f 
  {0x30, 0x49, 0x49, 0x49, 0x7E, 0x00}, //  g 
  {0xFF, 0x08, 0x10, 0x10, 0x0F, 0x00}, //  h 
  {0x00, 0x00, 0x5F, 0x00, 0x00, 0x00}, //  i 
  {0x02, 0x01, 0x21, 0xBE, 0x00, 0x00}, //  j 
  {0xFF, 0x04, 0x0A, 0x11, 0x00, 0x00}, //  k 
  {0x00, 0x81, 0xFF, 0x01, 0x00, 0x00}, //  l 
  {0x3F, 0x20, 0x18, 0x20, 0x1F, 0x00}, //  m 
  {0x3F, 0x10, 0x20, 0x20, 0x1F, 0x00}, //  n 
  {0x0E, 0x11, 0x11, 0x11, 0x0E, 0x00}, //  o 
  {0x3F, 0x24, 0x24, 0x24, 0x18, 0x00}, //  p 
  {0x10, 0x28, 0x28, 0x18, 0x3F, 0x00}, //  q 
  {0x1F, 0x08, 0x10, 0x10, 0x08, 0x00}, //  r 
  {0x09, 0x15, 0x15, 0x15, 0x02, 0x00}, //  s 
  {0x20, 0xFE, 0x21, 0x01, 0x02, 0x00}, //  t 
  {0x1E, 0x01, 0x01, 0x02, 0x1F, 0x00}, //  u 
  {0x1C, 0x02, 0x01, 0x02, 0x1C, 0x00}, //  v 
  {0x1E, 0x01, 0x0E, 0x01, 0x1E, 0x00}, //  w 
  {0x11, 0x0A, 0x04, 0x0A, 0x11, 0x00}, //  x 
  {0x00, 0x39, 0x05, 0x05, 0x3E, 0x00}, //  y 
  {0x11, 0x13, 0x15, 0x19, 0x11, 0x00}, //  z 
  {0x00, 0x41, 0xFF, 0x01, 0x00, 0x00}, //  1 
  {0x43, 0x85, 0x89, 0x91, 0x61, 0x00}, //  2 
  {0x42, 0x81, 0x91, 0x91, 0x6E, 0x00}, //  3 
  {0x18, 0x28, 0x48, 0xFF, 0x08, 0x00}, //  4 
  {0xF2, 0x91, 0x91, 0x91, 0x8E, 0x00}, //  5
  {0x1E, 0x29, 0x49, 0x89, 0x86, 0x00}, //  6 
  {0x80, 0x8F, 0x90, 0xA0, 0xC0, 0x00}, //  7 
  {0x6E, 0x91, 0x91, 0x91, 0x6E, 0x00}, //  8 
  {0x70, 0x89, 0x89, 0x8A, 0x7C, 0x00}, //  9 
  {0x7E, 0x89, 0x91, 0xA1, 0x7E, 0x00}, //  0 
  {0x60, 0x80, 0x8D, 0x90, 0x60, 0x00}, //  ? 
  {0x00, 0x00, 0xFD, 0x00, 0x00, 0x00}, //  ! 
  {0x00, 0x00, 0x00, 0x00, 0x00, 0x00}  // SPACE 
}; 

// character to letter mapping 
String letterPositions = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234567890?! "; 

// The database for the text to scroll 
byte *textBytes; 
int Length_Letters = 0; 
int colVal[8] = {1, 2, 4, 8, 16, 32, 64, 128}; /* same to {B00000001, B00000010,
B00000100, B00001000, B00010000, B00100000, B01000000, B10000000}; */


void setup() {
  pixels.begin();
  pixels.show();
  pinMode(interruptPin1, INPUT);
  pinMode(11, OUTPUT);
  pinMode(SW, INPUT);
  pinMode(LED, OUTPUT);
  pinMode(TOUCH, INPUT);
  pinMode(LIGHT, INPUT);
  pinMode(SOUND, INPUT);
  pinMode(IR, INPUT);
  Serial.begin(9600);
  pinMode(dataPin, OUTPUT);    // Configure Digital Pins 
  pinMode(latchPin, OUTPUT); 
  pinMode(clockPin, OUTPUT); 
  attachInterrupt(digitalPinToInterrupt(interruptPin1), exchange1, FALLING);
  loadString(String(" "));
}

void loop() {
  if (analogRead(SOUND) > 1000) {
    for (int i = 0; i <= 2000; i += 100) {
      pixels.setPixelColor(0, 255, 0, 0);
      pixels.show();
      delay(50);
      pixels.setPixelColor(0, 0, 0, 0);
      pixels.show();
      delay(50);
    }
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
  int p = -1; 
    int rowVal = 0; 
    
    // 반복을 변경하여 스크롤 텍스트의 속도 변경
     
      for (int col = 0; col < 8; ++col){ 
        rowVal = textBytes[p + col]; 
        DotMatrixWrite(~rowVal, colVal[col]); 
       }
  
  pot_output = analogRead(POT);
  brightness = map(pot_output, 0, 1023, 0, 255);
  Serial.println(brightness); //밝아지는 시간이 이상하다. 
  pixels.show();
  
  currentSW = debounce(previousSW);

  if(previousSW == HIGH && currentSW == LOW){
      
      previousSW = currentSW;
  }

/*if(digitalRead(SW) == LOW) {
  onoff = !onoff;
  }*/
  
if(touch != digitalRead(TOUCH)){
  color++;
  touch = digitalRead(TOUCH);
}
      if(color % 4 == 1){
        
        loadString(String("R"));
        pixels.setPixelColor(0, brightness, 0, 0);
       pixels.show();
        a=0;
      } 
      else if(color % 4 == 2) {
        
        loadString(String("G"));
        pixels.setPixelColor(0, 0, brightness, 0);
       pixels.show();
        a=1;
      }
      else if(color % 4 == 3) {
        
        loadString(String("B"));
        pixels.setPixelColor(0, 0, 0, brightness);
        pixels.show();
        a=2;
      } 
      else if(color % 4 == 0) {
        
        loadString(String("p"));
          pixels.setPixelColor(0, brightness, (brightness / 5), (brightness / 5) * 3);
          pixels.show();
        a=3;
      }


/*if(analogRead(LIGHT > 1000)){
  if(a == 0){
        loadString(String("R"));
        pixels.setPixelColor(0, 255, 0, 0);
         pixels.show();
      } 
      else if(a == 1) {
        loadString(String("G"));
        pixels.setPixelColor(0, 0, 255, 0);
         pixels.show();
      }
      else if(a == 2) {
        loadString(String("B"));
        pixels.setPixelColor(0, 0, 0, 255);
         pixels.show();
      } 
     else if(a == 3) {
        loadString(String("p"));
        pixels.setPixelColor(0, 255, 51, 153);
         pixels.show();
      } 
  else {
    loadString(String(" "));
    pixels.setPixelColor(0, 0, 0, 0);
         pixels.show();
    }
}
   /*if (analogRead(SOUND) > 1000) {
    for (int i = 0; i <= 2000; i += 100) {
      pixels.setPixelColor(0, 255, 0, 0);
      pixels.show();
      delay(50);
      pixels.setPixelColor(0, 0, 0, 0);
      pixels.show();
      delay(50);
    }
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
  }*/
}

void loadString(String text){ 
  // Build up byte array
  Length_Letters = text.length(); // length() 문자열의 길이를 반환합니다. 
  // Allocate memory for byte array 
  textBytes = (byte *)malloc(Length_Letters * 6 * sizeof(byte)); /* sizeof() 총 바이트 수를 반환합니다. So sizeof(byte) is equal to 1. */
  int pos = 0; // position. chPos:문자 위치.
  for (int i = 0; i < Length_Letters; ++i){ 
    int chPos = letterPositions.indexOf(text[i]); /* indexOf(val) 문자열 내의 val 인덱스를 반환합니다., or -1 if not found. */
    if (chPos == -1) 
      continue;     
    
    for (int j = 0; j < 6; ++j ){ 
      textBytes[pos++] = letters[chPos][j]; 
    }    
  }
  for (int k = 0; k < 8; ++k ){ 
      textBytes[pos++] = 0; 
  }
}
 
void DotMatrixWrite(int rowVal, int colVal){ 
  digitalWrite(latchPin, LOW); // Pull latch LOW to send data 
  shiftOut(dataPin, clockPin, MSBFIRST, rowVal); // Send the row data byte. Row data should be sent first.
  /* shiftOut(): Shifts out a byte of data one bit at a time. 
  Syntax of shiftOut(): shiftOut(dataPin, clockPin, bitOrder, value)
  clockPin: the pin to toggle once the dataPin has been set to the correct value(int).
  */
  shiftOut(dataPin, clockPin, MSBFIRST, colVal); // Send the column data byte 
  digitalWrite(latchPin, HIGH); // Pull latch HIGH to finish sending data   
}

 boolean debounce(boolean previous) {
  boolean current = digitalRead(SW);
  if (previous != current) {
    current = digitalRead(SW);
    
  }
  return current;
}
  void exchange1() {
  if(state1==false || LIGHT > 1000){ // 안될 시 else문 가서 LIGHT 추가 해보자
    
    if(a == 0){
        loadString(String("R"));
        pixels.setPixelColor(0, 255, 0, 0);
         pixels.show();
      } 
      else if(a == 1) {
        loadString(String("G"));
        pixels.setPixelColor(0, 0, 255, 0);
         pixels.show();
      }
      else if(a == 2) {
        loadString(String("B"));
        pixels.setPixelColor(0, 0, 0, 255);
         pixels.show();
      } 
     else if(a == 3) {
        loadString(String("p"));
        pixels.setPixelColor(0, 255, 51, 153);
         pixels.show();
      } 
 
   
    state1=true;
  }
  
  else {
        loadString(String(" "));
        pixels.setPixelColor(0, 0, 0, 0);
        pixels.show();
        
    state1=false;
  }
}
