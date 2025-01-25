#include <BluetoothSerial.h>

#include <OneWire.h>
#include <DallasTemperature.h>

BluetoothSerial SerialBT;

char action ;

int count = 0;

#include <SPI.h>
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#include "Talkie.h"
#include "Vocab_US_Large.h"

// heat sensor pinout
#define ONE_WIRE_BUS 26

//define sound speed in cm/uS
#define SOUND_SPEED 0.034


#define SCREEN_WIDTH 128 // OLED display width, in pixels
#define SCREEN_HEIGHT 64 // OLED display height, in pixels

// Declaration for an SSD1306 display conected to I2C (SDA, SCL pins)
// The pins for I2C are defined by the Wire-library. 
// On an arduino UNO:       A4(SDA), A5(SCL)
// On an arduino MEGA 2560: 20(SDA), 21(SCL)
// On an arduino LEONARDO:   2(SDA),  3(SCL), ...
#define OLED_RESET     -1 // Reset pin # (or -1 if sharing Arduino reset pin)
#define SCREEN_ADDRESS 0x3C ///< See datasheet for Address; 0x3D for 128x64, 0x3C for 128x32
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);



OneWire oneWire(ONE_WIRE_BUS);

DallasTemperature sensors(&oneWire);

// ultrasonic pinout
const int trigPin = 12;
const int echoPin = 14;




// relay pinout 
const int rel  = 18 ; 

long duration;
float distanceCm;

int distanceInch;

Talkie voice;

float Celsius = 0;
float Fahrenheit = 0;

void distance ()
{
   // Clears the trigPin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(5);
  // Sets the trigPin on HIGH state for 10 micro seconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(15);
  digitalWrite(trigPin, LOW);
  
  // Reads the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);
  
  // Calculate the distance
  distanceCm = duration * SOUND_SPEED/2;
  
  // Convert to inches
  //distanceInch = distanceCm * CM_TO_INCH;
  
  // Prints the distance in the Serial Monitor
  Serial.print("Distance (cm): ");
  Serial.println(distanceCm);
  /*Serial.print("Distance (inch): ");
  Serial.println(distanceInch);*/
  
  
}

void speaker(){
  //#if defined(TEENSYDUINO)
    pinMode(25, OUTPUT);
    digitalWrite(25, HIGH); //Enable Amplified PROP shield
//#endif
    voice.say(sp2_DANGER);
    voice.say(sp2_DANGER);
    voice.say(sp2_RED);
    voice.say(sp2_ALERT);
  
}


void stop ()
{
  pinMode(25,LOW);
}


void setup() {

   SerialBT.begin("GUNJAN");


  Serial.begin(9600); // Starts the serial communication
  pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPin, INPUT); // Sets the echoPin as an Input
  
  pinMode(rel,OUTPUT);


    // SSD1306_SWITCHCAPVCC = generate display voltage from 3.3V internally
  if(!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
    Serial.println(F("SSD1306 allocation failed"));
    for(;;); // Don't proceed, loop forever
  }

   // Show initial display buffer contents on the screen --
  // the library initializes this with an Adafruit splash screen.
  display.display();
  delay(2000); // Pause for 2 seconds

  // Clear the buffer
  display.clearDisplay();

  // Draw a single pixel in white
  display.drawPixel(10, 10, SSD1306_WHITE);

  // Show the display buffer on the screen. You MUST call display() after
  // drawing commands to make them visible on screen!
  display.display();
  delay(2000);




}

void loop() {

  //digitalWrite(rel,HIGH);

   if (SerialBT.available())
  {
     action = SerialBT.read();
  }

if (action == '1')
{
  count ++;
}

if (action == '0')
{ 
  count --;
}

  */
if ( distanceCm>5&& distanceCm <20)
{
  speaker();

}
/*else if  (distanceCm>27 && distanceCm <40)
{
  digitalWrite(led1,HIGH);
}*/

else
{
  //digitalWrite(led,LOW);
  //digitalWrite(led1,LOW);
stop();

}
  delay(1000);

if (count == 1 )
{
  distance();
}

if (count == 0 )
{
  stop();
}


 // digitalWrite(rel,HIGH);
  sensors.requestTemperatures();

  Celsius = sensors.getTempCByIndex(0);
  
  Serial.println(Celsius);
  Serial.print(" C  ");


  delay(10);

  display.clearDisplay();
  delay(1000);
  display.setTextSize(2);
  display.setTextColor(WHITE);
  display.setCursor(10, 10);
   display.println("Celsius");
  display.display();
   display.println(Celsius);
  display.display();

  delay (10);
 

 if (Celsius >= 50 && Celsius<=70)
 {
  digitalWrite(rel,HIGH);
 }
else 
{
  digitalWrite(rel,LOW);
}
  
  
}




