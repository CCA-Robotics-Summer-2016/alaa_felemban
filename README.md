# alaa_felemban
/*
   I am Alaa felemban this is a program for my robot that uses both the light sensors and the distance measuring sensor:
  1.Measure distance
  2.If the distance measurement is invalid, do nothing
  3.If the distance is more than 50 cm, check the light sensors
  A.If there is more light to the left, go left for a short while
  B.If there is more light to the right, go right for a short while
  4.If the distance is less than 50 cm, go backwards (reverse) for a short while


*/


// Control pins for the right half of the H-bridge
const int enable2 = 9; // PWM pin for speed control
const int in3 = 8;
const int in4 = 7;

//other half
const int enable1 = 6; // PWM pin for speed control
const int in1 = 4;
const int in2 = 2;

// ultrasonic distance measuring sensor
const int trigPin = 12;
const int echoPin = 11;

// light sensor
const int leftLDR = A0;
const int rightLDR = A2;




void setup() {

  Serial.begin (9600);

  Serial.println( "hello from Alaas program version 0.1");
  Serial.print('\n');

  // pins for the ultrasonic distance measuring sensor
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  // motors
  pinMode( enable1, OUTPUT);
  pinMode( in1, OUTPUT);
  pinMode( in2, OUTPUT);

  pinMode( enable2, OUTPUT);
  pinMode( in3, OUTPUT);
  pinMode( in4, OUTPUT);

  // Set the speed to 100, which is pretty slow
  analogWrite (enable1, 100);
  analogWrite (enable2, 100);

  // light sensors
  pinMode( enable1, OUTPUT);
  pinMode( in1, OUTPUT);
  pinMode( in2, OUTPUT);

  pinMode( enable2, OUTPUT);
  pinMode( in3, OUTPUT);
  pinMode( in4, OUTPUT);


}

void loop() {
  Serial.println("Hello from loop()");
  long distance;
  Serial.println("distance()");
  distance = measureDistance();

  if (distance > 50 ) {
    Serial.println("checkLight()");
    // check the light sensors
    checkLight();

    //If there is more light to the left, go left for a short while

    if (analogRead (leftLDR) > analogRead (rightLDR) ) {
      Serial.println("turnLeft()");
      // turn left for a certain amount of time reverse
      turnLeft; delay ( 1000);

      //If there is more light to the right, go right for a short while

    } else {
      Serial.println(" turnRight()");
      // turn right for a certain amount of time
      turnRight; delay (1000);
    }

  }       else if (distance < 50 ) {
    // go backward
    Serial.println("goBackward ()");
    goBackward (2000);
  }

} // end of loop

// go backward for a certain amount of time
void goBackward(int timeToMove) {
  Serial.println("Hello from goBackward");

  // left motor
  digitalWrite (in1, LOW);
  digitalWrite (in2, HIGH);
  // Right motor
  digitalWrite (in3, HIGH);
  digitalWrite (in4, LOW);

  delay (timeToMove);
}

// go forward for a certain amount of time
void goForward(int timeToMove) {
  Serial.println("Hello from goForward");

  // left motor
  digitalWrite (in1, HIGH);
  digitalWrite (in2, LOW);
  // Right motor
  digitalWrite (in3, LOW);
  digitalWrite (in4, HIGH);

  delay (timeToMove);
}

// turn left for a certain amount of time
void turnLeft (int timeToMove) {

  Serial.println("Hello from turnLeft");

  // left motor
  digitalWrite (in1, LOW);
  digitalWrite (in2, HIGH);
  // Right motor
  digitalWrite (in3, LOW);
  digitalWrite (in4, HIGH);

  delay (timeToMove);
}

// turn right for a certain amount of time
void turnRight (int timeToMove) {

  Serial.println("Hello from turnRight");


  // left motor
  digitalWrite (in1, HIGH);
  digitalWrite (in2, LOW);
  //Right motor
  digitalWrite (in3, HIGH);
  digitalWrite (in4, LOW);

  delay (timeToMove);
}

// Take a measurement using the ultrasonic discance
// measuring sensor and return the distance in cm
// no error checking takes place

long measureDistance() {
  long duration, distance;
  Serial.println("Hello from measureDistance");

  // measure how far anything is from us
  // send the pulse
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2); // low for 2 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10); // high for 10 microseconds
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH); // measure the time to the echo
  distance = (duration / 2) / 29.1; // calculate the distance in cm
  return distance;
}

// check the light sensors
void checkLight () {

  Serial.println("Hello from checkLight");
  if (analogRead (leftLDR) > analogRead (rightLDR) ) {

  }

}

