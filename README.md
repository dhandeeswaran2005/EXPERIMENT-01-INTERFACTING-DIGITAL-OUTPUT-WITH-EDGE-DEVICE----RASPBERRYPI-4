# EXPERIMENT-01-INTERFACTING-DIGITAL-OUTPUT-WITH-EDGE-DEVICE---(RASPBERRYPI-PI4)
### NAME : Dhandeeswaran selvakumar
### DEPARTMENT : CSE(IOT)
### ROLL NO : 212223110009
### DATE OF EXPERIMENT : 04-02-2026

### AIM
To interface a digital output device (LED) with the Raspberry Pi 4 and control it using Python.

## APPARATUS REQUIRED
Raspberry Pi 4
LED (Light Emitting Diode)
330Ω Resistor
IR Sensor
Breadboard
Jumper Wires
USB Cable
 ## THEORY

![Raspberry Pi Pin](https://github.com/user-attachments/assets/19e5a1e7-cb46-4909-ba59-e4f4560cae03)





 
 
 
 ### FIGURE-01 RASPI PI 4 PINOUT DIAGRAM 


The Raspberry Pi 4 Model B is built around a Broadcom BCM2711 system-on-chip that integrates a quad-core ARM Cortex-A72 (64-bit) CPU, VideoCore VI GPU, memory controller, and peripheral interfaces, forming a compact yet complete computer architecture where the SoC connects internally to RAM, USB 3.0 controller, Gigabit Ethernet, HDMI display, and wireless modules. Its 40-pin GPIO header provides a flexible pin configuration consisting of power pins (5 V and 3.3 V), multiple ground pins, and general-purpose input/output pins that operate at 3.3 V logic and can be programmed for digital I/O or alternate functions. Key alternate functions include I²C (SDA, SCL) for sensor communication, SPI (MOSI, MISO, SCLK, CS) for high-speed peripheral interfacing, UART (TX, RX) for serial communication, and PWM for control applications.  For communication, I2C (SDA, SCL), SPI (MOSI, MISO, SCK), and UART (TX, RX) interfaces are mapped across different GPIO pins, allowing seamless connectivity with sensors and peripherals. All GPIO pins support PWM (Pulse Width Modulation), making it useful for motor control, LED brightness adjustment, and sound applications. The BOOTSEL button enables USB mass storage mode for firmware flashing, while the DEBUG pins (SWD interface) provide debugging capabilities. With its low power consumption, flexible GPIO options, and rich interface support, the Raspberry Pi Pico is widely used for IoT, embedded systems, robotics, and automation projects.This architecture and pin multiplexing allow the Raspberry Pi 4 to act as both a general-purpose computing platform and an embedded controller, supporting rapid prototyping, hardware interfacing, and IoT applications.


## Working Principle:
Experiment 1A
The LED is connected to one of the GPIO pins of the Raspberry Pi 4.
The Python script sets the GPIO pin HIGH to turn the LED ON and LOW to turn it OFF.
CIRCUIT DIAGRAM
Connect the anode (longer leg) of the LED to GP15 via a 330Ω resistor.
Connect the cathode (shorter leg) of the LED to GND (ground).

Experiment 1B
The LED is connected to one of the GPIO pins of the Raspberry Pi 4.
The IR sensor is connected one of the GPIO pins in Raspberry Pi 4.
The Python script sets the GPIO pin HIGH to turn the LED ON and LOW to turn it OFF based on the IR sensor.
CIRCUIT DIAGRAM
Connect the anode (longer leg) of the LED to any one GPIO via a 330Ω resistor.
Connect the cathode (shorter leg) of the LED to GND (ground).
Connect the IR sensor Vcc to any +5V.
Connect the IR sensor GND to any GND.
Connect the IR sensor OUT to any one GPIO. 

## PROGRAM (Python)
## Experiment 1A
```
import RPi.GPIO as GPIO
import time
import urllib.request

# ThingSpeak details
WRITE_API_KEY = "IARCOVMCT5RNJ5W5"
CHANNEL_ID = 3241534
THINGSPEAK_URL = "https://api.thingspeak.com/update"

# Set GPIO numbering mode
GPIO.setmode(GPIO.BCM)

# Define LED pin
LED_PIN = 18

# Set GPIO18 as output
GPIO.setup(LED_PIN, GPIO.OUT)

def send_to_thingspeak(value):
    url = f"https://api.thingspeak.com/update?api_key=IARCOVMCT5RNJ5W5&field1={value}"
    urllib.request.urlopen(url)
    print("Sent to ThingSpeak:", value)

try:
    while True:
        # LED ON
        GPIO.output(LED_PIN, GPIO.HIGH)
        print("LED ON")
        send_to_thingspeak(1)
        time.sleep(15)

        # LED OFF
        GPIO.output(LED_PIN, GPIO.LOW)
        print("LED OFF")
        send_to_thingspeak(0)
        time.sleep(15)

except KeyboardInterrupt:
    print("Program stopped")

finally:
    GPIO.cleanup()

````

## Experiment 1B
```
import RPi.GPIO as GPIO
import time
import urllib.request

# ThingSpeak details
WRITE_API_KEY = "X839QZ0XT8UUS8KN"
CHANNEL_ID = 3249834
THINGSPEAK_URL = "https://api.thingspeak.com/update"



# Pin setup
SENSOR_PIN = 23   # Input from sensor
LED_PIN = 18      # Output to LED

# GPIO mode
GPIO.setmode(GPIO.BCM)

# Setup pins
GPIO.setup(SENSOR_PIN, GPIO.IN)
GPIO.setup(LED_PIN, GPIO.OUT)

def send_to_thingspeak(value):
    url = f"https://api.thingspeak.com/update?api_key=X839QZ0XT8UUS8KN&field1={value}"
    urllib.request.urlopen(url)
    print("Sent to ThingSpeak:", value)


print("Sensor + LED system running...")

try:
    while True:
        sensor_value = GPIO.input(SENSOR_PIN)

        if sensor_value == 0:   # Many IR sensors give LOW when object detected
            print("Object Detected! LED ON")
            GPIO.output(LED_PIN, GPIO.HIGH)
            send_to_thingspeak(1)

            time.sleep(15)
        else:
            print("No Object. LED OFF")
            GPIO.output(LED_PIN, GPIO.LOW)
            send_to_thingspeak(0)

            time.sleep(15)

        time.sleep(0.1)

except KeyboardInterrupt:
    print("Stopped by user")

finally:
    GPIO.cleanup()

```

### OUPUT  
# Experiment 1A

## LED ON

![led on](https://github.com/user-attachments/assets/6dec38d9-dc05-447a-8e94-ffb39b52dd55)

![thingspeak 1](https://github.com/user-attachments/assets/c2380f0d-c0e2-489e-9534-3edaefc907fb)

<img width="1920" height="898" alt="Screenshot (58)" src="https://github.com/user-attachments/assets/9dced7a8-511e-400f-ab5f-8127f5345dfa" />

## LED OFF

![led off](https://github.com/user-attachments/assets/5da9210c-d568-40a6-a25a-ae2d42ad109e)

![thingspeak 0](https://github.com/user-attachments/assets/35ff85cd-1ea5-4898-add2-9ca74376ca63)

<img width="1920" height="884" alt="Screenshot (59)" src="https://github.com/user-attachments/assets/7370c313-a4aa-4e90-b903-5ac06d57f4e4" />



# Experiment 1B

## OBSTACLE DETECTED 
![led on ir](https://github.com/user-attachments/assets/8cc8d4ed-5a97-4b21-9941-dae2d5dbd307)

![Console 1](https://github.com/user-attachments/assets/b04b1cef-5da0-4642-a379-fd59d9aa2df9)

<img width="1891" height="823" alt="Screenshot 2026-02-05 143015" src="https://github.com/user-attachments/assets/34f707c6-963b-48ba-bb27-c1803b75f9b3" />




## OBSTACLE NOT DETECTED 

![led off ir](https://github.com/user-attachments/assets/39418ee0-842e-462e-aa73-8c9f09fcef24)

![Console 0](https://github.com/user-attachments/assets/71289b92-c860-44ff-a6d5-5bfb125fab01)


<img width="1891" height="823" alt="Screenshot 2026-02-05 143015" src="https://github.com/user-attachments/assets/799cef44-ae67-4db9-a844-bca2ed8b361c" />

 
## RESULTS
The LED connected to the Raspberry Pi 4 successfully turns ON and OFF at  user defined time  confirming the proper interfacing of a digital output.
