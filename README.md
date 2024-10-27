# AVR LED Control with Button Interface

This project demonstrates the basic setup and control of LEDs using an AVR microcontroller. The code utilizes the microcontroller's Port A to control LEDs (PA0-PA3) and handle buttons (PA4-PA7).

## Requirements
- AVR microcontroller (with an 8 MHz clock frequency)
- 4 LEDs connected to pins PA0-PA3
- 4 buttons connected to pins PA4-PA7

## Functionality

### Setup
1. **Clock Frequency:** Set to 8 MHz.
2. **Port A:**
   - Pins PA0-PA3 are configured as outputs to control LEDs.
   - Pins PA4-PA7 are configured as inputs to handle buttons, with internal pull-up resistors enabled.

### Button Controls
- **PA4:** Turns on the currently selected LED.
- **PA5:** Turns off the currently selected LED.
- **PA6:** Toggles the state of the currently selected LED.
- **PA7:** Switches to the next LED (cycling through PA0 to PA3).

### Operation
- The program begins by initializing the ports, with all LEDs turned off initially.
- In the main loop, the microcontroller checks the state of each button (PA4-PA7) and performs the appropriate operations on the currently selected LED.
  - Short delays (`_delay_ms`) are used for buttons PA6 and PA7 to avoid button "bounce" effects (debounce).

## Code Structure
- `init_ports()`: Configures Port A as output for LEDs and input for buttons, and enables pull-up resistors.
- `toggle_led(pin)`: Function to toggle the state of the currently selected LED.
- `next_led()`: Function to switch to the next LED in sequence.
- `main()`: Main loop handling the program's operation.

## Example Usage
1. After connecting the LEDs and buttons to the appropriate pins, run the program on the microcontroller.
2. Use the buttons:
   - **PA4**: To turn on the selected LED.
   - **PA5**: To turn off the selected LED.
   - **PA6**: To toggle the selected LED.
   - **PA7**: To switch control to the next LED (cycling from PA0 to PA3).

## Author
This code demonstrates basic operations on AVR microcontroller ports and is designed for educational projects.

## License
This project is available under the MIT License.

