---
tags: Arduino, switch, LED, INPUT_PULLUP, digitalWrite, digitalRead
---
``` c++
const int ledPin = 13;
const int inputPin = 2;
void setup()
{
  pinMode(ledPin, OUTPUT);
  pinMode(inputPin, INPUT_PULLUP);
}

void loop()
{
  digitalWrite(ledPin, (digitalRead(inputPin) == LOW) ? HIGH : LOW);
}

```

```c++
const int ledPin = 13;
const int inputPin = 2;
int count = 0;
void setup()
{
  pinMode(ledPin, OUTPUT);
  pinMode(inputPin, INPUT_PULLUP);
  Serial.begin(115200);
}

void loop()
{
  int swInput = digitalRead(inputPin);
  int ledOutput = digitalRead(ledPin);

  if (swInput == LOW)
  {
    if (ledOutput)
    {
      digitalWrite(ledPin, LOW);
    }
    else
    {
      digitalWrite(ledPin, HIGH);
    }
    count++;
    Serial.println(count);
  }
  delay(100);
}

```