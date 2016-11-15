# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl -X "api_endpoint_here" \
     -H "Authorization: supersecretapikey"
```

> Make sure to replace `supersecretapikey` with your API key.

The API uses api keys to allow access.

The API expects for the key to be included in all API requests to the server in a header that looks like the following:

`Authorization: supersecretapikey`

<aside class="notice">
You must replace <code>supersecretapikey</code> with your personal API key.
</aside>
