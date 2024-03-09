
# HuskyLens Raspberry Pi Tutorial


# I. I2C Wiring Guide 

The primary protocol for communication between the HuskyLens and a Raspberry PI is I2C. This requires you to use the 4PIN connector to wrire ground, power, SDA, and SCL. To read more about how I2C works, please check out the following link:  https://en.wikipedia.org/wiki/I%C2%B2C

## Pin Outline

### [Raspberry Pi GPIO Pinout](https://pinout.xyz/pinout/i2c)

> ### I2C Wiring
>
> The 4 pin connector located on the bottom left has the following connections T, R , -, + (from left to right). Simply connect - and + to ground and 3.3-5.0V power respectively. Your T and R pins will connect to SDA and SCL pins on your Raspbery Pi. The blue R wire will connect to the SCL1 pin and the green T wire will connec to the SDA1, please refer the above picture where the SDA1 and SCL1 pins are outlined in red. 

##### Important Note

You must choose the protocol type and speed on the HuskyLens. Therefore, use the function to navigate to General Settings and then click Protocol. You can now use the function button again to choose I2C .

![Wiring](https://i.ibb.co/YydCcV4/101583380990-pic.jpg)

# II. Setting up the Raspberry PI 


On your Raspberry PI you must enable I2C in settings before being able to use it. Therefore open a terminal on your Raspberry PI and run the following commands

> 1) Run ```sudo raspi-config```
> 2) Use the down arrow to select 5 Interfacing Options
> 3) Arrow down to P5 I2C.
> 4) Select yes when it asks you to enable I2C
> 5) Also select yes if it asks about automatically loading the kernel module.
> 6) Use the right arrow to select the <Finish> button.
> 7) Select yes when it asks to reboot.
## Setting up in Virtual Enviroment (Recomended For Rasbery Pi 5 user)
> 1) After Reboot, run ```mkdir huskylens```
> 2) Run ```cd huskylens```
> 3) Run ```python -m env```
> 4) Run ```source env/bin/activate```
- The Action above will create a virtual environment
- All the codes will run in the virtual environment
- Save the coding file in the same path as the virtual environment
> 5) Now in the Virtual Environment Run ```pip install pypng```
> 6) Run ```pip install pyserial```
> 7) Run ```pip install SMBus2```
- This will install the dependency to the virtual environment.
- Run ```source env/bin/activate``` Before running the custom project


## Setting up in Global Environment
> 1) After reboot , run ```sudo apt-get install -y i2c-tools```
> 2) Run ```sudo apt-get install python-smbus```
> 3) Run ```sudo pip3 install pyserial```

# III. Coding Guide 

1) Download the Python Library <a href="/HUSKYLENS">here</a>
2) Run ```sudo i2cdetect -y 1```
    > a) This action is to determine the i2c address <br>
    > b) Please remember the address that pops up here, in my case it is 32. This is the I2C address for the HuskyLens
    If the above command returns an error please change to : ```sudo i2cdetct -y 0```

>```sh
>pi@raspberry: sudo i2cdetect -y 1
>0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
>00:          -- -- -- -- -- -- -- -- -- -- -- -- --
>10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
>20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
>30: -- -- 32 -- -- -- -- -- -- -- -- -- -- -- -- --
>40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
>50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
>60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
>70: -- -- -- -- -- -- -- --
>```
> - If there is no value return, Please check the physical conection. 
>
> 3) Place the huskylensPythonLibrary.py in your projects folder
> 4) In your python file import the library using
>
>```python 
> from huskylib import HuskyLensLibrary
>```

 ```
 5) Init the HuskyLens 
 ```python
 # replace the address value with your I2C address from before in 0x00 form
 hl= HuskyLensLibrary("I2C","",address=0x32)
 print(hl.knock())
 ```

6) Happy Coding !

7) For more information, reach me via email 
