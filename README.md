# Read Ethercat-Master Device names
This small library acts as a sample project to show how to read Ethercat-Master names in TwinCAT. 

## Dependencies
It references ZCore library from Zeugwerk Framework. This can be easily installed via [Twinpack](https://github.com/Zeugwerk/Twinpack) library Package Manager.

## Usage
- instantiate `GetDeviceData` function block
- call `Cyclic()` method on every PLC cycle
- start reading by calling method `DeviceNamesAsync('');`, leave AmsNetId empty to read from a local PLC
- Fetch result from VAR_INPUT arrays of the object

![deviceinfo](https://github.com/user-attachments/assets/e65c1735-6ff5-40d3-92db-5523b9fee53a)

## Example
```st
PROGRAM MAIN
VAR
  DeviceInfo : DeviceInfo.DeviceInfo;
  SlaveInfo : DeviceInfo.SlaveInfo;
  Step : ZCore.Step(0, 50);
  Start : BOOL;
  EcatMasterCount : UINT;
  EcatName : ZCore.ZString;
  EcatAmsNetId : Tc2_System.T_AmsNetID;
END_VAR
----------------------------------
DeviceInfo.Cyclic();
SlaveInfo.Cyclic();

CASE Step.Index OF
  0:
    IF Start 
    THEN 
      Start := FALSE;
      Step.SetNext(10);
		END_IF
    
  10:
    IF Step.OnEntry()
    THEN
      DeviceInfo.DeviceNamesAsync('');
    END_IF

    IF DeviceInfo.Done 
    THEN
      EcatMasterCount := DeviceInfo.EthercatMasterCount;
      EcatName := DeviceInfo.NameArray[0];
      EcatAmsNetId := DeviceInfo.NetIdArray[0];
      Step.SetNext(20);
    END_IF  
    
  20:
    IF Step.OnEntry()
    THEN
      SlaveInfo.SlaveNamesAsync('', DeviceInfo.DeviceIdArray[0]);
    END_IF
    
    IF SlaveInfo.Done
    THEN
      Step.SetNext(0);
		END_IF
    
END_CASE
```
