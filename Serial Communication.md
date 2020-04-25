# Serial Communication
## What is serial communication?
To transfer data from one system to another there are mainly two ways, **serial communication** and **parallel communtication**. As the name suggests, in serial type, the data is sent in a series form whereas in the parallel type the data is sent in a parallel type. What this means is that in parallel type, we would require a lot of wires connected between the systems which although **very fast** but is often **not feasable**. The serial type on the other hand sends the data in a serial order which therefore requires one cable for data transfer and one or two other for earthing etc. Hence we can deduce that this method is quite **slow** as compared to the other way but **is feasible**.<br><br>
### Serial Communication and Arduino
Serial Communication is a process of sending data 1 bit at a time sequentially over a communication channel. This the way the Arduino board communicates to the computer. Serial Communication is used when we send a commond from computer to Arduino board and vice-versa. Thus, uploading a code uses the same. The LEDs (present on Arduino) **RX** and **TX** flash when the arduino receives data and transmits data respectively.<br>
UART(Universal Asynchronous Receiver/Transmitter) Protocol is used over the USB cable (having three different wires for Transmitting, Receiving and a Ground wire) for Serial Communication with the Arduino. The initialization is made with:<br>
~~~
Serial.begin(speed)
~~~
here, speed is the band rate. The initialization can also be made in the following way providing two arguments speed and configuration:<br>
~~~
Serial.begin(speed, configuration)
~~~
configuration sets data bits, parity bits(to check errors) and stop bit.<br>
For example:<br>
~~~
Serial.begin(9600)
Serial.begin(9600, SERIAL_8N1)
~~~
An increase in band rate increases speed, though increasing the value of band rate above 9600 can cause synchronization errors.<br>We can also send text over Serial, this is done by using **Serial.print()** or **Serial.println()**. Example:
~~~ Serial.println("Hello");
~~~
This prints **Hello** continuously in new lines. Strings are converted into ASCII values and then sent using UART.<br>
Example:
~~~
Serial.write(42);
~~~
This prints asterisk(\*) since the ASCII value of * is 42.<br>
Apart from sending, we can also read data over Serial using Serial Monitor. When data is sent, it goes into a buffer in the Arduino untill it is read. **Serial.Available()** is used to see hpw many bytes are waiting in the buffer. For reading, we use **Serial.read()**. It returns 1 byte from Serial buffer and -1 for no data. **Serial.readBytes()** can be used for writing several data into a buffer. For example:
~~~
char buff[10];
Serial.readBytes[buff,10];
~~~
###### A simple Arduino code:<br>
~~~
void setup() {
Serial.begin(9600);
}

void loop() {
Serial.print('1');
delay(200);
}
~~~
Output:<br>
![Serial Communication](https://cdn.instructables.com/FOO/XDSD/J7JMSYT1/FOOXDSDJ7JMSYT1.LARGE.jpg?auto=webp&frame=1&fit=bounds)<br>
The above picture shows the Serial Output for the code.<br>

You may visit 
[this](https://www.arduino.cc/reference/en/language/functions/communication/serial/)
for more details.<br><br>
### Serial Communication using Python
Python can be used to interact with microcontrollers and other serial-port-enabled devices (including those using virtual ports). <br><br>
![Circuit](https://maker.pro/storage/3ZalKvD/3ZalKvDI6JPuLpMCvWxz2oBSmXKVYf7QkYM8gOTB.jpeg)
<br><br>We use PySerial for the purpose. **Installing PySerial:**<br>
On your computer, open a terminal or command prompt and type in “PIP”. If you get an unrecognized error, then your PIP did not install correctly. When installing Python, make sure that the “Add to environmental variables” option is checked. Once PIP is working, run the command shown below to install PySerial:<br><br>
~~~
pip install PySerial
~~~
![Code](https://maker.pro/storage/GUHsXPu/GUHsXPuNUHsokHAOP5zJtPiLlj99w8WUhPWOuhu3.jpeg)<br><br>
You need to configure a few parameters while using PySerial:<br>
* Baud rate – How fast your COM port operates. Arduino projects tend to operate at 115200
* Port – The name of the port being used (find this in device manager)
* Parity bits – These are used for error correction but are not normally used
* Stop bits – Only one stop bit is ever used unless there are timing issues
* Time out – Used to prevent the serial port from hanging<br><br>
Now, follow the code:<br>
~~~
import serial

serialPort = serial.Serial(port = "COM4", baudrate=115200,
                           bytesize=8, timeout=2, stopbits=serial.STOPBITS_ONE)
~~~
Commonly used Functions for using the Serial Port:
* open() – This will open the serial port
* close() – This will close the serial port
* readline() – This will read a string from the serial port
* read(size) – This will read n number of bytes from the serial port
* write(data) – This will write the data passed to the function to the serial port
* in_waiting – This variable holds the number of bytes in the buffer<br><br>
