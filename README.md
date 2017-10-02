[code]
//roep de library
#include <Servo.h>

Servo deurtje; // maakt servo object om de servo te besturen.
int deurPos; // variabele voor de positie in graden van de servo aka het deurtje.
int deurDefault = 0; // variabele voor de default stand van deurtje 0 graden = dicht.
int servoPin = 11;   // de pin waar de servo op staat op de Arduino
String klantBetaald = "Betaling geslaagd, de deur zal spoedig voor u open gaan."; //bericht voor klant wanneer betaling is geslaagd.
int arduinoBram = 2; //Pin waar de Servo signaal voor de betaling van krijgt


void setup() {
 // put your setup code here, to run once:
 deurtje.attach(servoPin); // Verbind de servo met pin 11 aan het servo object deurtje
 Serial.begin(9600);     //schrijf naar monitor
 pinMode(arduinoBram, INPUT);
 deurtje.write(deurDefault); // default dicht.
}
void loop(){
  if(digitalRead(arduinoBram)){ // Leest of stroom op de pin 2 staat van de Arduino van Bram.
    Serial.println(deurPos);
     if(deurPos == 90){
      Serial.println("open");
      openDeur();
      }
    }
    else{
     if(deurPos <= 0){
      Serial.println("close");
      sluitDeur();
      }
    }
}

void openDeur(){ 
   Serial.println(klantBetaald);                              //bericht voor klant wanneer de betaling is geslaagd.
   for (deurPos = 90; deurPos > 0; deurPos--){
    Serial.println(deurPos);
    deurtje.write(deurPos);  //gaat open 
    delay(30);               //over 30 ms
   }
}

void sluitDeur(){
   for (deurPos = 0; deurPos < 90; deurPos++) {    // Servo gaat van 0 naar 90 graden. ->deurtje dicht
     Serial.println(deurPos);
     deurtje.write(deurPos);                                    //deur koppelt met positie waardoor deur veranderd van positie.
     delay(30);                                                 // daar doet hij 30 ms over
  }  //deurtje sluit en blijft dicht.
}



[/code]
