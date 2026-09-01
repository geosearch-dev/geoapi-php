# GeoAPI\CountriesApi

Country data and regions within countries

All URIs are relative to https://geosearch.dev, except if the operation defines another base path.

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**countryNeighbors()**](CountriesApi.md#countryNeighbors) | **GET** /v1/countries/{code}/neighbors | List neighboring countries |
| [**getCountry()**](CountriesApi.md#getCountry) | **GET** /v1/countries/{code} | Get country by ISO code |
| [**listCountries()**](CountriesApi.md#listCountries) | **GET** /v1/countries | List countries |
| [**listCountryRegions()**](CountriesApi.md#listCountryRegions) | **GET** /v1/countries/{code}/regions | List regions in a country |


## `countryNeighbors()`

```php
countryNeighbors($code, $lang, $fields): \GeoAPI\Model\CountryListResponse
```

List neighboring countries

Returns countries that share a border with the specified country.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\CountriesApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$code = DE; // string | ISO alpha-2 country code
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->countryNeighbors($code, $lang, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling CountriesApi->countryNeighbors: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **code** | **string**| ISO alpha-2 country code | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoAPI\Model\CountryListResponse**](../Model/CountryListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `getCountry()`

```php
getCountry($code, $lang, $fields): \GeoAPI\Model\CountrySingleResponse
```

Get country by ISO code

Returns a single country by its ISO alpha-2 code.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\CountriesApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$code = US; // string | ISO alpha-2 country code
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->getCountry($code, $lang, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling CountriesApi->getCountry: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **code** | **string**| ISO alpha-2 country code | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoAPI\Model\CountrySingleResponse**](../Model/CountrySingleResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `listCountries()`

```php
listCountries($lang, $continent, $iso_code, $population_min, $population_max, $cursor, $limit, $fields, $sort): \GeoAPI\Model\CountryListResponse
```

List countries

Returns a paginated list of countries with optional filtering and sorting.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\CountriesApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$continent = EU; // string | Filter by continent code (AF, AN, AS, EU, NA, OC, SA)
$iso_code = US,CA,GB; // string | Filter by ISO alpha-2 codes (comma-separated)
$population_min = 1000000; // int | Minimum population filter
$population_max = 10000000; // int | Maximum population filter
$cursor = eyJpZCI6MjV9; // string | Pagination cursor from a previous response
$limit = 25; // int | Number of results per page (1-100, default 25)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response
$sort = -population; // string | Sort field and direction. Allowed: name, population, area_sq_km. Prefix with - for descending.

try {
    $result = $apiInstance->listCountries($lang, $continent, $iso_code, $population_min, $population_max, $cursor, $limit, $fields, $sort);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling CountriesApi->listCountries: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **continent** | **string**| Filter by continent code (AF, AN, AS, EU, NA, OC, SA) | [optional] |
| **iso_code** | **string**| Filter by ISO alpha-2 codes (comma-separated) | [optional] |
| **population_min** | **int**| Minimum population filter | [optional] |
| **population_max** | **int**| Maximum population filter | [optional] |
| **cursor** | **string**| Pagination cursor from a previous response | [optional] |
| **limit** | **int**| Number of results per page (1-100, default 25) | [optional] [default to 25] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |
| **sort** | **string**| Sort field and direction. Allowed: name, population, area_sq_km. Prefix with - for descending. | [optional] |

### Return type

[**\GeoAPI\Model\CountryListResponse**](../Model/CountryListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `listCountryRegions()`

```php
listCountryRegions($code, $lang, $cursor, $limit, $fields, $sort): \GeoAPI\Model\RegionListResponse
```

List regions in a country

Returns a paginated list of regions (administrative divisions) within a country.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\CountriesApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$code = US; // string | ISO alpha-2 country code
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$cursor = eyJpZCI6MjV9; // string | Pagination cursor from a previous response
$limit = 25; // int | Number of results per page (1-100, default 25)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response
$sort = name; // string | Sort field. Allowed: name, population.

try {
    $result = $apiInstance->listCountryRegions($code, $lang, $cursor, $limit, $fields, $sort);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling CountriesApi->listCountryRegions: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **code** | **string**| ISO alpha-2 country code | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **cursor** | **string**| Pagination cursor from a previous response | [optional] |
| **limit** | **int**| Number of results per page (1-100, default 25) | [optional] [default to 25] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |
| **sort** | **string**| Sort field. Allowed: name, population. | [optional] |

### Return type

[**\GeoAPI\Model\RegionListResponse**](../Model/RegionListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)
