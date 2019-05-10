# iWine Objective-C SDK

### Get info

```objectivec
- (IWineInfo*) getiWineInfo:(NSString*) pin;
```

Returns IWineInfo object instance pointer with temperature, volume, color, shugar. If device unavaliable `EiWineErrorException` thrown. If incorrect pin `EiWineAuthException` thrown. If token is incorrect \(never taken\)  `EiWineErrorTokenException` thrown.

**Parameters:**

`pin` NSString parameter must be PIN code of IWine device taped on bottom.



## Set new temperature

```objectivec
- (NSString*) setIWineNewTemperature:(NSString*) pin newTemperature:(float) temp onProgress:(void (^)(float temp)) onprogress
onComplete:(void (^)(void)) oncomplete onError:(void (^)(NSString* errmsg)) onerror;;
```

Begin temperature change.

#### Parameters

`pin` NSString parameter must be PIN code of IWine device taped on bottom.

`newTemperature` float value in 0.0 - 100.0 interval.

`onProgress` pointer to callback function for the progress report. In paramter returned current temperature.

`onComplete` pointer to callback function for call after completion operation

`onError` pointer to function that called on any error. Error message returned in parameter. 

Returns pointer to NSString with operation token. 

## Start shake

```objectivec
-(NSString*) startIWineShake:(NSString*) pin onProgress:(void (^)(void)) onprogress
onComplete:(void (^)(void)) oncomplete onError:(void (^)(NSString* errmsg)) onerror;;
```

Start shaking.

#### Parameters

`pin` NSString parameter must be PIN code of IWine device taped on bottom.

`onProgress` pointer to callback function for the progress report. 

`onComplete` pointer to callback function for call after completion operation

`onError` pointer to function that called on any error. Error message returned in parameter. 

Returns pointer to NSString with operation token. 

## Stop operation

```text
- (int) stopIWineOperation:(NSString*) pin OperationToken:(NSString*) token;
```

Stop any operation started by `startIWineShake` or `setIWineNewTemperature` call.

#### Parameters

`pin` NSString parameter must be PIN code of IWine device taped on bottom.

`token`  pointer to NSString with token returned by  `startIWineShake` or `setIWineNewTemperature` call. 

