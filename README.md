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
  _deviceInfo : DeviceInfo.DeviceInfo;
  _slaveInfo : DeviceInfo.SlaveInfo;
  _step : ZCore.Step(0, 50);
  _start : BOOL;
  _ecatMasterCount : UINT;
  _ecatName : ZCore.ZString;
  _ecatAmsNetId : Tc2_System.T_AmsNetID;
END_VAR
----------------------------------
_deviceInfo.Cyclic();
_slaveInfo.Cyclic();

CASE _step.Index OF
  0:
    IF _start 
    THEN 
      _start := FALSE;
      _step.SetNext(10);
    END_IF
    
  10:
    IF _step.OnEntry()
    THEN
      _deviceInfo.ReadDeviceNamesAsync('');
    END_IF

    IF _deviceInfo.Done 
    THEN
      _ecatMasterCount := _deviceInfo.EthercatMasterCount;
      _ecatName := _deviceInfo.NameArray[0];
      _ecatAmsNetId := _deviceInfo.NetIdArray[0];
      _step.SetNext(20);
    END_IF  
    
  20:
    IF _step.OnEntry()
    THEN
      _slaveInfo.ReadSlaveNamesAsync('', _deviceInfo.DeviceIdArray[0]);
    END_IF
    
    IF _slaveInfo.Done
    THEN
      _step.SetNext(0);
    END_IF
    
END_CASE
```
    
END_CASE
```
