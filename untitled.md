# iWine Java SDK

### **Constants used to determine operation progress.**

`const int IWINE_INPROGRESS=0;`

This value returned while process of changing temperature or shaking. 

`const int IWINE_COMPLETE=1;`

This value returned while process of changing temperature or shaking. 

`const int IWINE_ERROR=2;`

This value returned while process of changing temperature or shaking. 

### **Get iWine info**

`IWineInfo getiWineInfo(String pin);`

Returns IWineInfo object instance with temperature, volume, color, shugar. If device unavaliable `EiWineErrorException` thrown. If incorrect pin `EiWineAuthException` thrown. If token is incorrect \(never taken\)  `EiWineErrorTokenException` thrown.

**Parameters:**

`pin` String parameter must be PIN code of IWine device taped on bottom.



### Begin temperature change. 

`String setiWineNewTemperature(String pin,float newtemp);`

Returns String token that indentifies started process. Token used by `isiWineTempChangeCompleted` to check progress. If device unavaliable `EiWineErrorException` thrown. If incorrect pin `EiWineAuthException` thrown. 

#### Parameters.

`pin` device pin code. see get Info.

`newtemp` float value in 0.0 100.0 interval. 

### Start shake

`String startiWineShake(String pin);`

Starts shaking. Returns token that indentifies started process. Token used by `isiWineShakingComplete` to check progress. 

If device unavaliable `EiWineErrorException` thrown. If incorrect pin `EiWineAuthException` thrown. 

#### Parameters.

 `pin` device pin code. see get Info.

### Check temperature change progress

`int isiWineTempChangeCompleted(String pin,string token);`

Returns one of the `IWINE_INPROGRESS, IWINE_COMPLETE,IWINE_ERROR` constants. 

If device unavaliable `EiWineErrorException` thrown. If incorrect pin `EiWineAuthException` thrown. If token is incorrect \(never taken\)  `EiWineErrorTokenException` thrown.

#### Parameters.

`pin` device pin code. see get Info.

`token` string token returned by . `setiWineNewTemperature` call.

### Check shaking progress.

`int isiWineShakingComplete(String pin,string token);`

Returns one of the `IWINE_INPROGRESS, IWINE_COMPLETE,IWINE_ERROR` constants. 

If device unavaliable `EiWineErrorException` thrown. If incorrect pin `EiWineAuthException` thrown. If token is incorrect \(never taken\)  `EiWineErrorTokenException` thrown.

#### Parameters.

`pin` device pin code. see get Info.

`token` string token returned by . `startiWineShake` call.

### Stop operation

`bool stopiWineOperation(String pin,String token);`

Stop runned by `setiWineNewTemperature` or `startiWineShake` operation. If device unavaliable `EiWineErrorException` thrown. If incorrect pin `EiWineAuthException` thrown. If token is incorrect \(never taken\)  `EiWineErrorTokenException` thrown. 

Returns `true` of really stopped operation  or `false` if process already completed.

