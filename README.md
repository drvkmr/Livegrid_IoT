1. Connect everything together as shown in the "Connection key.jpeg". AC connection should be the last thing to plug in.
2. Connect a keyboard and mouse to the Pi and plug in the AC cable. Use this to connect it to wifi then - (https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md)
3. Alternatively you can also set up a headless SSH (https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)
4. Wi-Fi is very stable. But if you want to use ethernet, you will need to purchase a USB-Ethernet Adapter - (https://elinux.org/RPi_USB_Ethernet_adapters)
5. To test the matrix independently of BLE component, navigate to ./matrix/examples-api-use. And run this command - "sudo ./demo -D0 --led-rows=32 --led-cols=64 --led-slowdown-gpio=2 --led-gpio-mapping=adafruit-hat-pwm"
6. You can navigate to "https://github.com/hzeller/rpi-rgb-led-matrix" or just look at the readme.md in matrix to see what other demos can be run and how to build the files if needed. Just add the environment variables "--led-rows=32 --led-cols=64 --led-slowdown-gpio=2 --led-gpio-mapping=adafruit-hat-pwm" at the end of the command so the code knows the specifications of the panel.


Basic structure of Docker -
1. ble and matrix are 2 separate independent docker folders. Check the Dockerfiles within each to see how they are built.
2. They can be built independent to each other. They might not function properly because they use data from each other.
3. Navigate to the folder and use "docker build ." to build image and "docker run 'image hash' --privileged" to run them.
4. Image hash here is the hash generated on a succesful image build.
5. docker-compose.yml is the high level integration file. Run "docker-compose up" in the parent directory to run it.
6. The ble image is showing errors because of the bluetooth interfering with Wi-Fi. The pi can disconnect from Wi-Fi sometimes when the ble image is run.
7. If that happens the Pi will need to be force-restarted.