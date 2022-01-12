## Cumulocity MQTT Cheat Sheet 
**Topics**  
PUBLISH s/us  
&emsp;  `Send built-in message`  
PUBLISH s/us/5678  
&emsp; `Send built-in message to child "5678"`  
PUBLISH s/ud  
&emsp; `Send message using default template (myDevice_10)`  
PUBLISH s/ud/5678  
&emsp; `Same as above, but to child "5678"`  
PUBLISH s/uc/myCommon_10  
&emsp; `Send message using myCommon_10 template`  
PUBLISH s/uc/myCommon_10/5678  
&emsp; `Same as above, but to child "5678"`  
SUBSCRIBE s/ds  
&emsp; `Receive built-in commands`  
SUBSCRIBE s/dd  
&emsp; `Receive commands using default template (myDevice_10)`  
SUBSCRIBE s/dc/myCommon_10  
&emsp; `Receive commands using myCommon_10 template`  
SUBSCRIBE s/e  
&emsp; `Receive error messages`  

**Connection**  
CONNECT 1234:myDevice_10 acme/device_1234  
&emsp; `Connect device with serial "1234" and default template "myDevice_10" to tenant "acme" and user "device_1234". `  

**Topic format**  
&emsp; `<protocol>/<direction><type>[/<template>][/<child id>]`  
**protocol**  
&emsp; `s = standard`  
&emsp; `t = transient`  
**direction**  
&emsp; `u = upstream (from device)`  
&emsp; `d = downstream (to device)`  
&emsp; `e = error`  
**type**  
&emsp; `s = static (built-in)`  
&emsp; `c = custom (device-defined)`  
&emsp; `d = default (defined in connect)`  
&emsp; `t = template`  
&emsp; `cr = credentials`  
**template**  
&emsp; `name of the template defined in c8y`  
**child id**  
&emsp; `managed object id of the child device`  

**Device registration**  
1. order to register a device  
2. start device registration on the tenant  
3. `CONNECT 1234 management/deviceboostrap` using botstrap credentials  
4. `SUBSCRIBE s/dcr` to get the device credentials  
5. device need to be accepted from UI within the tenant  
6. `PUBLISH s/ucr`  
7. `PUBLISH s/ucr`  
8. …
9. Response  
10. `70,tenant,username,password`  

**Template registration**  
PUBLISH s/ut/myCommon_10  
&emsp; `10,999,POST,MEASUREMENT,,c8y_MyMeasurement,,c8y_MyMeasurement.M.value,NUMBER, …`  
&emsp; `10,msgId,api,method,response,type,time,custom1.path,custom1.type,custom1.value`  

#### Smart Rest 2.0
**Inventory**  
&emsp; `100,createdDeviceName,deviceType`  
&emsp; `101,createdChildId,childName,childType`  
&emsp; `105 (Get children, reply: 106,child1,child2,…)`  
&emsp; `107,fragmenttoBeUninstalled1,fragment2,…`  
&emsp; `110,serialNumber,hardwareModel,revision`  
&emsp; `111,IMEI,ICCID,IMSI,MCC,MNC,LAC,cellId`  
&emsp; `112,latitude,longitude,altitude,accuracy`  
&emsp; `113,"configProp1=val1\nprop2=val2\n…"`  
&emsp; `114,supportedOperation1,operation2,…`  
&emsp; `115,currentFirmwareName,version,url`  
&emsp; `116,currentSoftwareName1,version1,url1,name2,…`  
&emsp; `117,requiredInterval&emsp; `  
&emsp; `118,supportedLog1,log2,...`  
&emsp; `119,supportedConfiguration1,config2,...`  
&emsp; `120,configType,url,filename[,time]`  
&emsp; `121,profileExecuted,profileID`  

**Measurements**  
&emsp; `200,fragment,series,value,unit[,time]`  
&emsp; `210,rssi,ber[,time]`  
&emsp; `211,temperature[,time]`  
&emsp; `212,battery[,time]&emsp; `  

**Events**  
&emsp; `400,eventType,text[,time]`  
&emsp; `401,latitude,longitude,altitude,accuracy[,time]`  
&emsp; `402,latitude,longitude,altitude,accuracy[,time] (incl. inv. update)`  
&emsp; `407,eventType,fragmentToBeRemoved1,fragment2,...`  

**Alarms**  
&emsp; `301,criticalAlarmType[,text][,time]`  
&emsp; `302,majorAlarmType[,text][,time]`  
&emsp; `303,minorAlarmType[,text][,time]`  
&emsp; `304,warningAlarmType[,text][,time]`  
&emsp; `305,alarmType,newSeverity`  
&emsp; `306,alarmTypeToBeCleared`  
&emsp; `307,alarmType,fragmentToBeRemoved1,fragment2,`  

**Operations**  
&emsp; `500 (get pending)`  
&emsp; `501,typeToSetToExecuting`  
&emsp; `502,typeToSetToFailed,fialureReason`  
&emsp; `503,typeToSetToSuccessful,parameters`  
&emsp; `510,serial (restart)`  
&emsp; `511,serial,commandToExecute`  
&emsp; `513,serial,configurationText`  
&emsp; `515,serial,firmwareToBeInstalled,version,url`  
&emsp; `516,serial,softwareToBeInstalled1,version1,url1,sw2,ver2,url2, …`  
&emsp; `517,serial,measurementToBeSent`  
&emsp; `518,serial,relayStatusToBeSet [OPEN/CLOSED]`  
&emsp; `519,serial,relay1Status,relay2Status, …`  
&emsp; `520,serial (upload your current configuration)`  
&emsp; `521,serial,url (download configuration)`  
&emsp; `522,serial,logFileToBeSend,start,stop,searchText,maxLines`  
&emsp; `523,serial,communicationMode (SMS/IP)`  
&emsp; `524,serial,url,configType`  
&emsp; `525,serial,currentFirmwareName,version,url,dependency`  
&emsp; `526,serial,configType`  
&emsp; `527,serial,firmwareMarker,name,version,url,isPatch,dependency,softwareMarker,name,version,url,action,configurationMarker,url,type`  
&emsp; `528,serial,softwareToBeUpdated1,version1,url1,action1,sw2,ver2,url2,action2,.`  
&emsp; `530,serial,hostname,port,connectionKey`  

### JSON via MQTT Cheat Sheet
**Topics**  
PUBLISH event/events/create  
&emsp; `create an event message`  
PUBLISH event/events/createBulk  
&emsp; `create many event messages`  
PUBLISH event/events/update/<event_id>  
&emsp; `update an event message`  
PUBLISH event/events/delete/<event_id>  
&emsp; `delete an event message`  
PUBLISH alarm/alarms/create  
&emsp; `create an alarm`  
PUBLISH alarm/alarms/createBulk  
&emsp; `create many alarms`  
PUBLISH alarm/alarms/update/<alarm_id>  
&emsp; `update an alarm`  
PUBLISH measurement/measurements/create  
&emsp; `create a measurement`  
PUBLISH measurement/measurements/createBulk  
&emsp; `create many measurements`  
PUBLISH measurement/measurements/delete/<measurement_id>  
&emsp; `delete a measurement`  
PUBLISH inventory/managedObjects/create  
&emsp; `create a managedObject`  
PUBLISH inventory/managedObjects/update/<managedObject_id>  
&emsp; `update a managedObject`  
PUBLISH inventory/childOperations/create  
&emsp; `create a child operation`  
SUBSCRIBE error  
&emsp; `Receive error messages`  
SUBSCRIBE notification/operations  
&emsp; `Receive notifications of newly created operations`  

**Topics structure**  
To publish messages  
&emsp; `<api>/<resource>/<action>/<id>`  
To publish messages in transient mode:  
&emsp; `t/<api>/<resource>/<action>/<id>`  
To publish messages in quiescent mode  
&emsp; `q/<api>/<resource>/<action>/<id>`  
To publish messages in CEP mode  
&emsp; `c/<api>/<resource>/<action>/<id>`  

**Processing mode**  
PERSISTENT (default)  
&emsp; `All updates will be send both to the Cumulocity IoT database and to real-time processing.`  
TRANSIENT  
&emsp; `Updates will be sent only to real-time processing. As part of real-time processing, the user can decide case by case through scripts whether updates should be stored to the database or not.`  
QUIESCENT  
&emsp; `The QUIESCENT processing mode behaves like the PERSISTENT processing mode with the exception that no real-time notifications will be sent.`  
CEP  
&emsp; `With the CEP processing mode, requests will only be processed by Apama.`  

