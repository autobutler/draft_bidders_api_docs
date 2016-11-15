# Draft Offers

## Create a Draft Offer

```shell
curl -X "POST" "https://www.autobutler.dk/api/v2/draft_bidders/jobs/531512/draft_offer" \
     -H "Authorization: supersecretapikey" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d "{\"qualityOfParts\":\"OEM\",\"guaranteeOnParts\":12,\"guaranteeOnWork\":24,\"bodyText\":\"Dear car owner. Here is your offer.\",\"lineItems\":[{\"description\":\"Brake Fluid\",\"quantity\":1,\"unit\":\"liter\",\"netPrice\":\"100\",\"grossPrice\":\"120\",\"type\":\"part_people\",\"articleNumber\":\"123A-BCD-4EF\"}]}"
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint creates a draft offer for the job with the specified id. If the
specified job is unverified, it will be marked as verified at the same time.

### HTTP Request

`POST https://www.autobutler.dk/api/v2/draft_bidders/jobs/<JOB_ID>/draft_offer`

### URL Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | ---------------------------------------------
JOB_ID    | `null`  | yes      | The ID of the job to create a draft offer for

### JSON Body Parameters

> Example JSON input

```json
{
  "guaranteeOnWork": 24,
  "guaranteeOnParts": 12,
  "lineItems": [
    {
      "unit": "liter",
      "quantity": 1,
      "grossPrice": "120",
      "description": "Brake Fluid",
      "netPrice": "100",
      "type": "part_people",
      "articleNumber": "123A-BCD-4EF"
    },
    {
      "unit": "hours",
      "quantity": 1.5,
      "grossPrice": "399",
      "description": "Working hours",
      "netPrice": "399"
    }
  ],
  "qualityOfParts": "OEM",
  "bodyText": "Dear car owner. Here is your offer."
}
```

Parameter        | Type          | Default | Required | Description
---------------- | ------------- | ------- | -------- | -------------------------------------------------------------------------------------------------
qualityOfParts   | string        | `null`  | **yes**  | The quality of the parts included in the offer.<br>**_See below for accepted values_**
guaranteeOnParts | integer       | `null`  | **yes**  | The warranty in months on the parts included in the offer.<br>**_See below for accepted values_**
guaranteeOnWork  | integer       | `null`  | **yes**  | The warranty in months on the work included in the offer.<br>**_See below for accepted values_**
bodyText         | string        | `null`  | **yes**  | A message for the car owner describing the offer
lineItems        | array(object) | `null`  | **yes**  | A list of line items included in the offer.<br>**_See below for structure_**

### Accepted `qualityOfParts` values

- `"NONE"`
- `"ORIGINAL"`
- `"OEM"`
- `"ALTERNATIVE"`
- `"USED"`
- `"OTHER"`

### Accepted `guaranteeOnParts` and `guaranteeOnWork` values

- `0`: No warranty
- `6`
- `12`
- `18`
- `24`
- `30`
- `36`
- `48`
- `60`
- `72`
- `9999`: Lifetime warranty

### `lineItems` structure

Attribute     | Type    | Default | Required | Description
------------- | ------- | ------- | -------- | --------------------------------------------------------------------------------------------------------------------
description   | string  | `null`  | **yes**  | A description of the line item
quantity      | float   | 1.0     | no       | The number of this items included in the offer
unit          | string  | `"pcs"` | no       | An identifier that determines the type of individual units of this line item.<br>**_See below for accepted values_**
netPrice      | float   | `null`  | **yes**  | The net price of the line item per unit. Ie. what the workshop has to pay for a single unit of this item
grossPrice    | float   | `null`  | **yes**  | The gross price of the line item per unit. Ie. what the car owner has to pay for a single unit of this item
type          | string  | `null`  | no       | The type of line item.<br>**_See below for accepted values_**
articleNumber | string  | `null`  | no       | The article number for the part in your system

### Accepted `unit` values
- `"pcs"`: Pieces
- `"liter"`: Liters
- `"gram"`: Grams
- `"kg"`: Kilograms
- `"meter"`: Meters
- `"set"`: Sets
- `"hours"`: Hours - **Must be used for work-related line items**

### Accepted `type` values
- `null`: Generic line item with no 3rd party integrations
- `"meca"`: Line item with Meca spare part catalog integration
- `"part_people"`: Line item with Part People catalog integration
- `"twm"`: Line item with TWM crm system integration

### Potential Errors

Error Code | Meaning
---------- | ----------------------------------------------------------------------------------------------------
400        | Draft offer could not be created - Please check the `errors` value in the response for more details.
