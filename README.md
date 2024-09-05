# Counter Button

## Description

The Counter Button project uses a push button to increment a counter displayed on a 7-segment display. Each time the button is pressed, the counter increases by one. The 7-segment display shows the current count in a two-digit format.

## Components

- Arduino (e.g., Arduino Uno)
- 7-Segment Display
- Push Button
- Resistors (if required for 7-segment display and button)
- Jumper Wires

## Pin Configuration

| Component                      | Pin Number |
| ------------------------------ | ---------- |
| 7-Segment Display Segment Pins | 2 - 9      |
| Digit Select 1                 | 10         |
| Digit Select 2                 | 11         |
| Push Button                    | 12         |

## Code

```cpp
// Counter-Button
#define tombol 12

byte i,jumlah;
byte seven_seg_digits[10][7] = { { 0,0,0,0,0,0,1 },  // = 0
                                 { 1,0,0,1,1,1,1 },  // = 1
                                 { 0,0,1,0,0,1,0 },  // = 2
                                 { 0,0,0,0,1,1,0 },  // = 3
                                 { 1,0,0,1,1,0,0 },  // = 4
                                 { 0,1,0,0,1,0,0 },  // = 5
                                 { 0,1,0,0,0,0,0 },  // = 6
                                 { 0,0,0,1,1,1,1 },  // = 7
                                 { 0,0,0,0,0,0,0 },  // = 8
                                 { 0,0,0,0,1,0,0 }   // = 9
                                };

void setup() {
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(10, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(12, INPUT);
  digitalWrite(9,HIGH);
  digitalWrite(12,HIGH);

}

void sevenSegWrite(byte segment) {
  byte pin = 2;
  for (byte segCount = 0; segCount < 7; ++segCount) {
    digitalWrite(pin, seven_seg_digits[segment][segCount]);
    ++pin;
  }
}

void loop() {
  if(digitalRead(tombol)==0){
    jumlah++;
  }
  for(i=0;i<100;i++){
      digitalWrite(10,LOW);
      digitalWrite(11,HIGH);
      sevenSegWrite(jumlah/10);
      delay(5);
      digitalWrite(10,HIGH);
      digitalWrite(11,LOW);
      sevenSegWrite(jumlah%10);
      delay(5);
  }
}
```

## How It Works

1. Initialization:
   - The setup() function configures the pins connected to the 7-segment display and button.
   - The button pin is set as an input, and the other pins are set as outputs.
2. Counter Operation:
   - In the loop() function, the code checks if the button is pressed (digitalRead(tombol) == 0).
   - If the button is pressed, the counter (jumlah) increments by 1.
   - The display updates to show the current count using the sevenSegWrite() function, which manages the 7-segment display.
3. Display Control:
   - The sevenSegWrite() function sends signals to the 7-segment display to show the current digit.
   - The display alternates between showing the tens and units digits with a brief delay.

## Usage

1. Connect the 7-segment display and push button to the Arduino using the specified pin configuration.
2. Upload the code to the Arduino.
3. Press the button to increment the counter and observe the updated count on the display.

## Notes

- Ensure that the 7-segment display is correctly wired and that the push button is functioning as expected.
- Adjust resistor values if necessary to ensure proper operation of the display and button.
