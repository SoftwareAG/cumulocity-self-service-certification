## Cumulocity MQTT Cheat Sheet 
Topics

: PUBLISH s/us
   `Send built-in message`

: PUBLISH s/us/5678
   `Send built-in message to child "5678"`

: PUBLISH s/ud
   `Send message using default template (myDevice_10)`
  : PUBLISH s/ud/5678
   `Same as above, but to child "5678"`
  : PUBLISH s/uc/myCommon_10
   `Send message using myCommon_10 template`
  : PUBLISH s/uc/myCommon_10/5678
   `Same as above, but to child "5678"`
  : SUBSCRIBE s/ds
   `Receive built-in commands`
  : SUBSCRIBE s/dd
   `Receive commands using default template (myDevice_10)`
  : SUBSCRIBE s/dc/myCommon_10
   `Receive commands using myCommon_10 template`
  : SUBSCRIBE s/e
   `Receive error messages`

Connection
: CONNECT 1234:myDevice_10 acme/device_1234
 `Connect device with serial "1234" and default template "myDevice_10" to tenant "acme" and user "device_1234". `

: Topic format
 `<protocol>/<direction><type>[/<template>][/<child id>]`
: protocol
 `s = standard`
 `t = transient`
: direction
 `u = upstream (from device)`
 `d = downstream (to device)`
 `e = error`
: type
 `s = static (built-in)`
 `c = custom (device-defined)`
 `d = default (defined in connect)`
 `t = template`
 `cr = credentials`
: template
 `name of the template defined in c8y`
: child id
 `managed object id of the child device`

Device registration
: order to register a device
 start device registration on the tenant
 `CONNECT 1234 management/devicebootstrap` using botstrap credentials
 `SUBSCRIBE s/dcr` to get the device credentials
 device need to be accepted from UI within the tenant
 `PUBLISH s/ucr`
 `PUBLISH s/ucr`
…
 Response
 `70,tenant,username,password`

 Template registration
: PUBLISH s/ut/myCommon_10
 `10,999,POST,MEASUREMENT,,c8y_MyMeasurement,,c8y_MyMeasurement.M.value,NUMBER, …`
 `10,msgId,api,method,response,type,time,custom1.path,custom1.type,custom1.value`

 Smart Rest 2.0
: Inventory
 `100,createdDeviceName,deviceType`
 `101,createdChildId,childName,childType`
 `105 (Get children, reply: 106,child1,child2,…)`
 `107,fragmenttoBeUninstalled1,fragment2,…`
 `110,serialNumber,hardwareModel,revision`
 `111,IMEI,ICCID,IMSI,MCC,MNC,LAC,cellId`
 `112,latitude,longitude,altitude,accuracy`
 `113,"configProp1=val1\nprop2=val2\n…"`
 `114,supportedOperation1,operation2,…`
 `115,currentFirmwareName,version,url`
 `116,currentSoftwareName1,version1,url1,name2,…`
 `117,requiredInterval `
 `118,supportedLog1,log2,...`
 `119,supportedConfiguration1,config2,...`
 `120,configType,url,filename[,time]`
 `121,profileExecuted,profileID`

: Measurements
 `200,fragment,series,value,unit[,time]`
 `210,rssi,ber[,time]`
 `211,temperature[,time]`
 `212,battery[,time] `

: Events
 `400,eventType,text[,time]`
 `401,latitude,longitude,altitude,accuracy[,time]`
 `402,latitude,longitude,altitude,accuracy[,time] (incl. inv. update)`
 `407,eventType,fragmentToBeRemoved1,fragment2,...`

: Alarms
 `301,criticalAlarmType[,text][,time]`
 `302,majorAlarmType[,text][,time]`
 `303,minorAlarmType[,text][,time]`
 `304,warningAlarmType[,text][,time]`
 `305,alarmType,newSeverity`
 `306,alarmTypeToBeCleared`
 `307,alarmType,fragmentToBeRemoved1,fragment2,`

: Operations
 `500 (get pending)`
 `501,typeToSetToExecuting`
 `502,typeToSetToFailed,fialureReason`
 `503,typeToSetToSuccessful,parameters`
 `510,serial (restart)`
 `511,serial,commandToExecute`
 `513,serial,configurationText`
 `515,serial,firmwareToBeInstalled,version,url`
 `516,serial,softwareToBeInstalled1,version1,url1,sw2,ver2,url2, …`
 `517,serial,measurementToBeSent`
 `518,serial,relayStatusToBeSet [OPEN/CLOSED]`
 `519,serial,relay1Status,relay2Status, …`
 `520,serial (upload your current configuration)`
 `521,serial,url (download configuration)`
 `522,serial,logFileToBeSend,start,stop,searchText,maxLines`
 `523,serial,communicationMode (SMS/IP)`
 `524,serial,url,configType`
 `525,serial,currentFirmwareName,version,url,dependency`
 `526,serial,configType`
 `527,serial,firmwareMarker,name,version,url,isPatch,dependency,softwareMarker,name,version,url,action,configurationMarker,url,type`
 `528,serial,softwareToBeUpdated1,version1,url1,action1,sw2,ver2,url2,action2,.`
 `530,serial,hostname,port,connectionKey`

### JSON via MQTT Cheat Sheet
Topics
: PUBLISH event/events/create
`create an event message`
: PUBLISH event/events/createBulk
`create many event messages`
: PUBLISH event/events/update/<event_id>
`update an event message`
: PUBLISH event/events/delete/<event_id>
`delete an event message`
: PUBLISH alarm/alarms/create
`create an alarm`
: PUBLISH alarm/alarms/createBulk
`create many alarms`
: PUBLISH alarm/alarms/update/<alarm_id>
`update an alarm`
: PUBLISH measurement/measurements/create
`create a measurement`
: PUBLISH measurement/measurements/createBulk
`create many measurements`
: PUBLISH measurement/measurements/delete/<measurement_id>
`delete a measurement`
: PUBLISH inventory/managedObjects/create
`create a managedObject`
: PUBLISH inventory/managedObjects/update/<managedObject_id>
`update a managedObject`
: PUBLISH inventory/childOperations/create
`create a child operation`
: SUBSCRIBE error
`Receive error messages`
: SUBSCRIBE notification/operations
`Receive notifications of newly created operations`

Topics structure 
: To publish messages
`<api>/<resource>/<action>/<id>`
: To publish messages in transient mode:
`t/<api>/<resource>/<action>/<id>`
: To publish messages in quiescent mode
`q/<api>/<resource>/<action>/<id>`
: To publish messages in CEP mode
`c/<api>/<resource>/<action>/<id>`

Processing mode
: PERSISTENT (default)
`All updates will be send both to the Cumulocity IoT database and to real-time processing.`
: TRANSIENT
`Updates will be sent only to real-time processing. As part of real-time processing, the user can decide case by case through scripts whether updates should be stored to the database or not.`
: QUIESCENT
`The QUIESCENT processing mode behaves like the PERSISTENT processing mode with the exception that no real-time notifications will be sent.`
: CEP
`With the CEP processing mode, requests will only be processed by Apama.`

