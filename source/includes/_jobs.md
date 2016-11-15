# Jobs

## Get all Jobs

```shell
curl -X "https://www.autobutler.dk/api/v2/draft_bidders/jobs?page=1&includeUnverified=true" \
     -H "Authorization: supersecretapikey"
```

> The above command returns JSON structured like this:

```json
[
  {
    "currentPage": 1,
    "totalPages": 13,
    "job": {
      "id": 530218,
      "referenceNumber": "ab530218",
      "name": "Brakes",
      "car": "Jaguar XF - 2013",
      "zip": "BL1 6HY",
      "verified": true
    }
  },
  {
    "currentPage": 1,
    "totalPages": 13,
    "job": {
      "id": 530964,
      "referenceNumber": "ab530964",
      "name": "Bodywork (dents etc.)",
      "car": "Honda CR-V - 2013",
      "zip": "TW13 4GA",
      "verified": false
    }
  }
]
```

This endpoint retrieves all jobs available for draft bidding in your country as a paged result set.

### HTTP Request

`GET https://www.autobutler.dk/api/v2/draft_bidders/jobs`

### Query Parameters

Parameter         | Default | Required | Description
----------------- | ------- | -------- | ----------------------------------------------------------
page              | `1`     | no       | The number for the page to return
includeUnverified | `false` | no       | If set to `true`, the results will include unverified jobs

## Get a specific Job

```shell
curl -X "https://www.autobutler.dk/api/v2/draft_bidders/jobs/530785" \
     -H "Authorization: supersecretapikey"
```

> The above command returns JSON structured like this:

```json
{
  "job": {
    "id": 530218,
    "referenceNumber": "ab530218",
    "name": "Brakes",
    "zip": "BL1 6HY",
    "verified": true
  },
  "car": {
    "make": "Jaguar",
    "model": "XF",
    "series": null,
    "year": 2013,
    "registrationNumber": "AB12CDE",
    "vin": "",
    "kilometres": 45000,
    "variant": "D PREMIUM LUXURY SPORTBRAKE",
    "fuelType": "PETROL",
    "chassisNumber": null,
    "typeCode": "-",
    "lastServiceDate": "2016-03-01"
  },
  "jobTasks": [
    {
      "type": "brakes",
      "name": "Brakes",
      "description": "",
      "options": [
        {
          "type": "brakes_what",
          "name": "Which parts",
          "value": "replace_pads",
          "humanValue": "Need my brake pads replaced"
        },
        {
          "type": "brakes_where",
          "name": "Which brakes",
          "value": "front_and_rear",
          "humanValue": "Both front and rear "
        }
      ],
      "files": [
        {
          "url": "http://url_to_image.com/image.jpg"
        }
      ]
    }
  ]
}
```

This endpoint retrieves the details of a specific job.

### HTTP Request

`GET https://www.autobutler.dk/api/v2/draft_bidders/jobs/<ID>`

### URL Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------------------------
ID        | `null`  | **yes**  | The ID of the job to retrieve

### Potential Errors

Error Code | Meaning
---------- | -------
404 | Not Found -- The specified job id could not be found or is unavailable for draft bidding

## Hide a specific Job

```shell
curl -X "DELETE" "https://www.autobutler.dk/api/v2/draft_bidders/jobs/530785" \
     -H "Authorization: supersecretapikey"
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint hides a specific job so that it will no longer be included in
the list of all jobs. The job will still be available in all other endpoints as
long as it doesn't have a draft offer.

### HTTP Request

`DELETE https://www.autobutler.dk/api/v2/draft_bidders/jobs/<ID>`

### URL Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -------------------------
ID        | `null`  | **yes**  | The ID of the job to hide

### Potential Errors

Error Code | Meaning
---------- | ----------------------------------------------------------------------------------------
404        | Not Found -- The specified job id could not be found or is unavailable for draft bidding
