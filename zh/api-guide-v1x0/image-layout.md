<!-- Style added for the new format. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- The title has been changed to <h1> for the new format. -->
<h1>Image Layout</h1>

**Notification > Notification Hub > API v1.0 User Guide > Image Layout**



<span id="imageLayoutV1x0003GetImageLayout"></span>

## Retrieve Image Layout

Retrieves a single image layout based on its ID.

**Request**

```
GET /image-layout/v1.0/image-layouts/{id}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Location | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | App Key |
| X-NHN-Authorization | Header  | String | Y | Access Token |
| id | Path  | String | Y | Image Layout ID |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "imageLayout" : {
    "id" : "A9z0A9z0",
    "name" : "2025_Promotion_Coupon",
    "backgroundImage" : {
      "fileName" : "background.png",
      "filePreviewUrl" : "https://example.com/background.png"
    },
    "cardImage" : {
      "fileName" : "cardImage.png",
      "filePreviewUrl" : "https://example.com/background.png"
    },
    "title" : "A #{promotion} gift card from #{user} has arrived.",
    "body" : "* Product: Today's Product\n*Expires: Until #{expirydate}\n*Where to use: Online/offline stores (excluding some stores)",
    "useBarcode" : true,
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--Describe the fields of the response body.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| imageLayout | Object |  |
| imageLayout.id | String | Image Layout ID |
| imageLayout.name | String | Image Layout Name |
| imageLayout.backgroundImage | Object |  |
| imageLayout.backgroundImage.fileName | String | Background image file name |
| imageLayout.backgroundImage.filePreviewUrl | String | Background image preview URL |
| imageLayout.cardImage | Object |  |
| imageLayout.cardImage.fileName | String | Card image file name |
| imageLayout.cardImage.filePreviewUrl | String | Card image preview URL |
| imageLayout.title | String | Title |
| imageLayout.body | String | Body |
| imageLayout.useBarcode | Boolean | Whether to use a barcode |
| imageLayout.createdDateTime | String | Image layout creation date and time |
| imageLayout.updatedDateTime | String | Image layout modification date and time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve Image Layout

GET {{endpoint}}/image-layout/v1.0/image-layouts/{{id}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/image-layout/v1.0/image-layouts/${id}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="imageLayoutV1x0CreateImageLayout"></span>

## Create Image Layout

Creates an image layout.

**Request**

```
POST /image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
Content-Type: multipart/form-data
```

**Request Parameters**

| Name | Location | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | App Key |
| X-NHN-Authorization | Header  | String | Y | Access Token |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->


| Name | Type | Required | Description |
| - | - | - | - |
| name | String | Y | Image Layout Name |
| backgroundImage | String | Y | Background image file |
| cardImage | String | Y | Card image file |
| title | String | Y | Title |
| body | String | Y | Body |
| useBarcode | Bolean | Y | Whether to use a barcode |

**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "id" : "A9z0A9z0"
}
```

<!--Describe the fields of the response body.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| id | String | Image Layout ID |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Create Image Layout

POST {{endpoint}}/image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/image-layout/v1.0/image-layouts" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="imageLayoutV1x0DeleteImageLayout"></span>

## Delete Image Layout

Deletes an image layout.

**Request**

```
DELETE /image-layout/v1.0/image-layouts/{id}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Location | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | App Key |
| X-NHN-Authorization | Header  | String | Y | Access Token |
| id | Path  | String | Y | Image Layout ID |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--Describe the fields of the response body.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete Image Layout

DELETE {{endpoint}}/image-layout/v1.0/image-layouts/{{id}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/image-layout/v1.0/image-layouts/${id}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="imageLayoutV1x0GetImageLayoutList"></span>

## Retrieve Image Layout List

Retrieves a list of image layouts.

**Request**

```
GET /image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Location | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | App Key |
| X-NHN-Authorization | Header  | String | Y | Access Token |
| name | Query  | String | N | Image layout name (LIKE search) |
| limit | Query  | Integer | N | If limit is not set, default is 20 (max 1000) |
| offset | Query  | Integer | N | If offset is not set, default is 0 |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "imageLayouts" : [ {
    "id" : "A9z0A9z0",
    "name" : "2025_Promotion_Coupon"
  } ]
}
```

<!--Describe the fields of the response body.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | Total count |
| imageLayouts | Array |  |
| imageLayouts[].id | String | Image Layout ID |
| imageLayouts[].name | String | Image Layout Name |
| imageLayouts[].backgroundImage | Object |  |
| imageLayouts[].backgroundImage.fileName | String | Background image file name |
| imageLayouts[].backgroundImage.filePreviewUrl | String | Background image preview URL |
| imageLayouts[].cardImage | Object |  |
| imageLayouts[].cardImage.fileName | String | Card image file name |
| imageLayouts[].cardImage.filePreviewUrl | String | Card image preview URL |
| imageLayouts[].title | String | Title |
| imageLayouts[].body | String | Body |
| imageLayouts[].useBarcode | Boolean | Whether to use a barcode |
| imageLayouts[].createdDateTime | String | Image layout creation date and time |
| imageLayouts[].updatedDateTime | String | Image layout modification date and time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve Image Layout List

GET {{endpoint}}/image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/image-layout/v1.0/image-layouts" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="imageLayoutV1x0UpdateImageLayout"></span>

## Update Image Layout

Updates an image layout.

**Request**

```
POST /image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
Content-Type: multipart/form-data
```

**Request Parameters**

| Name | Location | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | App Key |
| X-NHN-Authorization | Header  | String | Y | Access Token |


**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->


| Name | Type | Required | Description |
| - | - | - | - |
| name | String | Y | Image Layout Name |
| backgroundImage | String | Y | Background image file |
| cardImage | String | Y | Card image file |
| title | String | Y | Title |
| body | String | Y | Body |
| useBarcode | Bolean | Y | Whether to use a barcode |


**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--Describe the fields of the response body.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Update Image Layout

PATCH {{endpoint}}/image-layout/v1.0/image-layouts/{{id}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PATCH "${endpoint}/image-layout/v1.0/image-layouts/${id}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
