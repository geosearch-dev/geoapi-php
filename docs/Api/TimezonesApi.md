# GeoSearch\TimezonesApi

IANA timezone data

All URIs are relative to https://geosearch.dev, except if the operation defines another base path.

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**getTimezone()**](TimezonesApi.md#getTimezone) | **GET** /v1/timezones/{tzId} | Get timezone by IANA ID |
| [**listTimezones()**](TimezonesApi.md#listTimezones) | **GET** /v1/timezones | List timezones |


## `getTimezone()`

```php
getTimezone($tz_id, $lang, $fields): \GeoSearch\Model\TimezoneSingleResponse
```

Get timezone by IANA ID

Returns a single timezone by its IANA identifier. Note: IANA timezone IDs contain slashes (e.g., America/New_York), so the path uses a wildcard match.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoSearch\Api\TimezonesApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$tz_id = America/New_York; // string | IANA timezone ID (e.g., America/New_York)
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->getTimezone($tz_id, $lang, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling TimezonesApi->getTimezone: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **tz_id** | **string**| IANA timezone ID (e.g., America/New_York) | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoSearch\Model\TimezoneSingleResponse**](../Model/TimezoneSingleResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `listTimezones()`

```php
listTimezones($lang, $country, $cursor, $limit, $fields, $sort): \GeoSearch\Model\TimezoneListResponse
```

List timezones

Returns a paginated list of timezones with optional filtering by country.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoSearch\Api\TimezonesApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$country = US; // string | Filter by ISO alpha-2 country code
$cursor = eyJpZCI6MjV9; // string | Pagination cursor from a previous response
$limit = 25; // int | Number of results per page (1-100, default 25)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response
$sort = gmt_offset; // string | Sort field. Allowed: timezone_id, gmt_offset, country_code.

try {
    $result = $apiInstance->listTimezones($lang, $country, $cursor, $limit, $fields, $sort);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling TimezonesApi->listTimezones: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **country** | **string**| Filter by ISO alpha-2 country code | [optional] |
| **cursor** | **string**| Pagination cursor from a previous response | [optional] |
| **limit** | **int**| Number of results per page (1-100, default 25) | [optional] [default to 25] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |
| **sort** | **string**| Sort field. Allowed: timezone_id, gmt_offset, country_code. | [optional] |

### Return type

[**\GeoSearch\Model\TimezoneListResponse**](../Model/TimezoneListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)
