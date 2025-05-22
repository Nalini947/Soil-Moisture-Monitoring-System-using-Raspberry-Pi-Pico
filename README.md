// Soil Moisture Monitoring System using Raspberry Pi Pico

const int sensorPin = 26; // GPIO26 = ADC0
int sensorValue = 0;
int moisturePercent = 0;

// Define moisture calibration values
const int airValue = 3700;    // Analog value when soil is dry
const int waterValue = 1200;  // Analog value when soil is fully wet

void setup() {
  Serial.begin(9600);
  delay(2000);
  Serial.println("Soil Moisture Monitoring Started");
}

void loop() {
  sensorValue = analogRead(sensorPin);  // Read ADC value from sensor

  // Map sensor value to moisture percentage
  moisturePercent = map(sensorValue, airValue, waterValue, 0, 100);
  moisturePercent = constrain(moisturePercent, 0, 100); // Clamp value between 0-100%

  // Print to serial monitor
  Serial.print("Raw ADC Value: ");
  Serial.print(sensorValue);
  Serial.print(" | Soil Moisture: ");
  Serial.print(moisturePercent);
  Serial.println(" %");

  delay(1000); // Delay for 1 second
}
