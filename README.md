#  arduino_color_sensor

##### 
This repository consists of  TCS3200 color sensor pin diagram and code.

The Pins are S0, S1, S2 and S3

The other pins are LED, OUT, and Vcc and GND.

TCS3200    Arduino 
S0..3 --->  4,5,6 7
Out ->   Pin 8

GND - GND
VCC and LED  -> is connected to 5V of Arduino


				
				#define S0 4
				#define S1 5
				#define S2 6
				#define S3 7
				#define sensorOut 8
				int frequency = 0;
				int frequency_orig=0;
				int red_frequency, blue_frequency, green_frequency ;
				
				void setup() {
				  pinMode(S0, OUTPUT);
				  pinMode(S1, OUTPUT);
				  pinMode(S2, OUTPUT);
				  pinMode(S3, OUTPUT);
				  pinMode(sensorOut, INPUT);
				  
				  // Setting frequency-scaling to 20%
				  digitalWrite(S0,HIGH);
				  digitalWrite(S1,LOW);
				  
				  Serial.begin(9600);
				}
				void loop() {
				  // Setting red filtered photodiodes to be read
				  digitalWrite(S2,LOW);
				  digitalWrite(S3,LOW);
				  // Reading the output frequency
				  frequency_orig = pulseIn(sensorOut, LOW);
				  //Remaping the value of the frequency to the RGB Model of 0 to 255
				  red_frequency = map(frequency_orig, 0, 1100 , 0, 255);  // has to be calibrated.
				  // Printing the value on the serial mnitor
				  Serial.print("R= ");//printing name
				  Serial.print(red_frequency );//printing RED color frequency
				  //Serial.print ("    ");
				  //Serial.print (frequency_orig );
				  if ( red_frequency <= 27 ) { Serial.print (" **RED** "); }
				  //Serial.print("  ");
				  
				  delay (300);
				  
				  // Setting Green filtered photodiodes to be read
				  digitalWrite(S2,HIGH);
				  digitalWrite(S3,HIGH);
				  // Reading the output frequency
				  frequency_orig = pulseIn(sensorOut, LOW);
				  //Remaping the value of the frequency to the RGB Model of 0 to 255
				  green_frequency = map(frequency_orig,0, 1100, 0, 255 );
				  // Printing the value on the serial monitor
				  Serial.print(" G= ");//printing name
				  Serial.print (green_frequency );
				  if ( green_frequency < 25) { Serial.print (" **GREEN** "); }
				  
				  delay(300);
				  
				  // Setting Blue filtered photodiodes to be read
				  digitalWrite(S2,LOW);
				  digitalWrite(S3,HIGH);
				  // Reading the output frequency
				  frequency_orig = pulseIn(sensorOut, LOW);
				  //Remaping the value of the frequency to the RGB Model of 0 to 255
				  blue_frequency = map(frequency_orig,0, 1100, 0, 255 );
				  // Printing the value on the serial monitor
				  Serial.print("  B= ");//printing name
				  Serial.print(blue_frequency);//printing RED color frequency
				  if ( blue_frequency < 25 ) { Serial.print (" **BLUE** "); }
				  delay (300);
				  
				  if ( red_frequency <15  &&  blue_frequency < 25 && green_frequency < 25) { Serial.print (" **WHITE** "); }
				  
				  Serial.println();
				    
				
				}
