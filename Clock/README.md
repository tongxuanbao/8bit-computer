# Clock Module

*Read this in other languages: [English](README.md), [Tiếng Việt](README.vn.md)*

## SR Latch
This one is how SR latch works

## 555 Timer Circuit

There are a lot of ways to build a clock for the computer. But we want the clock to be relatively flexible. We want to be able to adjust the speed. We do not want it to run too fast. One way to do it is using the classic 555 timer.

![Simple Timer Image](SimpleTimer.jpg "Simple Timer")

The 555 timer is powered by a 5V goes to pin 5 and and grounded to pin 1. And to control the timing, we have two resitors, 1k Ohm resistor goes from 5V to pin 7 and 1M Ohm resistor goes from pin 6 to pin 7 of the chip. Pin 6 and pin 2 are connected by the purple wire like above. A capacitor 1μF goes from pin 2 to ground. And the output of the chip (Pin 3) is connected to an LED.

![Diagram](Diagram.gif "Diagram")

This diagram is one way to understand what is going on inside the 555 timer. 

Inside the timer we have three 5K Ohm resistors (That is where the name "555" comes from). And they form a series and go from 5V to ground. This will make the voltage after passing the first resistor will be around 3.33V and after passing the second resistor is 1.67V.

When we first power it up, Pin 2, 6, and 7 are all have 0V. This will set the initial state for the comparators. (The way a comparator/"Triangle" work is it simply output which pin has the higher voltage). The top comparator has 3.33V at the negative input and 0V at the positive input, then the comparator will be off. The similar thing happens at the bottom comparator, we have the positive input is 1.67V and the negative input is 0V, the comparator will be on. This implies the SR latch is set, the latch will output on and the LED will be up.

What will happen next is the current is going to flow through 1K resistor and 1M resistor, then charge the capacitor. While the capacitor is charging, the voltage at Threshold and Trigger will rise until it get above 3.33V. At that point, the top comparator will be on and reset the SR latch. The result is the output will be off.

When the output is off, we have oposite pin will be on then it will active the transitor and allow current to go through it. At this state, both current from power source and the capacitor will go to pin 7. The capacitor will start to discharge. The voltage at pin 6 and 2 will fall until it hit below 1.67V. Then it will start to charge again.


![Simple Timer Behavior](SimpleTimerBehavior.gif "Simple Timer Behavior")

This loop will continue and the circuit final behavior will be on and off over and over again, implies that the LED will flash. And you can see that, the charging speed of the capacitor depend on the value of the resistor and the capacitor itself. When charging it will go though 2 resistors but when discharging it will go through only 1. Therefore, to make the timing of on and off state to be the same, we should choose one resistor to be extremely smaller than (in this case is 0.1%). Lastly, we can control the speed of the circuit by replacing the resistor to be a potentiometer. In this case i use 1M potentiometer.

This is the clock with adjustable speed.

![Timer Behavior](TimerBehavior.gif "Timer Behavior")
