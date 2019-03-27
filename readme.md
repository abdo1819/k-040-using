# Introduction:[[1]](https://en.wikipedia.org/wiki/Rotary_encoder)
```
A rotary encoder, is an electro-mechanical device that converts the angular position or motion of a shaft or axle to analog or digital output signal
```

There are two main types of rotary encoder: absolute and incremental. 
* The output of an absolute encoder indicates the current shaft position, making it an angle transducer. 
* The output of an incremental encoder provides information about the motion of the shaft, which typically is processed elsewhere into information such as position, speed and distance.

# k-040

is and increamental encounter as it provide a signal when 
it's stat changed [[2]](http://henrysbench.capnfatz.com/henrys-bench/arduino-sensors-and-input/keyes-ky-040-arduino-rotary-encoder-user-manual/)

## working concept:[[3]](http://henrysbench.capnfatz.com/henrys-bench/arduino-sensors-and-input/keyes-ky-040-arduino-rotary-encoder-user-manual/)

<p>A rotary encoder has a fixed number of positions per revolution.   These positions are easily felt as small &#8220;clicks&#8221; you turn the encoder.<br />
The Keyes module that I have has thirty of these positions.</p>
On one side of the switch there are three pins.   They are normally referred to as A, B and C.   In the case of the KY-040,  they are oriented as shown.</p>
<p>Inside the encoder there are two switches.  Once switch connects pin A to pin C and the other switch connects pin B to C.</p>
<p>In each encoder position, both switches are either opened or closed.  Each click causes these switches to change states as follows:</p>
<ul>
<li><span style="color: #0000ff;"><strong>If both switches are closed</strong></span>,  turning the encoder either clockwise or counterclockwise one position will cause both switches to open</li>
<li><span style="color: #0000ff;"><strong>If both switches are open</strong></span>, turning the encoder either clockwise or counterclockwise one position will cause both switches to close.</li>
</ul>
<p>The illustration below is representative of how the switch is constructed.</p>
<p><a href="https://i1.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Rotary-Encoder-Representation.png"><img class="aligncenter wp-image-1056 size-full" src="https://i1.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Rotary-Encoder-Representation.png?resize=420%2C300" alt="Rotary Encoder Representation" width="420" height="300" srcset="https://i1.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Rotary-Encoder-Representation.png?w=420 420w, https://i1.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Rotary-Encoder-Representation.png?resize=300%2C214 300w" sizes="(max-width: 420px) 100vw, 420px" data-recalc-dims="1" /></a>As you can see, the angular position of the A terminal and the B terminal is such that:</p>
<ul>
<li><span style="color: #0000ff;"><strong>Rotating the switch clockwise</strong></span> will cause the switch connecting A and C to change states first.</li>
<li><strong><span style="color: #0000ff;">Rotating the switch counterclockwise</span></strong> will cause the switch connecting B and C to change states first.</li>
</ul>
<p>If we were to represent the opening an closing of the switches as wave forms, it would look something like this.</p>
<p><a href="https://i1.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Rotary-Encoder-Phases.png"><img class=" size-full wp-image-556 aligncenter" src="https://i1.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Rotary-Encoder-Phases.png?resize=302%2C240" alt="Rotary Encoder Phases" width="302" height="240" srcset="https://i1.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Rotary-Encoder-Phases.png?w=302 302w, https://i1.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Rotary-Encoder-Phases.png?resize=300%2C238 300w" sizes="(max-width: 302px) 100vw, 302px" data-recalc-dims="1" /></a>Essentially,   determining which switch changed states first is how the direction of rotation is determined.</p>
<p>If A changed states first, the switch is rotating in a clockwise direction.</p>
<p>If B changed states first, the switch is rotating in a counter clockwise direction.</p>
<h1><span id="KY-040_Pin_Outs">KY-040 Pin Outs</span></h1>
<p>The pin outs for this rotary encoder are identified in the illustration below.</p>
<p><a href="https://i0.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Keyes-KY-040-Rotary-Encoder-Pin-Outs.png"><img class=" size-full wp-image-559 aligncenter" src="https://i0.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Keyes-KY-040-Rotary-Encoder-Pin-Outs.png?resize=351%2C109" alt="Keyes KY-040 Rotary Encoder Pin Outs" width="351" height="109" srcset="https://i0.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Keyes-KY-040-Rotary-Encoder-Pin-Outs.png?w=351 351w, https://i0.wp.com/henrysbench.capnfatz.com/wp-content/uploads/2015/05/Keyes-KY-040-Rotary-Encoder-Pin-Outs.png?resize=300%2C93 300w" sizes="(max-width: 351px) 100vw, 351px" data-recalc-dims="1" /></a>The module is designed so that a low is output when the switches are closed and a high when the switches are open.</p>
<p>The low is generated by placing a ground at Pin C and passing it to the CLK and DT pins when switches are closed.</p>
<p>The high is generated with a 5V supply input and pullup resistors, such that CLK and DT are both high when switches are open.</p>
<p>Not previously mentioned is the existence of of push button switch that is integral to the encoder.   If you push on the shaft, a normally open switch will close.    The feature is useful if you want to change switch function.   For example,  you may wish to have the ability to between coarse and fine adjustments.</p>


# arduino implementation
we may connect rotary c to ground 
and just measure from a and b

idealy when rotating Clockwise then counterclockwise
reads will be[[5]](https://tkkrlab.nl/wiki/Arduino_KY-040_Rotary_encoder_module)
<table class="wikitable">

<tbody><tr>
<th> A(clk)
</th>
<th> B(DT)
</th></tr>
<tr>
<td> 1
</td>
<td> 1
</td></tr>
<tr>
<td> 0
</td>
<td> 1
</td></tr>
<tr>
<td> 0
</td>
<td> 0
</td></tr>
<tr>
<td> 1
</td>
<td> 0
</td></tr>
<tr>
<td> 1
</td>
<td> 1
</td></tr>
<tr>
<td> 1
</td>
<td> 0
</td></tr>
<tr>
<td> 0
</td>
<td> 0
</td></tr>
<tr>
<td> 0
</td>
<td> 1
</td></tr></tbody></table>





the mean idea is to count the changes of switches and witch one has changed as indiacation of direction
here is simple implemetation with light indiction and serial value [[4]](https://www.hackster.io/vandenbrande/arduino-rotary-encoder-simple-example-ky-040-b78752)
![connections](https://hackster.imgix.net/uploads/cover_image/file/145888/KY-040%20Rotary%20Encoder%20schematic_bb.png?auto=compress%2Cformat&w=900&h=675&fit=min)

```c
/* Author: Danny van den Brande, Arduinosensors.nl
 This is a example on how to use the KY-040 Rotary encoder. 
 Its very basic but if your new to arduino or could not find 
 any code, then you have something to start with.
 because there is little documentation about the KY sensor kit.
 */
 int CLK = 9;  // Pin 9 to clk on encoder
 int DT = 8;  // Pin 8 to DT on encoder
 int RedLed = 4;// You do not need to use the leds. 
                // you can take a look in the serial monitor if you dont have leds.
                // there it will display values. 
 int GreenLed = 5;
 int BlueLed = 6;
 int RotPosition = 0; 
 int rotation;  
 int value;
 boolean LeftRight;
 void setup() { 
   Serial.begin (9600);
   pinMode (CLK,INPUT);
   pinMode (DT,INPUT);
   pinMode (RedLed, OUTPUT);
   pinMode (GreenLed, OUTPUT);
   pinMode (BlueLed, OUTPUT);
   rotation = digitalRead(CLK);   
 } 
 void loop() { 
   value = digitalRead(CLK);
     if (value != rotation){ // we use the DT pin to find out which way we turning.
     if (digitalRead(DT) != value) {  // Clockwise
       RotPosition ++;
       LeftRight = true;
     } else { //Counterclockwise
       LeftRight = false;
       RotPosition--;
     }
     if (LeftRight){ // turning right will turn on red led.
       Serial.println ("clockwise");
       digitalWrite (RedLed, HIGH);
       digitalWrite (GreenLed, LOW);
     }else{        // turning left will turn on green led.   
       Serial.println("counterclockwise");
       digitalWrite (RedLed, LOW);
       digitalWrite (GreenLed, HIGH);
     }
     Serial.print("Encoder RotPosition: ");
     Serial.println(RotPosition);
     // this will print in the serial monitor.
     
   } 
   rotation = value;
 } 
 ```

 # improvemed implemtation
 * as you can here see last implemetation will result some bouncing and miss some reads 

 <iframe width="560" height="315" src="https://www.youtube.com/embed/cYCTMdUi8P0?start=21" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


> one implemetaion for testing this
* check last value and make sure it will lead to the next one so we minimize missleading signals as here
[source](https://www.brainy-bits.com/arduino-rotary-encoder-ky-040)
```c
 if ((PreviousCLK == 0) && (PreviousDATA == 1)) {
    if ((digitalRead(PinCLK) == 1) && (digitalRead(PinDT) == 0)) {
      displaycounter++;
      P.print(displaycounter);
    }
    if ((digitalRead(PinCLK) == 1) && (digitalRead(PinDT) == 1)) {
      displaycounter--;
      P.print(displaycounter);
    }
  }

if ((PreviousCLK == 1) && (PreviousDATA == 0)) {
    if ((digitalRead(PinCLK) == 0) && (digitalRead(PinDT) == 1)) {
      displaycounter++;
      P.print(displaycounter);
    }
    if ((digitalRead(PinCLK) == 0) && (digitalRead(PinDT) == 0)) {
      displaycounter--;
      P.print(displaycounter);
    }
  }

if ((PreviousCLK == 1) && (PreviousDATA == 1)) {
    if ((digitalRead(PinCLK) == 0) && (digitalRead(PinDT) == 1)) {
      displaycounter++;
      P.print(displaycounter);
    }
    if ((digitalRead(PinCLK) == 0) && (digitalRead(PinDT) == 0)) {
      displaycounter--;
      P.print(displaycounter);
    }
  }  

if ((PreviousCLK == 0) && (PreviousDATA == 0)) {
    if ((digitalRead(PinCLK) == 1) && (digitalRead(PinDT) == 0)) {
      displaycounter++;
      P.print(displaycounter);
    }
    if ((digitalRead(PinCLK) == 1) && (digitalRead(PinDT) == 1)) {
      displaycounter--;
          P.print(displaycounter);
    }
  }            
```


* we may also enaple pull up in both clk,dt pins 
to get more accurate switching (remeber to correct the state changes)
```c
pinMode (CLK,INPUT_PULLUP);
pinMode (DT,INPUT_PULLUP);
```

* other thing that last implementation didn't take care of timing or how fast the avr will read that value as result,
we can miss some readings
so implementing with normal c code using avr pins may increase the speed for more critical tasks like reading pin value use this
```c
dt_reading = PIND & (1<</*pin number*/)
```
