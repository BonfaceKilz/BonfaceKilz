+++

date = "2017-04-28T18:56:26+03:00"
description = "A short introduction to AVR Timers"

title = "AVR Timers"

[taxonomies]
tags = ["electronics, AVR, timers"]
categories = ["electronics"]
+++

### Introduction ###
AVR microcontrollers have internal timers/ counters in them. Within the microcontroller, there are special registers that you can use to control these timers. Most AVR microcontrollers have 8 bit and/ or 16 bit timers in them. 8 bit timers use 8 bit registers while 16 bit timers have 16 bit registers in them. 8 bit counters are able to count 256 steps(2^8) and the 16 bit counters are able to count 65536 steps(2^16). Since timers are able to "count", they are also known as _counters._ Another important thing to point out is that timers are independent of CPU and that they can be operated in several modes:  
1. CTC mode  
2. Normal mode  
3. PWM mode  
In this article, the normal mode is used. Other modes will be discussed in future blog posts.

Another important concept to get down when working with timers/ counters is the concept of prescalers. To understand how prescalers work, you need to understand the concept of frequency and how the timer does the actual counting.

_Frequency_ is simply the number of counts per second. The period is how long a single count takes. The period is the inverse of frequency.
<center>
<math style="font-weight:bold;">
    <mrow>
        <mo>Frequency</mo>
        <mo>=</mo>
        <msup>
            <mi>Period</mi>
            <mn>-1</mn>
        </msup>
    </mrow>
</math>
</center>

The timer count can be calculated from the _delay_ (of the signal) we want and the clock period. It's calculated as follows:

<center>
    <math style="font-weight:bold;">
        <mo>Timer Count</mo>
        <mo> = </mo>
        <mfrac>
            <mi>Delay</mi>
            <mn>Time Period</mn>
        </mfrac>
        <mo> - </mo>
        <mo>1</mo>
    </math>
</center>

Note that we substract one because we start our count from 0. Let's say we had a uController that has a frequency of 4 Mhz and a 16 bit timer. If we substitute in the above formula, we get a maximum delay of 16.384ms. What do you do if you want to vary the value of this delay? Well, you'd first decrease the value of the Time Period which leads to a reduced value of the _timer counter_. In our case, if we reduced the frequency to 500 kHz(and our delay as 20ms), the _timer count_ would be 9999. With this timer count, the maximum delay is 131.072ms.

How do we reduce this frequency? _This is where **prescaling** comes in_. The actual frequency of the uController does not change. Instead, a technique of frequency division called _prescaling_ is applied to get the frequency we want. An important thing to remember here is that as you increase the desired time delay, the resolution reduces.

### The Registers ###
(i) **TCCRx Register**[Timer Counter Control Register]:
The first 3 bits are used to set the prescaler. Also used to configure mode of operation and other settings. In CTC mode, the timer compare value is stored in the WGM(Wave Generation Mode) Bits.

```
/*
 * In this example, we use a prescaler value of 64
 * and set the CTC mode. You can find this info in
 * the data sheet.
 */
TCCR1B |= (1 << WGM12)|(1 << CS11)|(1 << CS10);
```
(ii) **OCRxA/OCRxB Register**[Output Compare Register]:
These registers are utilised in the CTC mode. They store the compare value i.e. the value that will be compared with the counter's value. Here's an example usage:

```
/*
 * Our compare value is 24356
 *
 */
OCR1A = 24356
```

(iii) **TCNTx Register**[Timer Counter Register]:
The Timer/ Counter values is stored here.  
3. **TIMSK Register**[Timer Interrupt Mask Register]:
TOIEx(replace x with number) bit of this register is used to enable/ disable the Timer Overflow Interrupt Flag. It also has the Output Compare A/B Match Interrupt Enable(OCIEx) bits. Enabling these bits ensures that an interrupt is fired whenever a match occurs.  
4. **TIFR Register**[Timer Interrupt Flag Register]:
TOVx flag is used to check if the timer overflows. It is set whenever the timer overflows and cleared automatically as soon as the Interrupt Service Routing is executed. This register also has the OCF(Output Compare Flag) Bits which is set whenever a match occurs(TCNT1A becomes equal to OCF1A). It is cleared automatically whenever the ISR is executed. Clearing is done by writin a '1' to it.  
Here are some code snippets that use these registers(atmega 32/ 16 is assumed to be used here): https://github.com/BonfaceKilz/AVR-Playground/tree/master/timers/src

For now, that's it. I'll hopefully write more on this later.


### Resources ###
1. [Introduction to AVR Timers](https://maxembedded.wordpress.com/2011/06/22/introduction-to-avr-timers/ ) 
2. [8 bit timers](http://www.electroschematics.com/9785/atmega8-advanced-guide-8-bit-timers/ ) 
3. http://www.electroschematics.com/9846/avr-8-16-bit-timers-counters/
