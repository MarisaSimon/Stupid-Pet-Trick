# Stupid-Pet-Trick

// code based off of Arduino Projects Book and slightly modified for my specific project

int sensorValue;
int sensorLow = 1023;
int sensorHigh = 0;

const int ledPin = 13;

void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, HIGH);

  while (millis() < 5000) {

    sensorValue = analogRead(A0);
    if (sensorValue > sensorHigh) {
      sensorHigh = sensorValue;
    }

    if (sensorValue < sensorLow) {
      sensorLow = sensorValue;
    }
    Serial.print("Sensor Value = ");
    Serial.println(sensorValue);
    delay(5);
  }

  digitalWrite(ledPin, LOW);
}

void loop() {
  sensorValue = analogRead(A0);
  Serial.print("Sensor Value = ");
  Serial.println(sensorValue);
  delay(5);

  int pitch = map(sensorValue, sensorLow, sensorHigh, 50, 4000);

  tone(12,pitch,25);

  delay(11);
}
