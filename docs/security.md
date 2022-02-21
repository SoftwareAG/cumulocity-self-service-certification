# Endpoints provided by the Open API python microservice


## Products
Get an existing product by a product ID
GET `{{baseUrl}}/products/{product_id}`  [GET product](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0NzU-get-product)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------

Get all products for a particular tenant/vendor
GET `{{baseUrl}}/products`  [GET products](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mjc5OTAxNjU-get-products)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


Update an existing product
PUT `{{baseUrl}}/products/{product_id}`  [UPDATE product](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0NzY-update-product)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


Create a new product providing a partial product managed object
POST `{{baseUrl}}/products`  [CREATE product](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0NzQ-create-product)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


Delete an existing product
DELETE `{{baseUrl}}/products/{product_id}`  [DELETE product](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0Nzc-delete-product)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


## Testsuites
Get latest testSuite
GET `{{baseUrl}}/testsuites/latest`  [GET latest testSuite](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0NzE-get-latest-test-suite)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


Get a testSuite by ID
GET `{{baseUrl}}/testsuites/{testsuite_id}`  [GET testSuite by ID](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0NzI-get-test-suite-by-id)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------

## Testruns


Get a testrun for a product by testrun ID
GET `{{baseUrl}}/testruns/{testrun_id}`  [GET testrun](https://softwareag.stoplight.io/docs/gateway-certification/b3A6MzgxMzEwNDc-get-testrun)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


Get all testruns
GET `{{baseUrl}}/testruns`  [Get testruns](https://softwareag.stoplight.io/docs/gateway-certification/b3A6MzgxMzEwNDU-get-testruns)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


Udate an existing testrun
PUT `{{baseUrl}}/testruns/{testrun_id}`  [UPDATE testrun](https://softwareag.stoplight.io/docs/gateway-certification/b3A6MzgxMzEwNDg-update-testrun)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


Create a testrun
POST `{{baseUrl}}/testruns`    [CREATE testrun](https://softwareag.stoplight.io/docs/gateway-certification/b3A6MzgxMzEwNDY-create-testrun)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


delete an existing testrun
DELETE `{{baseUrl}}/testruns/{testrun_id}`    [DELETE testrun](https://softwareag.stoplight.io/docs/gateway-certification/b3A6MzgxMzEwNDk-delete-testrun)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


Starts the execution of the device certification
GET `{{baseUrl}}/testruns/{testrun_id}/certify`  [GET testrun certify](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0ODM-get-testrun-certify)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


## Testcertificates

Get certificate by id
GET `{{baseUrl}}/certificates/{certificate_id}`  [GET certificate](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc1ODYxNjU-get-certificate)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


Get all certificates for a particular product id (managed object id).
GET `{{baseUrl}}/certificate`  [GET certificate](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0ODQ-get-certificates)


| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | Yes       |
| `None`     | No        |

---------


Create a certificate managed object
POST `{{baseUrl}}/certificates`  [CREATE  certificate](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0ODU-create-certificate)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


Delete certificate by id
DELETE `{{baseUrl}}/certificates/{certificate_id}`  [DELETE certificate](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc1ODYxNjY-delete-certificate)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | No       |
| `None`     | No        |

---------


## Document

Get one PDF document of a certified device to download the file
GET `{{baseUrl}}/document/{document_id}`  [GET document](https://softwareag.stoplight.io/docs/gateway-certification/b3A6Mzc0MDk0ODg-get-document)

| Role  | Access |
| --------- | --------- |
| `ADMIN_CERTIFICATION_ROLE`   | Yes       |
| `READ_CERTIFICATION_ROLE` | Yes       |
| `None`     | No        |

---------

