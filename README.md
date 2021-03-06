rshfiq serves has hardware description of the RS-HFIQ from HobbyPCB to be used with quisk.
Meanwhile a hardware description for the FuncubePro+ dongle is available, too.

This package was tested with quisk-4.1.76 and hamlib 4 and python 3.9.

It contains two possible hardware descriptions: 

  * hardware_usbserial.py  
    This description requires the installation of the Python pyserial package. Using this descriptions quisk directly communicates with the rs-hfiq hardware via the serialport, normally /dev/ttyUSB0.
 If your system uses another port, you have to modify

    serialport.port = "/dev/ttyUSB0"
accordingly in the 'hardware_usbserial.py' file.
 

  * hardware_rshfiq_hamlib.py
    This description requires hamlib with python bindings. 
    This description may be adopted to other models supported by hamlib, for instance the funcube dongle.

  * hardware_funcube.py
    As the FuncubePro+ dongle has settings for LNA Mixer and IF gain, settings that are not known to the RS-HFIQ, here is an hardware description that support these settings.

 
If you have a running installation of quisk, untar or clone this repository into a directory of your choosing. Then start quisk and select config.

Select the 'Radios' tab, select 'Add a new radio'. I suggest to choose 'Softrock fixed'. After adding choose the tab of the newly created radio and switch to the Hardware tab.

If you wish to use the hardware_usbserial.py descripton, add it to the 'Hardware File Path'.

If you want to use the funcubePro+ add hardware_funcube.py to the 'Hardware File Path' and funcube_widget.py to the 'Widget File Path'. This adds the buttons for the gain controls. 

Then on the 'Sound' tab, configure the sound device settings according to your system configuration.

**Important:**

**RS-HFIQ **A given signals output must be turned on for the signal to be present. [See: Interface Commands](https://sites.google.com/site/rshfiqtransceiver/home/technical-data/interface-commands)

Generally a 4 ma drive seems like it works OK. This setting has to be done only once.
You can do this using the arduino ide or uncomment line 45 in hardware_usbserial.py


On my system I had to change the I/Q channels for I/Q Sample Input and Tx Output.

With some soundcards I got no sound on transmit. 
The solution was to use

plughw:x,y instead of the hw:x,y proposed by quisk.

<u>Example</u>:

quisk offers  alsa:USB Audio Device USB Audio (hw:3,0) , which I use for 'I/Q sample Input'.

With some soundcards I can use this setting for 'I/Q Tx Output', too. But with some cards and the StarTech card is one of them, I had to enter manually

plughw:3,0 

instead.

After stopping and starting everything worked flawless.

