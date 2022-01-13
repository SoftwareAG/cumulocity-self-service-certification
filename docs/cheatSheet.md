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

#### Smart Rest 2.0 Send
**Inventory**  
&emsp; [`100,createdDeviceName,deviceType`](https://cumulocity.com/guides/device-sdk/mqtt/#device-creation-100)  
&emsp; [`101,createdChildId,childName,childType`](https://cumulocity.com/guides/device-sdk/mqtt/#child-device-creation-101)  
&emsp; [`105 (Get children, reply: 106,child1,child2,…)`](https://cumulocity.com/guides/device-sdk/mqtt/#get-child-devices-105)  
&emsp; [`107,fragmenttoBeUninstalled1,fragment2,…`](https://cumulocity.com/guides/device-sdk/mqtt/#clear-devices-fragment-107)   
&emsp; [`110,serialNumber,hardwareModel,revision`](https://cumulocity.com/guides/device-sdk/mqtt/#configure-hardware-110)   
&emsp; [`111,IMEI,ICCID,IMSI,MCC,MNC,LAC,cellId`](https://cumulocity.com/guides/device-sdk/mqtt/#configure-mobile-111)   
&emsp; [`112,latitude,longitude,altitude,accuracy`](https://cumulocity.com/guides/device-sdk/mqtt/#configure-position-112)   
&emsp; [`113,"configProp1=val1\nprop2=val2\n…"`](https://cumulocity.com/guides/device-sdk/mqtt/#set-configuration-113)   
&emsp; [`114,supportedOperation1,operation2,…`](https://cumulocity.com/guides/device-sdk/mqtt/#set-supported-operations-114)   
&emsp; [`115,currentFirmwareName,version,url`](https://cumulocity.com/guides/device-sdk/mqtt/#set-firmware-115)   
&emsp; [`116,currentSoftwareName1,version1,url1,name2,…`](https://cumulocity.com/guides/device-sdk/mqtt/#set-software-list-116)   
&emsp; [`117,requiredInterval`](https://cumulocity.com/guides/device-sdk/mqtt/#set-required-availability-117)   
&emsp; [`118,supportedLog1,log2,...`](https://cumulocity.com/guides/device-sdk/mqtt/#set-supported-logs-118)   
&emsp; [`119,supportedConfiguration1,config2,...`](https://cumulocity.com/guides/device-sdk/mqtt/#set-supported-configurations-119)   
&emsp; [`120,configType,url,filename[,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#set-currently-installed-configuration-120)   
&emsp; [`121,profileExecuted,profileID`](https://cumulocity.com/guides/device-sdk/mqtt/#set-device-profile-that-is-being-applied-121)   

**Measurements**  
&emsp; [`200,fragment,series,value,unit[,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#create-custom-measurement-200)   
&emsp; [`210,rssi,ber[,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#create-signal-strength-measurement-210)  
&emsp; [`211,temperature[,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#create-temperature-measurement-211)  
&emsp; [`212,battery[,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#create-battery-measurement-212)  

**Events**  
&emsp; [`400,eventType,text[,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#create-basic-event-400)  
&emsp; [`401,latitude,longitude,altitude,accuracy[,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#create-location-update-event-401)  
&emsp; [`402,latitude,longitude,altitude,accuracy[,time] (incl. inv. update)`](https://cumulocity.com/guides/device-sdk/mqtt/#create-location-update-event-with-device-update-402)  
&emsp; [`407,eventType,fragmentToBeRemoved1,fragment2,...`](https://cumulocity.com/guides/device-sdk/mqtt/#clear-events-fragment-407)  

**Alarms**  
&emsp; [`301,criticalAlarmType[,text][,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#create-critical-alarm-301)  
&emsp; [`302,majorAlarmType[,text][,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#create-major-alarm-302)  
&emsp; [`303,minorAlarmType[,text][,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#create-minor-alarm-303)  
&emsp; [`304,warningAlarmType[,text][,time]`](https://cumulocity.com/guides/device-sdk/mqtt/#create-warning-alarm-304)  
&emsp; [`305,alarmType,newSeverity`](https://cumulocity.com/guides/device-sdk/mqtt/#update-severity-of-existing-alarm-305)  
&emsp; [`306,alarmTypeToBeCleared`](https://cumulocity.com/guides/device-sdk/mqtt/#clear-existing-alarm-306)  
&emsp; [`307,alarmType,fragmentToBeRemoved1,fragment2,`](https://cumulocity.com/guides/device-sdk/mqtt/#clear-alarms-fragment-307)  

**Operations**  
&emsp; [`500 (get pending)`](https://cumulocity.com/guides/device-sdk/mqtt/#get-pending-operations-500)  
&emsp; [`501,typeToSetToExecuting`](https://cumulocity.com/guides/device-sdk/mqtt/#set-operation-to-executing-501)  
&emsp; [`502,typeToSetToFailed,fialureReason`](https://cumulocity.com/guides/device-sdk/mqtt/#set-operation-to-failed-502)  
&emsp; [`503,typeToSetToSuccessful,parameters`](https://cumulocity.com/guides/device-sdk/mqtt/#set-operation-to-successful-503)  
&emsp; [`510,serial (restart)`](XXXXX)  
&emsp; [`511,serial,commandToExecute`](XXXXX)  
&emsp; [`513,serial,configurationText`](XXXXX)  
&emsp; [`515,serial,firmwareToBeInstalled,version,url`](XXXXX)  
&emsp; [`516,serial,softwareToBeInstalled1,version1,url1,sw2,ver2,url2, …`](XXXXX)  
&emsp; [`517,serial,measurementToBeSent`](XXXXX)  
&emsp; [`518,serial,relayStatusToBeSet [OPEN/CLOSED]`](XXXXX)  
&emsp; [`519,serial,relay1Status,relay2Status, …`](XXXXX)  
&emsp; [`520,serial (upload your current configuration)`](XXXXX)  
&emsp; [`521,serial,url (download configuration)`](XXXXX)  
&emsp; [`522,serial,logFileToBeSend,start,stop,searchText,maxLines`](XXXXX)  
&emsp; [`523,serial,communicationMode (SMS/IP)`](XXXXX)  
&emsp; [`524,serial,url,configType`](XXXXX)  
&emsp; [`525,serial,currentFirmwareName,version,url,dependency`](XXXXX)  
&emsp; [`526,serial,configType`](XXXXX)  
&emsp; [`527,serial,firmwareMarker,name,version,url,isPatch,dependency,softwareMarker,name,version,url,action,configurationMarker,url,type`](XXXXX)  
&emsp; [`528,serial,softwareToBeUpdated1,version1,url1,action1,sw2,ver2,url2,action2,.`](XXXXX)  
&emsp; [`530,serial,hostname,port,connectionKey`](XXXXX)  

#### Smart Rest 2.0 Response
**Inventory**  
&emsp; [`106,child1,child2,child3`](https://cumulocity.com/guides/device-sdk/mqtt/#get-children-of-device-106)  

**Operations**  
&emsp; [`510,serial (restart)`](https://cumulocity.com/guides/device-sdk/mqtt/#restart-510)  
&emsp; [`511,serial,commandToExecute`](https://cumulocity.com/guides/device-sdk/mqtt/#command-511)  
&emsp; [`513,serial,configurationText`](https://cumulocity.com/guides/device-sdk/mqtt/#configuration-513)  
&emsp; [`515,serial,firmwareToBeInstalled,version,url`](https://cumulocity.com/guides/device-sdk/mqtt/#firmware-515)  
&emsp; [`516,serial,softwareToBeInstalled1,version1,url1,sw2,ver2,url2, …`](https://cumulocity.com/guides/device-sdk/mqtt/#software-list-516)  
&emsp; [`517,serial,measurementToBeSent`](https://cumulocity.com/guides/device-sdk/mqtt/#measurement-request-operation-517)  
&emsp; [`518,serial,relayStatusToBeSet [OPEN/CLOSED]`](https://cumulocity.com/guides/device-sdk/mqtt/#relay-518)  
&emsp; [`519,serial,relay1Status,relay2Status, …`](https://cumulocity.com/guides/device-sdk/mqtt/#relayarray-519)  
&emsp; [`520,serial (upload your current configuration)`](https://cumulocity.com/guides/device-sdk/mqtt/#upload-configuration-file-520)  
&emsp; [`521,serial,url (download configuration)`](https://cumulocity.com/guides/device-sdk/mqtt/#download-configuration-file-521)  
&emsp; [`522,serial,logFileToBeSend,start,stop,searchText,maxLines`](https://cumulocity.com/guides/device-sdk/mqtt/#logfile-request-522)  
&emsp; [`523,serial,communicationMode (SMS/IP)`](https://cumulocity.com/guides/device-sdk/mqtt/#communication-mode-523)  
&emsp; [`524,serial,url,configType`](https://cumulocity.com/guides/device-sdk/mqtt/#download-configuration-file-with-type-524)  
&emsp; [`525,serial,currentFirmwareName,version,url,dependency`](https://cumulocity.com/guides/device-sdk/mqtt/#firmware-from-patch-525)  
&emsp; [`526,serial,configType`](https://cumulocity.com/guides/device-sdk/mqtt/#upload-configuration-file-with-type-526)  
&emsp; [`527,serial,firmwareMarker,name,version,url,isPatch,dependency,softwareMarker,name,version,url,action,configurationMarker,url,type`](https://cumulocity.com/guides/device-sdk/mqtt/#set-device-profiles-527)  
&emsp; [`528,serial,softwareToBeUpdated1,version1,url1,action1,sw2,ver2,url2,action2,.`](https://cumulocity.com/guides/device-sdk/mqtt/#update-software-528)  
&emsp; [`530,serial,hostname,port,connectionKey`](https://cumulocity.com/guides/device-sdk/mqtt/#cloud-remote-access-connect-530)  


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

