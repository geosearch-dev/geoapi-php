# GeoSearch\IPGeolocationApi



All URIs are relative to https://geosearch.dev, except if the operation defines another base path.

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**lookupIP()**](IPGeolocationApi.md#lookupIP) | **GET** /v1/ip/{address} | IP geolocation lookup |
| [**lookupMyIP()**](IPGeolocationApi.md#lookupMyIP) | **GET** /v1/ip/me | Caller&#39;s IP geolocation |


## `lookupIP()`

```php
lookupIP($address, $lang, $fields): \GeoSearch\Model\IPSingleResponse
```

IP geolocation lookup

Returns geolocation data for a given IPv4 or IPv6 address.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoSearch\Api\IPGeolocationApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$address = 8.8.8.8; // string | IPv4 or IPv6 address
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->lookupIP($address, $lang, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling IPGeolocationApi->lookupIP: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **address** | **string**| IPv4 or IPv6 address | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoSearch\Model\IPSingleResponse**](../Model/IPSingleResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `lookupMyIP()`

```php
lookupMyIP($lang, $fields): \GeoSearch\Model\IPSingleResponse
```

Caller's IP geolocation

Auto-detects the client's IP address (from X-Forwarded-For or RemoteAddr) and returns its geolocation data.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoSearch\Api\IPGeolocationApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->lookupMyIP($lang, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling IPGeolocationApi->lookupMyIP: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoSearch\Model\IPSingleResponse**](../Model/IPSingleResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)
