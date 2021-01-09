In [this video](https://youtu.be/NoUetPb6N6g) I used TCP sockets. I have since switched to UDP sockets with no buffering. Results are similarly smooth but servos are more responsive.

I use the following setup:

- [SparkFun ESP32 Thing](https://www.sparkfun.com/products/13907)
- [MG92B servos](http://www.towerpro.com.tw/product/mg92b/) 
- ESP32 is an access point (creates a wifi network) and a UDP socket server
- gamepad communicates with the phone over bluetooth
- phone joins the wifi network and sends data to the UDP socket
- I need only one-way communication


To get this working I used esp-idf and Kolban's book:

- http://esp-idf.readthedocs.io/en/latest/
- https://github.com/espressif/esp-idf-template
- https://leanpub.com/kolban-ESP32
- https://github.com/nkolban/esp32-snippets


I attach code that I use to test servos:

- `servo-tester.c` is the ESP32 program
- `servo-tester-client.py` is a Python 2.7 script that I run on my computer
- ESP32 is an access point and UDP socket server
- in each message I send 4 bytes (one 32-bit integer)


I use UDP sockets instead of TCP sockets because the latency is smaller. UDP doesn't guarantee that messages will arrive in the order they were sent, or that they will arrive at all, but it's OK for my use case. If you want more reliable (but slower) communication, or two-way communication, you should use TCP sockets.