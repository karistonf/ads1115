# ADS1115

Library for using the ADS1115 from TI with the STM32 I2C interface


## Settings

The ADS1115 supports two types of measurements: single-ended,
where AIN0, AIN1, AIN2 or AIN3 are referenced to GND, 
and differential, where the voltage difference between two channels is measured. 

### Address

| ADDR | Command |
| -- | -- |
| Address pin is connected on GND | ADS1115_ADDRESS 0x48 |
| Address pin is connected on VCC | ADS1115_ADDRESS 0x49 |
| Address pin is connected on SDA | ADS1115_ADDRESS 0x50 |
| Address pin is connected on SCL | ADS1115_ADDRESS 0x51 |

exemple:

```C 
//ADS1115 ADDR pin connected on GND

#define ADS1115_ADDRESS 0x48   //GND
//#define ADS1115_ADDRESS 0x49 //VCC
//#define ADS1115_ADDRESS 0x50 //SDA
//#define ADS1115_ADDRESS 0x51 //SCL
```

### Mutex setting to Single-ended measurements

| Ports        | Command             |
| ------------ | ------------------- |
| AN0 with GND | CONFIG_MUX_AIN0_GND | 
| AN1 with GND | CONFIG_MUX_AIN1_GND |
| AN2 with GND | CONFIG_MUX_AIN2_GND |
| AN3 with GND | CONFIG_MUX_AIN3_GND |

### Mutex setting to Differential measurements

| Ports        | Command             |
| ------------ | ------------------- |
| AN0 with AN1 | CONFIG_MUX_AIN0_AIN1|
| AN2 with AN3 | CONFIG_MUX_AIN2_AIN3|

### Programmable gain amplifier configuration (PGA)

Is possible set the internal gain using the PGA

| Gain         | Command           |
| ------------ | ----------------- |
| 2/3          | CONFIG_PGA_6_144V |                
| 1            | CONFIG_PGA_4_096V |               
| 2            | CONFIG_PGA_2_048V |               
| 4            | CONFIG_PGA_1_024V |               
| 8            | CONFIG_PGA_0_512V |               
| 16           | CONFIG_PGA_0_256V | 

| Mode |  Command |
| - | - |
|   | CONFIG_MODE_CONTINUOUS  |
|   | CONFIG_MODE_SINGLE_SHOT |

### Data rate
SPS -> samples per second

| Data rate (samples per second) | Command |
| --- | -------------------- |
| 8   | *Not implemented yet*|
| 16  | *Not implemented yet*|
| 32  | *Not implemented yet*|
| 64  | *Not implemented yet*|
| 128 | CONFIG_DR_128SPS |
| 250 | CONFIG_DR_250SPS |
| 475 | CONFIG_DR_475SPS |
| 860 | CONFIG_DR_860SPS |

```C
configureADS1115(CONFIG_MUX_AIN2_GND,
                 CONFIG_PGA_0_512V,
                 CONFIG_DR_128SPS,
                 CONFIG_MODE_CONTINUOUS);
```