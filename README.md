# Automated Bottle Inspection and Sorting System

This project is an STM32-based embedded system designed to automate the quality control process of bottle filling. The system reads sensor data to verify whether a bottle is correctly filled to a specific threshold and then automatically sorts the bottles into "Accepted" or "Rejected" bins.

## Features

*   **Automated Inspection:** Uses an ADC (Analog-to-Digital Converter) to read the fill level or quality sensor.
*   **Real-time Display:** Uses an LCD to display the status of the current bottle ("Accepted" or "Rejected") and keeps a running count of total accepted and rejected bottles.
*   **Physical Sorting:** Outputs a PWM signal (via Timer 3) to control a servo motor, which physically sorts the bottles based on the inspection result.
*   **Serial Monitoring:** Sends status updates (`"BOTTLE FILLING..."`, `"BOTTLE CHECKING..."`, process halted/resumed) over UART for monitoring on a computer.
*   **Pause/Resume Control:** Includes a hardware interrupt (debounced) for an emergency stop or manual pause button.

## Hardware Components

*   **Microcontroller:** STM32 Series 
*   **Sensor:** Analog sensor connected to ADC1 (Channel 0).
*   **Display:** LCD screen.
*   **Actuator:** Servo motor controlled via PWM on TIM3 (Channel 1).
*   **Control Input:** Push button connected to PA12 for the pause/resume interrupt.

## How it Works

1.  **Read Sensor:** The system triggers an ADC conversion to read the analog value from the sensor.
2.  **Threshold Logic:**
    *   If the ADC level is between `870` and `1524`, the bottle is considered **Accepted**. The servo PWM pulse is set to `1500`.
    *   If the ADC level is outside this range, the bottle is **Rejected**. The servo PWM pulse is set to `2000`.
3.  **Update UI:** The LCD and UART interfaces are updated with the result and current statistics.
