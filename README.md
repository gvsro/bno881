# bno881
A quest for bluetooth audio retrofit

![cdc pic](https://raw.githubusercontent.com/gvsro/bno881/master/images/cdc.jpg)


After a long night(3h+) trying to get this unit of a friends car without proper tools so he could install a crap head-unit just because 'it has bluetooth', I found some spare time to get this project up and running.

The plan:
  1. Plant an arduino cdc emulator into this unit. [https://github.com/tomaskovacik/vwcdavr]
  2. Feed a bluetooth audio into the cdc analog audio input.
  3. Smash the crap head-unit and light it on fire.
  4. Profit.
  
 First problem: 
 
 This unit is wired in such a way that CAN (bus) or K-Line (or both) is fed into it. The car 'knows' the unit and the unit 'knows' the car. If you take it out and just apply power to it this will happen.

![cdc pic](https://raw.githubusercontent.com/gvsro/bno881/master/images/what%20code.jpg)
 
 3 wrong codes later.
 ![cdc pic](https://raw.githubusercontent.com/gvsro/bno881/master/images/safe.jpg)
 
 emm.. 
 ![wait what](https://s.newsweek.com/sites/www.newsweek.com/files/styles/full/public/2018/02/28/rick-and-morty-rest-and-ricklaxation.jpg)
 
 Ok, plan B:
  1. Find an eeprom reader/writer or build one myself.
  2. Rewrite eeprom with a dump found on the interweb, and pray. Else, try to get the code out of the actual dump.
  3. Continue plan A.
  
  After searching for a programmer(that I built in the past) with no luck, I realized that the ods were against me. I had to build yet another one. Hurray..
  
  Hardware:
  ![arduino eeprom](http://www.learningaboutelectronics.com/images/24LC256-EEPROM-circuit-with-an-arduino.png)
  
  ![bno811-i2c](https://www.elforum.info/uploads/monthly_11_2017/post-176905-0-39489000-1510146550.jpg)
  
  Software (i2c scanner, i2c eeprom read, i2c eeprom write):
  
  I2c scanner:
  ![umm](https://raw.githubusercontent.com/gvsro/bno881/master/images/eeprom.png)
  ![what](https://i.kym-cdn.com/photos/images/newsfeed/000/993/875/084.png)
  
  So this is the main i2c line. My eeprom is inside the processor (FIS), the internet say I should read the eeprom as a 24c32. 
  The 24c32 has a minimum address of 0x50, so that's my address.
  
  After uploading the eeprom read sketch into the arduino, saving the file (via the log method within Tera Term), and viewing it in a hex editor, I confirmed that this is my eeprom. I double dumped the eeprom just to be safe aaaaand:
  
  ![que]()
  
  Great. My files are different from the first read. This is gonna be a long night.
  
  
