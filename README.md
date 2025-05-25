This Arduino code manages two solar power batteries, switching between them based on ambient light conditions detected by a photocell. It uses two relays to control the power to each battery and incorporates a delay to prevent rapid switching due to fleeting changes in light.

How the Code Works
The code continuously monitors the light level through a photocell connected to LIGHT_PIN (A0). It then calculates the resistance of the photocell, which changes with light intensity.

Key Components and Their Roles:
Photocell (LIGHT_PIN A0): Measures ambient light.
R1signal_PIN (Digital Pin 10): Controls a relay for Battery 1.
R2signal_PIN (Digital Pin 11): Controls a relay for Battery 2.
DARK_THRESHOLD and LIGHT_THRESHOLD: These are crucial values that you'll need to calibrate for your specific setup. They define the photocell resistance at which the environment is considered "dark" or "light."
DELAY_DURATION (30 seconds): This delay prevents the system from rapidly switching batteries if the light conditions fluctuate briefly. The code needs to sense a consistent light or dark condition for this duration before taking action.
Logic Breakdown:
Read Light Sensor: The loop() function constantly reads the analog value from the photocell, converts it to voltage, and then calculates the photocell's resistance.
Darkness Detection:
If the photocell resistance is greater than or equal to DARK_THRESHOLD, the code recognizes it as "dark."
It then starts a 30-second timer.
If the darkness persists for the entire DELAY_DURATION, Battery 1 is switched OFF (by setting R1signal_PIN HIGH), and Battery 2 is ensured to be ON (by setting R2signal_PIN LOW).
During darkness, the "light" timer and state are reset.
Lightness Detection:
If the photocell resistance is less than or equal to LIGHT_THRESHOLD, the code recognizes it as "light."
Similar to darkness detection, it starts a 30-second timer.
If the lightness persists for the entire DELAY_DURATION, Battery 2 is switched OFF (by setting R2signal_PIN HIGH), and Battery 1 is ensured to be ON (by setting R1signal_PIN LOW).
During lightness, the "dark" timer and state are reset.
Ambient/In-Between State:
If the light conditions are neither consistently dark nor consistently light (i.e., the resistance falls between the LIGHT_THRESHOLD and DARK_THRESHOLD), both timers and states are reset.
In this state, both Battery 1 and Battery 2 are kept ON (both relays are LOW).
Serial Monitor Output: The code prints diagnostic information to the Serial Monitor, showing the voltage, resistance, and the current state of the system, which is very helpful for debugging and calibration.
