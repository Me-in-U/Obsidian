---
tags: Arduino, LED, digitalWrite
---
``` c++
const int ledPin = 13;

void setup()
{
	Serial.begin(115200);
	pinMode(ledPin, OUTPUT);
}

void loop()
{
	digitalWrite(ledPin, HIGH);
    delay(200);
    digitalWrite(ledPin, LOW);

    delay(200);
}
```

