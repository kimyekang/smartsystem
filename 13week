#include <DHT.h>
#include<DHT_U.h>
#include <Adafruit_NeoPixel.h>

#define Buzzer 6
#define LED 11
#define POWER 12
#define temp A2
#define IR A3
#define TOUCH A4
#define POT A5

int dataPin = 10;
int latchPin = 8;
int clockPin = 7;
int note[] = {3136, 2349, 3136, 2349, 3136, 2349};
int dotbright;
int c;
#define DHTPIN 4
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);
Adafruit_NeoPixel pixels = Adafruit_NeoPixel(1, LED, NEO_GRB + NEO_KHZ800);
int X = A0;
int Y = A1;
int Z = 3;
byte red[8] = {0x00, 0x7E, 0x48, 0x5C, 0x32, 0x00, 0x00, 0x00};
byte green[8] = {0x00, 0x3C, 0x42, 0x4A, 0x2C, 0x00, 0x00, 0x00};
byte blue[8] = {0x00, 0x7E, 0x52, 0x52, 0x2C, 0x00, 0x00, 0x00,};
byte pink[8] = {0x00, 0x7E, 0x48, 0x48, 0x30, 0x00, 0x00, 0x00};
byte smile[8] = {0x3C, 0x42, 0xA9, 0x85, 0x85, 0xA9, 0x42, 0x3C};
byte sad[8] = {0x3C, 0x42, 0xA5, 0x89, 0x89, 0xA5, 0x42, 0x3C};
byte one[8] = {0x00, 0x00, 0x10, 0x20, 0x7E, 0x00, 0x00, 0x00};
byte two[8] = {0x00, 0x00, 0x36, 0x4A, 0x52, 0x22, 0x00, 0x00};
byte three[8] = {0x00, 0x00, 0x42, 0x52, 0x52, 0x7E, 0x00, 0x00};
byte dot[8] = {0x00, 0x00, 0x00, 0x00, 0x01, 0x00, 0x00, 0x00};
byte space[8] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
const int sensorPin = 5;
int sensorValue = 0;
int VibSensor = 9;
int USensor = 2;
int USensorValue = 0;
int rowVal = 0;
int brightness = 100;
boolean started = false;
int posy = B00000001;
int posx = B00010000;
int dotY = 128;
int dotY2 = 128;
int dotY3 = 128;
int dotY4 = 128;
int dotX;
int dotX2;
int dotX3;
int dotX4;
int k;
int state = 0;
int touchsensor = 1;
int pot_output = 0;
int LED_COLOR = 0;
int J3 = 1;
unsigned long previousMillis = 0;
unsigned long currentMillis = 0;
boolean newDot = false;
int score = 0;
int previousScore = 0;
int speedUp = 200;
int V;
int count = 1;
byte letters[][8] = {

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
  {0x00,0x00,0x20,0x7E,0x00,0x00,0x00,0x00}, //  1 
  {0x00,0x5E,0x52,0x72,0x00,0x00,0x00,0x00}, //  2 
  {0x00,0x52,0x52,0x7E,0x00,0x00,0x00,0x00}, //  3 
  {0x00,0x60,0x10,0x7E,0x00,0x00,0x00,0x00}, //  4 
  {0x00,0x72,0x52,0x5C,0x00,0x00,0x00,0x00}, //  5
  {0x00,0x7E,0x52,0x5E,0x00,0x00,0x00,0x00}, //  6 
  {0x00,0x70,0x40,0x7E,0x00,0x00,0x00,0x00}, //  7 
  {0x00,0x7E,0x52,0x7E,0x00,0x00,0x00,0x00}, //  8 
  {0x00,0x70,0x50,0x7E,0x00,0x00,0x00,0x00}, // 9 
  {0x00,0x7E,0x42,0x7E,0x00,0x00,0x00,0x00}, //  0
  {0x60, 0x80, 0x8D, 0x90, 0x60, 0x00}, //  ?
  {0x00, 0x00, 0xFD, 0x00, 0x00, 0x00}, //  !
  {0x00, 0x00, 0x00, 0x00, 0x00, 0x00}  // SPACE
};
String letterPositions = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234567890?! ";
byte *textBytes;
int Length_Letters = 0;
int colVal[8] = {1, 2, 4, 8, 16, 32, 64, 128};
void setup() {
  dht.begin();
  Serial.begin(9600);
  Serial.println("Ready");
  pinMode(USensor, INPUT);
  pinMode(VibSensor, INPUT);
  pinMode(Buzzer, OUTPUT);
  pinMode(POWER, INPUT);
  pinMode(LED, OUTPUT);
  pinMode(TOUCH, INPUT);
  pinMode(dataPin, OUTPUT);
  pinMode(latchPin, OUTPUT);
  pinMode(clockPin, OUTPUT);
  DotMatrixWrite(~0, 0);
  pinMode(X, INPUT);
  pinMode(Y, INPUT);
  pinMode(Z, INPUT);
  pixels.begin();
  pixels.show();
  Serial.begin(9600);
  randomSeed(analogRead(2));
  dotX = randomMapping(random(1, 9));
  dotX2 = randomMapping2(random(1, 9));
  dotX3 = randomMapping3(random(1, 9));
  dotX4 = randomMapping4(random(1, 9));
  loadString(String(" "));
}
void loop() {
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
  V = digitalRead(VibSensor);
  if (V == LOW) {
    delay(1000);
    int elementCount = sizeof(note) / sizeof(int);
    for (int i = 0; i < elementCount; i++)
    {
      delay(200);
      tone(Buzzer, note[i], 100);
      delay(300);
    }
  }
  USensorValue = digitalRead(USensor);
  if (USensorValue == LOW) {
    delay(1000);
    int elementCount = sizeof(note) / sizeof(int);
    for (int i = 0; i < elementCount; i++)
    {
      delay(200);
      tone(Buzzer, note[i], 100);
      delay(300);
    }
  }
  sensorValue = digitalRead(sensorPin);
  if (sensorValue > 0.5) {
    delay(1000);
    int elementCount = sizeof(note) / sizeof(int);
    for (int i = 0; i < elementCount; i++)
    {
      delay(200);
      tone(Buzzer, note[i], 100);
      delay(300);
    }
  }
  
  if (digitalRead(POWER) == LOW || J3 == 0) {
   delay(200);
    state++;
  }

  if (touchsensor != digitalRead(TOUCH)) {
    LED_COLOR++;
    touchsensor = digitalRead(TOUCH);
  }
  pot_output = analogRead(POT);
  brightness = map(pot_output, 0, 1023, 0, 255);
  dotbright = map(pot_output, 0, 1023, 0, 27);
  c = 27 - dotbright;
  
  switch (k) {
    case 2 :
      if (LED_COLOR % 4 == 3) {
        
        if(c < 27) {
        Display2(pink);
        delay(c);
        pixels.setPixelColor(0, brightness, (brightness / 5) , (brightness / 5) * 3);
        pixels.show();
        Display2(space);
        }
        else if(c >= 27) {
          Display2(space);
          pixels.setPixelColor(0, 0, 0, 0);
      pixels.show();
        }
      }
      break;
    case 1 :
      pixels.setPixelColor(0, 0, 0, 0);
      pixels.show();
      Display2(space);
      break;
  }

  switch (k) {
    case 2 :
      if (LED_COLOR % 4 == 0) {
        if(c < 27) {
        pixels.setPixelColor(0, brightness, 0, 0);
        pixels.show();
        Display2(red);
        delay(c);
        Display2(space);
        }
        else if(c >= 27) {
          Display2(space);
          pixels.setPixelColor(0, 0, 0, 0);
      pixels.show();
        }
      }
      break;
    case 1 :
      pixels.setPixelColor(0, 0, 0, 0);
      pixels.show();
      Display2(space);
      break;
  }
  
  switch (k) {
     case 2 :
      if (LED_COLOR % 4 == 1) {
        if(c < 27) {
        pixels.setPixelColor(0, 0, brightness, 0);
        pixels.show();
        Display2(green);
        delay(c);
        Display2(space);
        }
        else if(c >= 27) {
          Display2(space);
          pixels.setPixelColor(0, 0, 0, 0);
          pixels.show();
        }
        
      }
      break;
    case 1 :
      pixels.setPixelColor(0, 0, 0, 0);
      pixels.show();
      Display2(space);
      break;
  }

  switch (k) {
    case 2 :
      if (LED_COLOR % 4 == 2) {
        if(c < 27) {
        pixels.setPixelColor(0, 0, 0, brightness);
        pixels.show();
        Display2(blue);
        delay(c);
        Display2(space);
        }
        else if(c >= 27) {
          Display2(space);
          pixels.setPixelColor(0, 0, 0, 0);
          pixels.show();
        }
      }
        break;
      
    case 1 :
      pixels.setPixelColor(0, 0, 0, 0);
      pixels.show();
      Display2(space);
      break;
  }


  if (state % 4 == 0 || count == 0) {
    k = 1;
  }

  if (state % 4 == 1 ) {
    k = 2;
    if(count == 0){
      k = 1;
    }
  }

  if (state % 4 == 2) {
    k = 3;
  }
  
  if (state % 4 == 3) {
    k = 4;
  }


  if (k == 3) {
    pixels.setPixelColor(0, 0, 0, 0);
    pixels.show();
    int t = dht.readTemperature();
    Serial.print(t);
    loadString(String(t));
    for (int repeat = 0; repeat < 100; repeat++) {
      for (int col = 0; col < 8; ++col) {
        rowVal = textBytes[col ];
        DotMatrixWrite(~rowVal, colVal[col]);
      }
    }
  }

    if (k == 4) {
    pixels.setPixelColor(0, 0, 0, 0);
    pixels.show();
    
    int h = dht.readHumidity();
    Serial.print(h);
    loadString(String(h));
    for (int repeat = 0; repeat < 100; repeat++) {
      for (int col = 0; col < 8; ++col) {
        rowVal = textBytes[col ];
        DotMatrixWrite(~rowVal, colVal[col]);
      }
    }
  }
  
  int J3 = digitalRead(Z);
  if (J3 == 0 && started == false && state % 4 == 1) {
    count = 0;
    startGame();
    blinkCharacter();
    started = true;
    loadString(String(" "));
  }

  if (started) {
    int x = map(analogRead(X), 0, 1023, -10, 10);
    int y = map(analogRead(Y), 0, 1023, -10, 10);

    if(x > 0 && posx != 128) posx = posx*2;
    if(x < 0 && posx != 1) posx = posx/2;
    if(y > 0 && posy != 128) posy = posy*2;
    if(y < 0 && posy != 1) posy = posy/2;
    
    currentMillis = millis();
    if((currentMillis - previousMillis) >= speedUp) {
      if(LED_COLOR % 4 == 0){
      dotY = dotY/2;
      }
      if(LED_COLOR % 4 == 1) 
      {dotY = dotY/2; dotY2 = dotY2/2;
      }
      if(LED_COLOR % 4 == 2) {
        dotY = dotY/2; dotY2 = dotY2/2; dotY3 = dotY3/2;
        }
      if(LED_COLOR % 4 == 3) {
        dotY = dotY/2; dotY2 = dotY2/2; dotY3 = dotY3/2; dotY4 = dotY4/2;
        }
      previousMillis = currentMillis;
      }
     if(dotY >= 1 && dotY2 >= 1 ) newDot = false;
     else newDot = true;
        Serial.println(score);

     if (newDot) {
        dotX2 = randomMapping2(random(1, 9));
        dotX = randomMapping(random(1, 9));
        dotX3 = randomMapping3(random(1, 9));
        dotX4 = randomMapping4(random(1, 9));
        
         if(LED_COLOR % 4 == 0){
          dotY = 128;
          }
         if(LED_COLOR % 4 == 1){
          dotY2 = 128; dotY = 128;
          }
         if(LED_COLOR % 4 == 2){
          dotY3 = 128; dotY2 = 128; dotY = 128;
          }
         if(LED_COLOR % 4 == 3){
          dotY4 = 128;dotY3 = 128;dotY2 = 128; dotY = 128;
         }
        score++;
      }
      if(dotX == dotX2){
        dotX = randomMapping(random(1, 9));
        }
        if(dotX == dotX3){
        dotX = randomMapping(random(1, 9));
        }
        if(dotX == dotX4){
        dotX = randomMapping(random(1, 9));
        }
        if(dotX2 == dotX3){
        dotX2 = randomMapping(random(1, 9));
        }if(dotX2 == dotX4){
        dotX2 = randomMapping(random(1, 9));
        }
        if(dotX3 == dotX4){
        dotX3 = randomMapping(random(1, 9));
        }
    
      if((score - previousScore) == 5) {
        previousScore = score;

        if(speedUp > 50) speedUp = speedUp - 25;
        }
        if(LED_COLOR % 4 == 0) {
        Draw_1(posx, posy, dotX, dotY);
        }
        if(LED_COLOR % 4 == 1) {
        Draw_2(posx, posy, dotX, dotY,dotX2,dotY2);
        }
        if(LED_COLOR % 4 == 2) {
        Draw_3(posx, posy, dotX, dotY,dotX2, dotY2, dotX3, dotY3);
        }
        if(LED_COLOR % 4 == 3) {
        Draw_4(posx, posy, dotX, dotY,dotY2, dotY3, dotY4, dotX2, dotX3, dotX4);
        }
        
        
       if ((posx == dotX && posy == dotY ) || (posx == dotX2 && posy == dotY2  ) || (posx == dotX3 && posy == dotY3) || (posx == dotX4 && posy == dotY4 )) {
        tone(Buzzer, 2349, 250);
        delay(200);
        tone(Buzzer, 2349, 250);
        delay(200);
        tone(Buzzer, 2093, 250);
        delay(50);
        Display(sad, 1000);
        
        loadString(String(score));
        for (int repeat = 0; repeat < 1000; repeat++) {
        for (int col = 0; col < 8; ++col) {
          rowVal = textBytes[col];
          DotMatrixWrite(~rowVal, colVal[col]);
        }
      }
        DotMatrixWrite(~0, 0);
        posx = B00010000;
        posy = B00000001;
         if(LED_COLOR % 4 == 0){dotY = 128;}
         if(LED_COLOR % 4 == 1){dotY2 = 128;dotY = 128;}
         if(LED_COLOR % 4 == 2){dotY3 = 128;dotY2 = 128;dotY = 128;}
         if(LED_COLOR % 4 == 3){dotY4 = 128;dotY3 = 128;dotY2 = 128;dotY = 128;}
        started = false;
        score = 0;
        count = 1;
    }
  }
}

void DotMatrixWrite(int rowVal, int colVal) {
    digitalWrite(latchPin,LOW);
    shiftOut(dataPin, clockPin, MSBFIRST, rowVal);
    shiftOut(dataPin, clockPin, MSBFIRST, colVal);
    digitalWrite(latchPin, HIGH);
    }

void Display2(byte data[]) {
  if(count == 1) {
  for (int i = 0; i < 8; i++) {
    rowVal = data[i];
    DotMatrixWrite(~rowVal, colVal[i]);
  }
  }
}

void Display(byte data[], int millisec) {

  long startTime = millis();
  long endTime = 0;
  while ((endTime - startTime) <= millisec) {
    for (int i = 0; i < 8; i++) {
      rowVal = data[i];
      DotMatrixWrite(~rowVal, colVal[i]);
    }
    endTime = millis();
  }
}
       void Draw_1 (int posx, int posy, int dotX, int dotY) {
        int xChar = onePos(posx);
        int xDot = onePos(dotX);
        byte screen[8] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

        if (xChar == xDot) screen[xChar] = posy + dotY;
        else {
          screen[xChar] = posy;
          screen[xDot] = dotY;
          }
          Display(screen, 100);
        }
         void Draw_2 (int posx, int posy, int dotX, int dotY, int dotX2, int dotY2) {
        int xChar = onePos(posx);
        int xDot = onePos(dotX);
        int xDot2 = onePos(dotX2);
        byte screen[8] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

        if (xChar == xDot) screen[xChar] = posy + dotY;
        else {
          screen[xChar] = posy;
          screen[xDot] = dotY;
          }
          if (xChar == xDot2) screen[xChar] = posy + dotY2;
         else {
          
          //screen[xChar] = posy;
          screen[xDot2] = dotY2;
          }
          Display(screen, 100);
        }
         void Draw_3 (int posx, int posy, int dotX, int dotY, int dotX2, int dotY2, int dotX3, int dotY3) {
        int xChar = onePos(posx);
        int xDot = onePos(dotX);
        int xDot2 = onePos(dotX2);
        int xDot3 = onePos(dotX3);
        byte screen[8] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

        if (xChar == xDot) screen[xChar] = posy + dotY;
        else {
          screen[xChar] = posy;
          screen[xDot] = dotY;
          }
          if (xChar == xDot2) screen[xChar] = posy + dotY2;
         else {
          
          //screen[xChar] = posy;
          screen[xDot2] = dotY2;
          }
          if (xChar == xDot3) screen[xChar] = posy + dotY3;
         else {      
          
          //screen[xChar] = posy;
          screen[xDot3] = dotY3;      
          }
          Display(screen, 100);
        }
         
        
      void Draw_4(int posx, int posy, int dotX, int dotY,int dotY2, int dotY3, int dotY4, int dotX2, int dotX3, int dotX4) {       
        int xChar = onePos(posx);
        int xDot = onePos(dotX);
        int xDot2 = onePos(dotX2);
        int xDot3 = onePos(dotX3);
        int xDot4 = onePos(dotX4);
        byte screen[8] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
       
        if (xChar == xDot) screen[xChar] = posy + dotY;
         else {
          
          screen[xChar] = posy;
          screen[xDot] = dotY;
          }
        
        if (xChar == xDot2) screen[xChar] = posy + dotY2;
         else {
          
          //screen[xChar] = posy;
          screen[xDot2] = dotY2;
          }
         
        if (xChar == xDot3) screen[xChar] = posy + dotY3;
         else {      
          
          //screen[xChar] = posy;
          screen[xDot3] = dotY3;      
          }
           
        if (xChar == xDot4) screen[xChar] = posy + dotY4;//여기 수정마지막에!!!!
        else {      
         
          //screen[xChar] = posy;
          screen[xDot4] = dotY4;
          }
          Display(screen, 100);
        }

int onePos(int x) {
   String a = String(x, BIN);
   int c = a.length() - 1;
   return c;
  }
void startGame() {
  Display(smile, 1000);
  tone(Buzzer, 3136, 250);
  Display(three, 1000);
  tone(Buzzer, 3136, 250);
  Display(two, 1000);
  tone(Buzzer, 3136, 250);
  Display(one, 1000);
  }

void blinkCharacter() {
  tone(Buzzer, 4186, 1200);
  for (int i = 0; i < 3; i++) {
    Display(dot, 200);
    Display(space, 200);
    }
  }
int randomMapping(int dotX) {
  
   switch (dotX) {
    case 1: dotX = 1; break;
    case 2: dotX = 2; break;
    case 3: dotX = 4; break;
    case 4: dotX = 8; break;
    case 5: dotX = 16; break;
    case 6: dotX = 32; break;
    case 7: dotX = 64; break;
    case 8: dotX = 128; break;
    }
    return dotX;
}
int randomMapping2(int dotX2){
  
   switch (dotX2) {
    case 1: dotX2 = 1; break;
    case 2: dotX2 = 2; break;
    case 3: dotX2 = 4; break;
    case 4: dotX2 = 8; break;
    case 5: dotX2 = 16; break;
    case 6: dotX2 = 32; break;
    case 7: dotX2 = 64; break;
    case 8: dotX2 = 128; break;
    }
    return dotX2;
}
int randomMapping3(int dotX3){
  switch (dotX3) {
    case 1: dotX3 = 1; break;
    case 2: dotX3 = 2; break;
    case 3: dotX3 = 4; break;
    case 4: dotX3 = 8; break;
    case 5: dotX3 = 16; break;
    case 6: dotX3 = 32; break;
    case 7: dotX3 = 64; break;
    case 8: dotX3 = 128; break;
    }
    return dotX3;
}
int randomMapping4(int dotX4){
  
  switch (dotX4) {
    case 1: dotX4 = 1; break;
    case 2: dotX4 = 2; break;
    case 3: dotX4 = 4; break;
    case 4: dotX4 = 8; break;
    case 5: dotX4 = 16; break;
    case 6: dotX4 = 32; break;
    case 7: dotX4 = 64; break;
    case 8: dotX4 = 128; break;
    }
    return dotX4;
  }


void lightLED(uint32_t c) {
  pixels.setPixelColor(0, c);
  pixels.show();
}

void loadString(String text) {
  Length_Letters = text.length(); 
  textBytes = (byte *)malloc(Length_Letters * 4 * sizeof(byte)); 
  int pos = 0; // position. chPos: character position.
  for (int i = 0; i < Length_Letters; ++i) {
    int chPos = letterPositions.indexOf(text[i]); 
    if (chPos == -1)
      continue;
  for (int j = 0; j < 4; ++j ) {
      textBytes[pos++] = letters[chPos][j];
    }
  }
  for (int k = 0; k < 8; ++k ) {
    textBytes[pos++] = 0;
  }
}
