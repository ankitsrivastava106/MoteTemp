Telosb Malicious Temperature Sensor

********************************README********************************

2 Motes Communicating

The code is built off of the Modified Blink Example submitted as the first step of the project.  This code displays the three lowest bits of a counter on the three LEDs.  This counter is incremented as a timer fires.

The code was modified for communication between 2 Motes.  They are both programmed with the exact same code which completes the following procedure:

Starts the Radio when booted -> then a periodic timer once the radio is booted
The timer is set to fire every 1 second
Everytime the timer fires the counter is incremented, a packet is created holding the NODE_ID and the value of the counter, and the packet is sent in a Multicast fashion.
The other mote that receives this packet, checks if it is the correct packet length and then takes the value of the counter from the packet and displays the three lowest bits of a counter on the three LEDs.

Both motes are programmed to do this so every second they will both increment thier respective counters and then send a packet to one another with the value of the counter and then they will display each others three lowest bits of a counter on the three LEDs. 

******************************SCREENSHOT******************************

Because it was hard to capture the Blinking LEDs in a picture for proof it is easier to explain the method of proving that our code was correct.

1)When the first mote is programmed it has no LEDs flashing, which means it is not receiving any packets
2)As soon as the second mote is programmed they both begin to start flashing codes on their LEDs
3)If the RESET button is held on one of the motes, the other mote pauses and displays the LEDs that it was currently displaying without changing.
	-This is the desired behavior because it has not received any other packets because the other mote is paused.
	-When the RESET button is unpressed the other mote starts its LEDs over counting from 0.
	-This is because when the mote was RESET the counter started again back at 0.
4)Another test was to take the motes out of range of each other where they both paused and displayed the LEDs they last had without changing
	-When brought back it range so their radios could communicate the LEDs began changing again

***************MAKEFILE FLAGS***************

-DCC2420_DEF_CHANNEL=20
	Specifies the Operating Channel of the Mote between [13-26]

-DCC2420_DEF_RFPOWER=30
	Specifies the RF Power of transmission of the Mote between [3-31]