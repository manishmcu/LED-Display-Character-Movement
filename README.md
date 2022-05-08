# LED-Display-Interface
To print every character of a string one by one as, rightward to leftward movement.

In this project we are interfacing 16x2 display with Arduino UNO. Here Arduino UNO is the controlling unit and 16x2 display unit. After completion of this process, we can pass any string through Arduino IDE to controller-board and it will be shown to its display accordingly. The circuit diagram and coding part is given below.

<p align="center">
  <img 
    height="300"
    src="Images/LED Interface.png"
  >
</p>

### Coding
{{
#include <LiquidCrystal.h>

// Connections:
// rs (LCD pin 4) to Arduino pin 12
// rw (LCD pin 5) to Arduino pin 11
// enable (LCD pin 6) to Arduino pin 10
// LCD pin 15 to Arduino pin 13
// LCD pins d4, d5, d6, d7 to Arduino pins 5, 4, 3, 2
LiquidCrystal lcd(12, 11, 10, 5, 4, 3, 2);
char Manish[]= "Mr Manish";
int len = strlen(Manish);
int i=0;
int j=1;

byte smiley[8] = {
  B00000,
  B10001,
  B00000,
  B00000,
  B10001,
  B01110,
  B00000,
};
int pos=15;
int backLight = 13;    // pin 13 will control the backlight

void setup()
{
  pinMode(backLight, OUTPUT);
  digitalWrite(backLight, HIGH); // turn backlight on. Replace 'HIGH' with 'LOW' to turn it off.
  lcd.begin(16,2);              // columns, rows.  use 16,2 for a 16x2 LCD, etc.
  lcd.clear();                  // start with a blank screen
  
  lcd.setCursor(0,0);           // set cursor to column 0, row 0 (the first row)
  //lcd.print("Mr Manish");    // change text to whatever you like. keep it clean!
  //lcd.setCursor(0,1);           // set cursor to column 0, row 1
  //lcd.print("Robotics Lab");
  
  //lcd.createChar(0, smiley);
  lcd.setCursor(15, 1);  
  lcd.write(byte(0));
  
  Serial.begin(9600);
  
}
void charMove()
{
  lcd.clear();
  
  for (int i=0;i<len;i++) 
  {
    lcd.setCursor(pos,0);
    lcd.print(Manish[i]);
    for(int pos=15; pos>=j; pos--){
      lcd.setCursor(pos-1,0);
      lcd.print(Manish[i]);
      lcd.setCursor(pos,0);
      lcd.print(" ");
      delay(200);

    }
    j+=1;
  }}

void loop()
{
  // Turn on the display:
  lcd.display();
  charMove();
  j=1;
  delay(1000);

  // Turn on the display:
  //lcd.offDisplay();
  
  int valor_sensor = analogRead(A0);
  Serial.println(valor_sensor);
  delay(1);      
}

}}
