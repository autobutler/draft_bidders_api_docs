# Errors

Apart from the possible error codes listed for the individual endpoints, the API
also uses the following general errors:

Error Code | Meaning
---------- | -------------------------------------------------------------------------------------------
401        | Unauthorized -- Your API key is wrong
403        | Forbidden -- Your account is blocked. Please contact support
404        | Not Found -- The specified item could not be found
500        | Internal Server Error -- We had a problem with our server. Try again later.
503        | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
