🚦 Smart Traffic Light System (STM32 + FreeRTOS)

This project implements a smart, congestion-adaptive traffic light controller using an STM32 microcontroller. The system uses ultrasonic sensors, TM1637 displays, FreeRTOS tasks, and a 4×4 keypad with PIN authentication to control two-lane traffic intelligently.

📌 Features
✅ 1. Congestion Detection (Ultrasonic Sensors)

Each lane uses two HCSR04 sensors to detect vehicles.

If both sensors read < 15 cm, the lane is considered congested.

Traffic light green times adjust dynamically:

Lane with congestion gets extended green.

Opposing lane gets shorter green.

Both lanes congested → equal moderate green.

No congestion → default timing.

✅ 2. FreeRTOS-Based Task Management

TrafficLightTask handles:

Green / Yellow / Red light sequencing

Display countdown on TM1637 modules

Dynamic timing updates based on congestion

password_task manages keypad input and system access control.

testing task continuously reads sensor data for debugging.

✅ 3. Keypad PIN Authentication

4-digit PIN (default: 1234)

Press * to enter PIN mode

Press # to submit

Correct PIN → traffic starts

Wrong PIN → “Access Denied”

✅ 4. Display Systems

Two TM1637 4-digit displays show countdown timers for each lane.

LCD displays user prompts and messages.

🧩 System Components
Hardware Used

STM32 microcontroller

4×4 matrix keypad

TM1637 7-segment displays

HCSR04 ultrasonic sensors (4 units total)

LCD (16x2 or compatible)

Traffic light LED signals (Green, Yellow, Red)

Driver circuits + GPIO interface

📁 Project Structure

Main functionality is handled inside main.c:

Function	Purpose
TrafficLightTask()	Controls traffic timing & displays
password_task()	Keypad authentication
testing()	Live sensor reading
setup_sensors()	Initialize all HCSR04 modules
traffic_congetion()	Lane congestion logic
scan_keypad()	Keypad scanning routine
⏱ Traffic Light Timing Logic

Timing values automatically adjust:

Example:

Lane 1 congested → Lane 1 green = 20s, Lane 2 green = 8s

Lane 2 congested → Lane 2 green = 20s, Lane 1 green = 8s

Both congested → both get 15s green

No congestion → each gets 12s green

Yellow is always 3 seconds.

🛡 Access Control Workflow

System starts with a Welcome message.

User presses * to start PIN entry.

PIN appears as **** on LCD.

Correct PIN → both lanes set to red for 10 seconds → system activates.

🔧 How to Build & Flash

Open the project using STM32CubeIDE

Generate code (if modifying .ioc)

Build project

Flash to STM32 board using ST-Link

Start system

📸 Future Enhancements (Optional)

IoT remote monitoring

Cloud-based traffic analytics

Emergency vehicle priority mode

Web control panel

📜 License

This project is provided under MIT License unless otherwise specified.
