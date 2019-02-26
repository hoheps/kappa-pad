# KappaPad

Repo was forked from fb39ca4.

KappaPad is a two-button keypad intended for playing osu!. Unlike other keypads with mechanical switches, KappaPad has fixed metal pads and uses capacitive sensing to determine when they are being pressed. Because there is no key travel, one can minimize the distance their fingers move to conserve stamina during long streams.

![KappaPad](images/f.jpg?raw=true)

## Usage

Just plug the KappaPad into a computer, and it should work as a USB keyboard, with the keys bound to Z and X. (The key bindings can be changed in the Arduino sketch.) The side button works an as Esc key.

## How to Make One

There aren't any plans to sell these yet, but it is fairly simple to build your own. Here is an example of how to build one, but you don't have to follow it exactly. Just use the materials you have on hand.

### Physical Construction

I 3d printed the (attached as an .stl file). The base is attached with a silicone sticky pad.

### Electronics

![Closeup of Electronics](images/e.jpg?raw=true)

Components Used

* Solder
* Around 1.5m of 3d printing filament
* Clone of Arduino Pro Micro
* 2x 330 kOhm Resistor
* Solid-Core Wire
* Brass plate

The keys were made out of .01 millimeter brass plate, with the wires soldered on. Apparently aluminum is better but I think brass is better.

### Software

The Arduino Sketch is located in the KappaPad directory of this repository. It requires the [CapacitiveSensor library](https://github.com/PaulStoffregen/CapacitiveSensor) so install that first. 

Make sure the correct pin numbers are given where the CapacitiveKey classes are initialized, and make sure the disable pin (15 by default) is accessible on your board.

Upload the sketch to the board using the appropriate board type. (Use Arduino Leonardo if you have a Pro Micro.) After uploading, note that your board may recieve a different serial port number.

At this point the keyboard may work, or the treshold values may have to be adjusted. If keys act like they are being held down and your computer is now unusable when the keypad is plugged in, connect a wire from the disable pin to ground to stop keypresses from being sent. If the keys do not work, uncomment the `#DEFINE SERIAL_OUTPUT` and reupload the sketch. Now, when you open the Arduino serial monitor (at 115200 baud) you should see the sensed capacitance for each key. Change the tresholds so that they are just above the largest values you see when not touching the keys, and reupload the sketch. Once you are satisfied with the operation of the keyboard, disable serial output again to improve performance.
