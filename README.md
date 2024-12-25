# Read Ethercat-Master Device names
This small library acts as a sample project to show how to read Ethercat-Master names in TwinCAT. 

## Dependencies
It references ZCore library from Zeugwerk Framework. This can be easily installed via [Twinpack](https://github.com/Zeugwerk/Twinpack) library Package Manager.

## Usage
- instantiate function block
- call `Cyclic()` method on every PLC cycle
- start reading by calling method `DeviceNamesAsync('');`, leave AmsNetId empty to read from a local PLC
- Fetch result from VAR_INPUT arrays of the object

## Example
```st
PROGRAM MAIN
VAR
  GetDeviceData : GetDeviceData.GetDeviceData;
  Step : ZCore.Step(0, 50);
  Start : BOOL;
  EcatMasterCount : UINT;
  EcatName : ZCore.ZString;
  EcatAmsNetId : Tc2_System.T_AmsNetID;
END_VAR
----------------------------------
GetDeviceData.Cyclic();

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
      GetDeviceData.DeviceNamesAsync('');
    END_IF

    IF GetDeviceData.Done 
    THEN
      EcatMasterCount := GetDeviceData.EthercatMasterCount;
      EcatName := GetDeviceData.NameArray[0];
      EcatAmsNetId := GetDeviceData.NetIdArray[0];
      Step.SetNext(0);
    END_IF  
    
END_CASE
```
