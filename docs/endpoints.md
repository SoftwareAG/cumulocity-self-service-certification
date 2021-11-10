# Endpoints provided by the python microservice

## Overall Tests

This endpoint shall trigger all tests for a device. Call Certification Endpoint (General)

GET `{{baseUrl}}/service/gateway-certification/perform_certification/{testRunID}?d={deviceId}`

---

## Testsuites

This endpoint will give you all Testsuites
GET `{{baseUrl}}/inventory/managedObjects?type=c8y_certification_testSuite`

This endpoint will give you the latest Testsuites
GET `{{baseUrl}}/inventory/managedObjects?pageSize=1&query=$filter=(type eq 'c8y_certification_testSuite')$orderby=lastUpdated desc`

This endpoint will create a new Testsuite
POST `{{baseUrl}}/inventory/managedObjects/testsuite`

This endpoint will distribute Testsuite from enterprise tenant to all subtenants that are subscribed for Gateway-Certification microservice.
GET `{{baseUrl}}/service/gateway-certification/testsuite


---

## Testruns

This endpoint will give you all Testruns
GET `{{baseUrl}}/inventory/managedObjects?type=c8y_certification_testRun`

This endpoint will give you all Testruns - ordered by updated
GET `{{baseUrl}}/inventory/managedObjects?withTotalPages=true&pageSize=1&currentPage=1&query=$filter=type eq 'c8y_certification_testRun'$orderby=lastUpdated asc`

This endpoint will give you all Testruns - with Partial Name
GET `{{baseUrl}}/inventory/managedObjects?withTotalPages=true&pageSize=10&currentPage=1&query=$filter=(type eq 'c8y_certification_testRun' and name eq '*DIRK*')$orderby=lastUpdated asc`

This endpoint will create a new Full Certification Run
POST `{{baseUrl}}/service/gateway-certification/test_run` with the body for the POST request as:

`{
 "tenant_id": "tenant_id",                               
 "device_id": "device_id",                               
 "vendor_name": "vendor_name", 
 "product_name": "product_name", 
 "product_type": "product_type" 
 }`


This endpoint will update a certification run
PUT `{{baseUrl}}/inventory/managedObjects/{{test_run_id}}`


---

## Testcertificates

This endpoint will give you all Testcertificates
GET `{{baseUrl}}/inventory/managedObjects?withTotalPages=true&pageSize=1&currentPage=1&query=$filter=type eq 'c8y_certification_testCertificate'`

This endpoint will give you all Testcertificates - ordered by updated
GET `{{baseUrl}}/inventory/managedObjects?withTotalPages=true&pageSize=1&currentPage=1&query=$filter=type eq 'c8y_certification_testCertificate'$orderby=creationTime asc`

This endpoint will give you all Testcertificates - with Partial Name

This endpoint will give generate test_certificate from test_run ID
GET `{{baseUrl}}/service/gateway-certification/test_certificate/{testRunID}?t={tenantID}`

---
