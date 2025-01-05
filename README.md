# 100 LED Chaser Circuit Using IC555 and CD4017

[![LhBIRMMAGGE](https://i.imgur.com/M3fhr3o.png)](https://www.youtube.com/watch?v=paxPiBps6Mk)
A Chaser Circuit consists of a clocked IC or other electronic unit like an Arduino that drives an array of LEDs in such a way that individual LEDs (or small groups of LEDs) turn on and off in a predetermined and repeating sequence producing a visually attractive pattern.

In this tutorial I am going to create a chaser circuit that can drive 20 or more LEDs using 555 timer IC and CD4017 decade counter. Watch this video for detailed step by step instructions on how to build this circuit and for a complete instruction on how the circuit works.
Video: https://www.youtube.com/watch?v=paxPiBps6Mk 


Components Required
-------------------
For this tutorial we need:
1 x NE555 Timer IC
2 x CD4017 Decade Counters
1 x 10K Resistor
1 x 1K Resistor
3 x 220E Resistors
1 x 33mfd Capacitor 
2 x 2N2222 NPN Transistor
21 x LEDs
1 x Custom Built PCB or Breadboard



How This Circuit Works
----------------------
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhhapy4EPOXE7cxle-_7MgJ4gcjHJLGBijanS8QDfCWxOjWpBFPNTUS5LBrxN1A2y5KH6P8dFpLpgOuEkVMJ84652it0Htsn0MISoVa8yORs62yiEyOfcAVQWEoUZzjJw7DHTPd8h0W3Esr3BsizBz7nfcXntqeVWAlF_O0tHp4e9aadIat0etrYU1zbQE/w640-h360/2.png)

The circuit is very simple. 
The 555 Timer IC operates as a clock oscillator or clock generator. The signal from the 555 IC clocks the 4017 decade counter. Output from PIN-3 of the 555 timer IC is given as an input to PIN-14 of the 4017 IC. Whenever a pulse is received by the 4017 IC, the counter increments the count and activates the corresponding output PIN (Q0 to Q9) causing a shift. This IC can count upto 10.
To know more about the ICs please check out my tutorial no. 26 "555 Pulse Generator Module, How it Works", the link is in the description below.

Now, to flash more than 10 LEDs (upto 100) we need to connect a 2nd decade counter to this setup. The Carry Out pin (CO) PIN-12 of the 1st 4017 IC connects to the clock input pin PIN-14 of the 2nd 4017 IC.
The Carry Out pin goes from LOW to HIGH when the counter of the 1st IC reaches 10. By connecting this pin to the clock input of the 2nd decade counter, we can count numbers higher than 10.

In my first setup, I am flashing the same 10 LEDs using the 2 decade counters. 
The Q0 PIN of the 2nd IC is connected to a NPN transistor. A small input current at the Base of the transistor allows much higher current to flow between the Collector and Emitter. The Q1 PIN of the 2nd 4017 IC is connected to the RESET pin (PIN-15). By connecting Q1 to the RESET pin we stop the 2nd IC from counting further up, resetting itself and sending the control back to the 1st IC.

Now, to add another lot of 10 LEDs we just need to move the RESET pin from Q1 to Q2 and connect the common cathode of the second lot to pin Q1 via a transistor. The anodes connect to the 1st IC exactly the same way the 1st lot of LEDs are connected. 

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj0tlH93OCCX6_gZO6NUIGBUGdVJSAGqv2DWcdoYKRO1LoIQqVUP8nRiJ-mkXR6-EZ0Gy-oT4mNw1NdDmJPlG1sXdHXGxcmQszV3DHX4_ws2inM8Be3n1q8BEgo7BjI0Gmg9srhgH5AjixZ1lP-2gkqpfXDzENEnVUt7OQa5FHlVq2LwwsDdy48hxi2PPc/w640-h360/3.png)

You can continue adding LEDs to the 2nd IC just by moving the RESET pin to the next corresponding pin and connecting the anodes to the 1st IC. To change the speed of the LEDs go ahead and change the capacitor to a higher or lower value.



Bread Board Demo
----------------
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEidbKUHBCWZAeY8QOu7fpdjhwiKbKdH30dK6r6mq87ofV7nX3ezjqb4oMaqyJ2edMBVy0IfN65uoSUs5bvMvD4sXKmX5BpCxHMZu7S5Ug72L0gSsTg6aJJljfkmnH-CBbFI6OtpD0u7jY-5BTb5SJrTtwNBXOreC_MXrq-mzsLl0okxYxLYc-zI8xmsLkU/w640-h360/4.png)

Before designing the PCB, I tested the circuit and its logic on a breadboard.
Setting up 20 LEDs on a breadboard along with other components, made the board way too crowded. So, this is the 555 timer IC generating the pulse and these are the two 4017 ICs that will run the chaser circuit. 

Firing up the circuit, lights up the LEDs and the LEDs appear to chase each other. Bingo, everything works as expected.



The Board Design
----------------
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhflHpljDbjf6ThlvQxIsAgCpyR9umBoQOm3Pk_peBiVSmKFMq0x5K8fq42vuI_MZjq6jpf45ICD-Rz68IaShAOIDvroipvsMypEbrxDkIg-Cic1zAADFvGjQfCI7jePj6dKAwjzUDtnRJjtRhCKBU9F1X2rgMn_sTxuxPqkwCIHhkN588CwDX_Qqenphg/w640-h360/5.png)

Using an EDA I designed the circuit board for this project.
The board has 3 sections. Starting from left to right the 1st section is for powering up the board using a female MicroUSB socket. 
The 2nd section generates the clock pulse using the 555 timer IC. 
The 3rd section is for the 4017 ICs and for connecting the cluster of LEDs.

To create a chaser effect using 10 LEDs, we need to solder one NPN transistor and one 100E/200E resistor in the No.1 sockets of the board. Then we need to connect the RESET pin to terminal number 1. After that, connect the +ve terminals of the 10 LEDs to the bottom "LED Array" and then go ahead and solder all their -ve terminals together. After soldering the -ve terminals, solder this junction to pin number 1 of the "Common Cathode LED Array". That's it as simple as that.

Now, to chase 20 LEDs we need to add another lot of transistor and resistor to socket number 2 of the board and move the RESET pin to terminal number 2. Then connect the +ve terminals of the 2nd lots of LEDs to the bottom LED array and their common cathodes to pin number 2 of the "Common Cathode LED Array" at the top of the board.

We can keep on adding more LEDs to the board just by adding more transistors and resistors and by moving the RESET pin to the next one and by connecting the LED arrays common -ve terminals to the next port of the "Common Cathode LED Array".

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiVFGRwSjDxqq1BvDobzQ7dqz6BMa_uypdovfoWAW5N993WFhv9IRXsYtpIZgdnKSzRKMpmt1D1-ejPNy3sCBuI9jFUZzNNndQY74_ZGFS1k-xdA2HWaO2rMaQeZw5xu-VtCY9Rhyphenhyphen-7Bwb-wXIW-IPjMvZ1wUMCHWAtytu2x7InR9X5uzDRH-NvciQKuCE/w640-h360/6.png)

To make our life easy, I have also created a HAT for this circuit board. You can solder male pin headers on the main board and female pin headers on the hat and then slide the hat on top of the main board.

To flash 10 LEDs, all you have to do is connect the +ve terminals of the LEDs to the 1-10 ports on the board and the common -ve to the -ve port of the same column. You also need to jumper the top two ports to reset the chaser. To add another 10 LEDs just go ahead and connect them to the 2nd column and then jumper the second column's reset pins. Please make sure you only jumper one column at any given time. 



Soldering
---------
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjDFKMuYevmEmnlEgnfR9-Jx3jv4suAiSPnP3OSSKhGs0VanhViijfRncvshUhDY2IyDHx5kDK8oJV2dGbGaU-ut42-1zK28TwfgYYrhHnglouQjuBAGb37NGev2tVFailnvlcQxp6vRgwY7u77uyIGwq_oVhQ1ZBOGV7h2m72vG5QVLaBwPWxlg99rI0U/w640-h360/8.png)

Let's start soldering the components from the left to right of the board. 
Let's first solder the MicroUSB socket to the board. Then, let's solder the IC base for the 555 timer IC and the resistances to the board. Next, let's solder the 3mm red LED and the 33 mfd capacitor to the board.

Now, lets solder the IC bases for the 2 x 4017 ICs to the board. Since I care a lot about my ICs and micro-controllers, I never solder them directly to the board. In case of an ICs, I always try to use IC bases or if a base is not available I use female pin-headers. 

For this demo, I am going to create a chasing effect using 20 LEDs. 
So, I will be adding 2 x transistors and 2 x 100E/220E resistors to the board.

Since I will be using the HAT for connecting the LEDs to the board, I need to solder 3 x male pin-headers to the 3 x sides of the board. That's pretty much all we have to do on the main board.

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhFO77xrOGY-RHLhfKLNm-dS-CpkHr4gwxFdZkKMjxnzltalmw9l_6HfO3acYtSZa9uCR0xN-lGy5A9xsFAcFPsTbgm78Gq_1xn-ZcdSiqNl7Y0b2QfGdj2HOP_cRW0vOKWkxRKGo37F18r2-M324PDRZy2jn_Dl0a1_vK4MOk-z6yU9ea_zFFHavb-FM0/w640-h360/9.png)

Now, let's solder the components to the HAT. To slide the HAT on top of the main board we need to solder female pin-headers to the sides of the HAT. Since, my plan is to create the chasing effect using 20 LEDs I am soldering female pin headers to the first two columns of the HAT. 
As discussed earlier, we need to jump the 2nd column of the HAT to reset the circuit once it finishes the 2nd cycle. If we had another 10 LEDs then we would have jumped the 3rd column and so on.



Demo
----
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEit78lAOQ00lrBy76hyphenhyphenh16KLRkoKA_tKilNYVFYmsPlhH1scawnP3dM1Mz0_T5sVXdb7NYpBwsteRJbVDVw5GAmOEi9yUkDkqlXpWNuTY5LEL5eAnHj8qD66Jsprznn5yq5qAOnBg_aJD9pr0OtDoeWB7MbGPSrg5gPd3ZQr4wP-9yAd8t-UM_FR701cDk/w640-h360/10.png)

So, this is how my final setup looks like.
Lets slide the 20 LEDs into the female pin-headers and fire-up the circuit. Bingo, job done. 

The possibilities are endless and I know you guys have a lot going on in your mind. So, what are you waiting for?

Do comment and let me know if there are any scopes of improvement. 



Thanks
------
[![LhBIRMMAGGE](https://i.imgur.com/M3fhr3o.png)](https://www.youtube.com/watch?v=paxPiBps6Mk)

Thanks again for checking my post. I hope it helps you.
If you want to support me subscribe to my YouTube Channel: https://www.youtube.com/user/tarantula3


Video: [View](https://youtu.be/paxPiBps6Mk)

Full Blog Post: [View](https://diyfactory007.blogspot.com/2025/01/100LED.html) 


## References
GitHub: https://github.com/tarantula3/100-LED-Chaser-Circuit-Using-IC555-and-CD4017/tree/main

Gerber: https://github.com/tarantula3/100-LED-Chaser-Circuit-Using-IC555-and-CD4017/tree/main

DIY 555 Pulse Generator Module: https://youtu.be/bMAnipPOjFo


## Support My Work

BTC: 1Hrr83W2zu2hmDcmYqZMhgPQ71oLj5b7v5

LTC: LPh69qxUqaHKYuFPJVJsNQjpBHWK7hZ9TZ

DOGE: DEU2Wz3TK95119HMNZv2kpU7PkWbGNs9K3

ETH: 0xD64fb51C74E0206cB6702aB922C765c68B97dCD4

BAT: 0x9D9E77cA360b53cD89cc01dC37A5314C0113FFc3

BNB: 0xD64fb51C74E0206cB6702aB922C765c68B97dCD4

POL: 0xD64fb51C74E0206cB6702aB922C765c68B97dCD4

LBC: bZ8ANEJFsd2MNFfpoxBhtFNPboh7PmD7M2

COS: bnb136ns6lfw4zs5hg4n85vdthaad7hq5m4gtkgf23 Memo: 572187879


Thanks, ca again in my next tutorial.



Tags
----
chaser circuit,led chaser,step by step led turn on and off,led,running led,beautiful led effect,led chaser circuit,electronics,how to make a led lighting circuit,beautiful led light,new led circuit,20 step shifting,20 LED Step by Step Running Circuit Using CD4017 IC,bitwise shift,flipflop,555 Pulse Generator,20 LED Step by Step Running Circuit Using CD4017 IC,es tech,100 led chaser

Rumble: https://rumble.com/v64k48j-100-led-chaser-circuit-using-ic555-and-cd4017.html
Odysee: https://odysee.com/@Arduino:7/100-LED-Chaser-Circuit-Using-IC555-and-CD4017:d 
Cos: https://cos.tv/videos/play/57967446799454208 

Blog1: https://diyfactory007.blogspot.com/2025/01/100LED.html
Blog2: https://diy-projects4u.blogspot.com/2025/01/blog-post.html
