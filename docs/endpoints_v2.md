# Endpoints provided by the Open API python microservice
** Release 2.0**


## Products
Get an existing product by a product ID
GET `{{baseUrl}}/products/{product_id}`  [GET product](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0NzU-get-product)

Get all products for a particular tenant/vendor
GET `{{baseUrl}}/products/`  [GET products](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mjc5OTAxNjU-get-products)

Update an existing product
PUT `{{baseUrl}}/products/{product_id}`  [UPDATE product](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0NzY-update-product)

Create a new product providing a partial product managed object
POST `{{baseUrl}}/products/`  [CREATE product](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0NzQ-create-product)

Delete an existing product
DELETE `{{baseUrl}}/products/{product_id}`  [DELETE product](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0Nzc-delete-product)

---

## Testsuites
Get latest testSuite
GET `{{baseUrl}}/testsuites/latest`  [GET latest testSuite](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0NzE-get-latest-test-suite)

Get a testSuite by ID
GET `{{baseUrl}}/testsuites/{testsuite_id}`  [GET testSuite by ID](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0NzI-get-test-suite-by-id)

---

## Testruns


Get a testrun for a product by testrun ID
GET `{{baseUrl}}/testruns/{testrun_id}`  [GET testrun](https://softwareag.stoplight.io/docs/gateway-certification/b3A6MzgxMzEwNDc-get-testrun)

Get all testruns
GET `{{baseUrl}}/testruns/`  [Get testruns](https://softwareag.stoplight.io/docs/gateway-certification/b3A6MzgxMzEwNDU-get-testruns)

Udate an existing testrun
PUT `{{baseUrl}}/testruns/{testrun_id}`  [UPDATE testrun](https://softwareag.stoplight.io/docs/gateway-certification/b3A6MzgxMzEwNDg-update-testrun)

Create a testrun
POST `{{baseUrl}}/testruns/`    [CREATE testrun](https://softwareag.stoplight.io/docs/gateway-certification/b3A6MzgxMzEwNDY-create-testrun)

delete an existing testrun
DELETE `{{baseUrl}}/testruns/{testrun_id}`    [DELETE testrun](https://softwareag.stoplight.io/docs/gateway-certification/b3A6MzgxMzEwNDk-delete-testrun)

Starts the execution of the device certification
GET `{{baseUrl}}/testruns/{testrun_id}/certify`  [GET testrun certify](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0ODM-get-testrun-certify)


---

## Testcertificates

Get certificate by id
GET `{{baseUrl}}/certificates/{certificate_id}`  [GET certificate](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc1ODYxNjU-get-certificate)

Create a certificate managed object
POST `{{baseUrl}}/certificates/`  [CREATE  certificate](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0ODU-create-certificate)

Delete certificate by id
DELETE `{{baseUrl}}/certificates/{certificate_id}`  [DELETE certificate](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc1ODYxNjY-delete-certificate)

---

## Document

Get one PDF document of a certified device to download the file
GET `{{baseUrl}}/document/{document_id}`  [GET document](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0ODg-get-document)


---

# Endpoints that can use DPP

Provides all necessary certification information to the devicepartnerportal DPP.

---
## Search for Productname and Vendor

should search for Productname and Vendor as output we expect 0 or 1 valid Product to show the certification Logo

### Request

**GET** `{{url}}/inventory/managedObjects?pageSize=1&query=$filter=(type eq 'c8y_certification_testCertificate' and product.productName eq '{{product_name}}' and product.vendorName eq '{{vendor_name}}' and certificate.status.code eq 'VALID')$orderby=lastUpdated desc`

### Response

List of `c8y_certification_testCertificate` managed objects. If list is empty it means that no certification exists (no certification Logo). If list contains one element it means that this prodcut was certified (certification logo).

## GET all device certificates for one Product

should get all device certificates for one Product to present them

### Request

**GET** `{{url}}/inventory/managedObjects?withTotalPages=true&pageSize=100&currentPage=1&query=$filter=(type eq 'c8y_certification_testCertificate' and product.productName eq '{{product_name}}' and product.vendorName eq '{{vendor_name}}' and certificate.status.code eq 'VALID')$orderby=lastUpdated desc`

### Response

List of `c8y_certification_testCertificate` managed objects of the same product, descending order (newest first). Device information of each certificate object looks as follows:
```json
{
"device": {
                "c8y_Firmware": {
                    "name": "debian-10.11",
                    "version": "5.10.60.1-microsoft-standard-WSL2",
                    "url": null
                },
                "c8y_Agent": {
                    "name": "DM Reference Agent",
                    "version": "0.2",
                    "url": "8893a9f33a8c"
                },
                "c8y_Hardware": {
                    "serialNumber": "8893a9f33a8c",
                    "model": "docker",
                    "revision": "1.0"
                },
                "deviceId": "1184255"
            }
}
```

**!! PDF Link not defined yet !!**

## GET latest Capabilites for one product where STATUS equals `SUCCESSFUL`
should get for one product all latest Capabilites which have the STATUS of `SUCCESSFUL`

### Request

**GET** `{{url}}/inventory/managedObjects?pageSize=1&query=$filter=(type eq 'c8y_certification_testCertificate' and product.productName eq '{{product_name}}' and product.vendorName eq '{{vendor_name}}' and certificate.status.code eq 'VALID')$orderby=lastUpdated desc`

### Response

List of `c8y_certification_testCertificate` managed objects of a specific product ( 0 or 1). If list contains one entity, to get all `SUCCESSFUL` capabilties, search for fragment `tests.modules` and loop through all items. Either the item is type of an `container` (`{"container": true}`), then loop again through all `modules` and check if status equals `SUCCESSFUL`. 

**Example:**

```json
{ "container": true,
  "id": "sendingOperationalData",
  "title": "Sending Operational Data",
  "mandatory": true,
  "modules": [
     {
       "capabilities": [...],
       "id": "operationDataAlarms",
       "title": "Sending Operational Data - Alarms",
       "status": { 
          "code": "SUCCESSFUL"
       }
     }, ... ]
}
```

Otherwise, if the item is not type of a `container` (no fragment `container` exists), then search straight for status equals `SUCCESSFUL`.

**Example:**

```json
{
    "capabilities": [...],
    "id": "deviceLogs",
    "title": "Log File Retrieval",
    "status": {
       "code": "SUCCESSFUL"
       }
}
```

## GET all products and filter for capabilities 

should get all products which meets the selected capabilities but needed for the startpage to limit down the amount of products (Filtering)

### Request

**GET** `{{url}}/inventory/managedObjects?withTotalPages=true&pageSize=1000&currentPage=1&query=$filter=(type eq 'c8y_certification_testCertificate' and certificate.status.code eq 'VALID' ) $orderby=lastUpdated desc`

### Response

List of all `c8y_certification_testCertificate` managed objects, order by latest updates descending. To filter the list of certificates, go through each `tests.modules` items and validat for `status.code` equals `SUCCESSFUL`. The following table shows the matches between DPP filter name and certificate id:
|DPP Filtername|Capability|
|-------------|-------------|
| Alarms|`operationDataAlarms`|
| Child Device Management|`deviceGateways`|
| Cloud remote access|`deviceCloudRemoteAccess`|
| Configuration management|`deviceConfiguration`|
| Device profile|`deviceProfile`|
| Device shell|`deviceShell`|
| Events|`operationDataEvents`|
| Firmware management|`deviceFirmware`|
| Identity|`externalId`|
| Location & Tracking|`deviceLocationAndTracking`|
| Measurements|`operationDataMeasurements`|
| Mobile|`deviceMobile`|
| Network configuration|`deviceNetwork`|
| Remote log retrieval|`deviceLogs`|
| Restart|`deviceRestart`|
| Measurement requests|`measurementRequest`|
| Service monitoring|`deviceInformation_c8y_RequiredAvailability`|
| Software management|`managingDeviceSoftware`|

## GET pdf file for explicit product

should get for one product a pdf file (extension of Case 2)

------
