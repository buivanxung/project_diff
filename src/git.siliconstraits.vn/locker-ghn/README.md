# LOCKER - Station Server

* This repo is a part of *Locker System*, checkout all related repo at here [locker-ghn](https://git.siliconstraits.vn/locker-ghn).
* Run on Raspbery Pi 3 or Mini PC (intel chipset) use Linux OS.
* I create project with Backend and Frontend in same repo.

## Getting Started

Nothing to share!.

### Prerequisites

* Golang v1.8.2 or lastest
* Linux OS (Raspbian or Ubuntu)
* Backend Framework
  * Checkout this [labstack/echo](https://github.com/labstack/echo)
  * Structure [Restful API](https://medium.com/@kyawmyintthein/building-golang-restful-api-with-echo-framework-1-422abc78e3a7)

---

### Installing

A step by step series of examples that tell you have to get a development env running

Say what the step will be


### Installing driver
If you use a chip serial to uart such as CH340, CP1202, PL2303, then you have install driver for OS. 
* Program running and installing driver CH340 or CH341 in flatform Ubuntu, Raspberry and Linux OS.

* You dowload file git, open folder and run command
```sh
$ ./ch341-driver.sh
```
or
```sh
$ sudo ./ch341-driver.sh
```
Note:
* Chip producted by China
* Link information driver  [Link] (http://www.wch.cn/download/CH341SER_LINUX_ZIP.html)

### Persistant names usb to serial device
You can check usb serial using command
```
lsusb
```
*Output command*: Inportant ID **8087:0a2a**. *It is idVendor and idProduct*
```
Bus 001 Device 005: ID 8087:0a2a Intel Corp.
```
Using command show *ATTRS {serial}*:
```sh
udevadm info -a -n /dev/ttyUSB* | grep '{serial}' | head -n1
```
*Example out command*:
```
ATTRS{serial}=="AL00FNEH"
```
Created a file and add put the following line 
```sh
$ sudo nano /etc/udev/rules.d/99-usb-serial.rules
```
Add Folowing:
```
SUBSYSTEM=="tty", ATTRS{serial}=="0000:00:15.0", SYMLINK+="ttyLocker"
SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="A6008isP",  SYMLINK+="ttyLocker"
SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="A7004IXj",  SYMLINK+="ttyLocker"
SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="FTDIF46B",  SYMLINK+="ttyLocker"
```
After Reload usb device
```
$ sudo udevadm trigger
```
You can check again usb using command:
```sh
ls /dev/
```

### Run permission connection hardware 

Using *vim* or *nano* .Open file *./bashrc* and put the following line 
```
sudo chmod 755 /dev/input/event0
sudo chmod 755 /dev/input/event2
sudo chmod a+rw /dev/ttyUSB0
sudo chmod a+rw /dev/ttyUSB1
sudo chmod a+rw /dev/ttyS0
sudo chmod a+rw /dev/ttyACM0
```


```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Viet Trinh** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
