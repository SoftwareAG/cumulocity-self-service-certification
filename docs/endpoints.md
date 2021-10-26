# Endpoints provided by the python microservice

## Overall Tests

This endpoint shall trigger all tests for a device. Call Certification Endpoint (General)

GET `{{baseUrl}}/gateway-certification/certification/{deviceId}`

---

## Testsuites

This endpoint will give you all Testsuites
GET `{{baseUrl}}/inventory/managedObjects?type=c8y_certification_testSuite`

This endpoint will give you the latest Testsuites
GET `{{baseUrl}}/inventory/managedObjects?pageSize=1&query=$filter=(type eq 'c8y_certification_testSuite')$orderby=lastUpdated desc`

This endpoint will create a new Testsuite
POST `{{baseUrl}}/inventory/managedObjects/`
as body for Postman POST request you can take this [Test Suite JSON](./data/testsuite.jsonc) as starting point.

---

## Testruns

This endpoint will give you all Testruns
GET `{{baseUrl}}/inventory/managedObjects?type=c8y_certification_testRun`

This endpoint will give you all Testruns - ordered by updated
GET `{{baseUrl}}/inventory/managedObjects?withTotalPages=true&pageSize=1&currentPage=1&query=$filter=type eq 'c8y_certification_testRun'$orderby=lastUpdated asc`

This endpoint will give you all Testruns - with Partial Name
GET `{{baseUrl}}/inventory/managedObjects?withTotalPages=true&pageSize=10&currentPage=1&query=$filter=(type eq 'c8y_certification_testRun' and name eq '*DIRK*')$orderby=lastUpdated asc`

This endpoint will create a new Full Certification Run
POST `{{baseUrl}}/inventory/managedObjects/`
as body for Postman POST request you can take this [Full Certification JSON](./data/full-certification-run.jsonc) as starting point.

This endpoint will update a certification run
PUT `{{baseUrl}}/inventory/managedObjects/{{test_run_id}}`
as body for Postman PUT request you can take this [Update Certification JSON](./data/update-certification-run.jsonc) as starting point.

---

## Testcertificates

This endpoint will give you all Testcertificates
GET `{{baseUrl}}/inventory/managedObjects?withTotalPages=true&pageSize=1&currentPage=1&query=$filter=type eq 'c8y_certification_testCertificate'`

This endpoint will give you all Testcertificates - ordered by updated
GET `{{baseUrl}}/inventory/managedObjects?withTotalPages=true&pageSize=1&currentPage=1&query=$filter=type eq 'c8y_certification_testCertificate'$orderby=creationTime asc`

This endpoint will give you all Testcertificates - with Partial Name

---
