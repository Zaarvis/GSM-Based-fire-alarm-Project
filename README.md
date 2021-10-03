# GSM-Based-fire-alarm-Project
GSM Based fire alarm Project Using Arduino   Gsm Based fire alarm project with Arduino is a very useful project and this project is in trending nowadays. It could be used in a major project in colleges and universities. So who is making their mind to make this awesome project by themselves they are in the right place.  We are posting a briefly explained project here with the working code and the diagram. and we will also help all the students to make this project in the comment section. we have more projects on gsm like gsm based home automation using Arduino this project is also in Trending so you can make this project also a major project. We are going to explain all the steps and instructions below if you want to learn the project you need to read the full article carefully and you need to know only some basics of electronic and embedded systems to make this project.This project is to protect the Forest especially. or it may be used in our home also. this is a very cool project though. GSM(global service for mobile) is used in mobile phones to communicate with the long-distance by wirelessly.  So, we are using this technology to protect the forest. because this system is not used any wire to communicate with another system. There we use the GSM SIM900N module with a sim card to notify the authorized person. when any mishappening occurs in the area where the system has been installed the message or call hangs up on the authorized person to make notify about the fire. GSM-based fire alarm project Uses the sim recharge also for the message and the call.  This is normally the alarm system for a fire near the forest and where you want to install it. as you can see in the above image there is a fire sensor interface with the gsm module and the Arduino and there is a sim inside the module.Component Required gsm based fire alarm project;- Arduino Uno GSM SIM900 module IR flame sensor LED Arduino Cable 16X2 LCD display I2C Module for LCD Jumper wire Breadboard 220-ohm resistor 12 Volt  2 amp adaptor. The above-given diagram is tested and verified you can use this diagram in your project. and if you have any doubt we are explaining the diagram below.  Connect Arduino Tx to the GSM Rx Connect Arduino Rx to the GSM Tx  (Note:- plug out the Rx wire of the Arduino during the upload program) Connect Arduino A4 to the I2C SCL Connect Arduino A5 to the I2C SDA Connect Arduino 4 to the Flame sensor DO Connect Arduino 5 to the LED +ve pin Connect Arduino  6 to the Buzzer +ve pin Common all device Ground to each other. GSM module works with the Arduino with the UART protocol which is also known as the serial data protocol. in this protocol the shift register is used to make the parallel data to the serial data. you can read all the AT commands in our previous post which is a GSM-based circuit breaker.  you must know the AT command to operate the gsm module. there are a lot of AT commands but we are using only some AT commands.
 // Techatronic.com  
 #include <Wire.h>           
 #include <LiquidCrystal_I2C.h>    
 LiquidCrystal_I2C lcd(0x27,16,2);   
  int val = 0 ;  
  int temp=0,i=0;  
  char str[15];  
 void setup()  
 {  
    Serial.begin(9600);  
    lcd.init();      
    lcd.backlight();  
    pinMode(4,INPUT);  // Flame Sensor  
    pinMode(5,OUTPUT); // Led  
    pinMode(6,OUTPUT); // Buzzer  
    lcd.setCursor(0,0);  
    lcd.print(" GSM Base Fire     ");  
    lcd.setCursor(0,1);  
    lcd.print("Security System ");  
    delay(2000);  
    lcd.clear();  
    Serial.println("AT+CNMI=2,2,0,0,0");  
    delay(500);  
    Serial.println("AT+CMGF=1");  
    delay(1000);  
 }  
 void loop()  
 {  
  if(temp==1)  
  {  
   check();  
   temp=0;  
   i=0;  
   delay(1000);  
  }  
   val = digitalRead(4); // pir sensor output pin connected  
   Serial.println(val); // see the value in serial mpnitor in Arduino IDE  
   delay(100);  
  if(val == 0 )  
   {  
   Serial.print("\r");  
   delay(1000);           
   Serial.print("AT+CMGF=1\r");  
   digitalWrite( 5,HIGH); // led   
   digitalWrite( 6,HIGH); // Buzzer  
   lcd.setCursor(0,0);  
   lcd.print(" Fire Detected     ");  
   lcd.setCursor(0,1);  
   lcd.print("   Be Safe    ");    
    delay(1000);  
   /*Replace XXXXXXXXXX to 10 digit mobile number & ZZ to 2 digit country code*/  
   Serial.print("AT+CMGS=\"+917000000000\"\r");    
   delay(1000);  
   //The text of the message to be sent.  
   Serial.print("Fire Alert");  
   delay(1000);  
   Serial.write(0x1A);  
 }  
 else  
  {  
     digitalWrite( 5,LOW); // led  
     digitalWrite( 6,LOW); // Buzzer  
     lcd.setCursor(0,0);  
     lcd.print("  FIRE NOT    ");  
     lcd.setCursor(0,1);  
     lcd.print("  DETECTED    ");  
  }  
  }  
  void serialEvent()   
  {  
  }  
  void check()  
  {  
   }  
