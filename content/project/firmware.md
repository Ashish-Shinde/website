+++
# Date this page was created.
date = "2016-04-27"

# Project title.
title = "Firmware/Embedded Systems Projects"

# Project summary to display on homepage.
#summary = "An example of linking directly to an external project website using `external_link`."

# Optional image to display on homepage (relative to `static/img/` folder).
#image_preview = "firm5.png"
#image_preview = "firm6.JPG"
#image_preview = "firm7.jpg"
#image_preview = "firm8.jpg"
#image_preview = "firm10.png"
image_preview = "firm19.jpg"
#image_preview = "firm20.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["firmware"]

# Optional external URL for project (replaces project detail page).
#external_link = "http://example.org"

# Does the project detail page use math formatting?
math = false

+++

### Portable Braille Reader
{{< youtube  B3hEWhktRMw >}}
\\
A portable, low-cost braille reader has adjustable reading speeds and the ability to go back in the text whenever required. A multistate button is used to start, pasue or restart the reading. A user can send any text file to the braille reader by using the Bluetooth on his cell phone. The device follows the Grade-I braille standard by making sure that all the identifier characters are correctly encoded. We also designed a debugger which was used to verify the functioning of the device. A PIC32 is interfaced with a Bluetooth and a putty debugger terminal using UART protocol.  


### Cricket Call Generator
{{< youtube  6zPjkK49ztI >}}
\\
Designed a cricket call generator using a Direct Digital Synthesis (DDS). Various parameters specifying a cricket call such as, chirp repeat interval, syllable duration, number of syllables were entered through an user interface using a TFT screen and a keypad. The keypad keys were debounced in software. To generate the cricket calls in the range of 1 kHz to 6 kHz, we can sample at any frequency greater than 12 kHz to prevent aliasing. However, in order to make sure that the generated sine wave has first harmonic which is at least 20 dB less than the fundamental, we oversample at 96 kHz. A sample value from a 256 entry sine table is sent to a DAC using a SPI channel. 

### 1-DOF Helicopter
{{< youtube  _OEBiSgXTk4 >}}
\\
A one degree of freedom helicopter is constructed with a light movable beam. On the one end of a movable beam we have a motor which provides a lift torque and on the other end we have an angle sensor which is used by the PID (Proportional-Integral-Derivative) algorithm to generate PWM (Pulse Width Modulation) signal which controls the speed of the motor. A PID algorithm continuously modifies the motor control based on the error angle. We also use protection circuitry to protect microcontroller from the motor inductive load. A Potentiometer and a button is used to set the PID parameters and desired angle. The motor control and beam angle data is also displayed on the oscilloscope.

### TFT Video Game
{{< youtube CMDxxUYti2c >}}
\\
The game consists of a paddle, barriers and number of balls which are either reflected or collected by the barriers. The paddle was implemented using an ADC and a potentiometer. The balls collide as per the elastic collision and conserve the momentum. Since the frame rate was required to be minimum 15 frames/second, all the ball collision vector math was performed in fixed-point to make sure that the game does not lag. Along with the TFT display, we also use DMA (Direct Memory Access) to add three different sound effects to the game. The advantage of using DMA is that it operates without any CPU intervention and is capable of transferring data bursts at high sample rates to produce the real time sound effects.

