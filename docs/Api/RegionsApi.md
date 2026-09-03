# GeoSearch\RegionsApi

Administrative regions/states/provinces

All URIs are relative to https://geosearch.dev, except if the operation defines another base path.

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**getRegion()**](RegionsApi.md#getRegion) | **GET** /v1/regions/{id} | Get region by ID |
| [**listRegionCities()**](RegionsApi.md#listRegionCities) | **GET** /v1/regions/{id}/cities | List cities in a region |
| [**listRegions()**](RegionsApi.md#listRegions) | **GET** /v1/regions | List regions |
| [**regionChildren()**](RegionsApi.md#regionChildren) | **GET** /v1/regions/{id}/children | List child cities of a region |


## `getRegion()`

```php
getRegion($id, $lang, $fields): \GeoSearch\Model\RegionSingleResponse
```

Get region by ID

Returns a single region by its numeric ID.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoSearch\Api\RegionsApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$id = 5332921; // int | Region ID
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->getRegion($id, $lang, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling RegionsApi->getRegion: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **id** | **int**| Region ID | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoSearch\Model\RegionSingleResponse**](../Model/RegionSingleResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `listRegionCities()`

```php
listRegionCities($id, $lang, $cursor, $limit, $fields, $sort): \GeoSearch\Model\CityListResponse
```

List cities in a region

Returns a paginated list of cities within a specific region.  THIS ENDPOINT AND `/v1/cities?within=` ANSWER DIFFERENT QUESTIONS AND WILL SOMETIMES RETURN DIFFERENT CITIES FOR THE SAME REGION. That is intended, not a bug. This endpoint answers the ADMINISTRATIVE question — which cities are assigned to this region by GeoNames' own admin codes — while `?within=` answers the GEOMETRIC one, which cities fall inside the region's polygon. The two disagree wherever an enclave, an exclave or a blank admin code puts a city's assignment at odds with its location.  Use this endpoint when you want the official assignment; use `/v1/cities?within=` when you want what is physically inside the boundary. This one is charged at the standard 1 unit; `?within=` costs 2.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoSearch\Api\RegionsApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$id = 5332921; // int | Region ID
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$cursor = eyJpZCI6MjV9; // string | Pagination cursor from a previous response
$limit = 25; // int | Number of results per page (1-100, default 25)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response
$sort = -population; // string | Sort field. Allowed: name, population.

try {
    $result = $apiInstance->listRegionCities($id, $lang, $cursor, $limit, $fields, $sort);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling RegionsApi->listRegionCities: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **id** | **int**| Region ID | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **cursor** | **string**| Pagination cursor from a previous response | [optional] |
| **limit** | **int**| Number of results per page (1-100, default 25) | [optional] [default to 25] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |
| **sort** | **string**| Sort field. Allowed: name, population. | [optional] |

### Return type

[**\GeoSearch\Model\CityListResponse**](../Model/CityListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `listRegions()`

```php
listRegions($lang, $country, $level, $population_min, $population_max, $cursor, $limit, $fields, $sort): \GeoSearch\Model\RegionListResponse
```

List regions

Returns a paginated list of regions with optional filtering by country, level, and population.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoSearch\Api\RegionsApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$country = US; // string | Filter by ISO alpha-2 country code
$level = 1; // int | Filter by administrative level
$population_min = 1000000; // int | Minimum population filter
$population_max = 10000000; // int | Maximum population filter
$cursor = eyJpZCI6MjV9; // string | Pagination cursor from a previous response
$limit = 25; // int | Number of results per page (1-100, default 25)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response
$sort = -population; // string | Sort field. Allowed: name, population.

try {
    $result = $apiInstance->listRegions($lang, $country, $level, $population_min, $population_max, $cursor, $limit, $fields, $sort);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling RegionsApi->listRegions: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **country** | **string**| Filter by ISO alpha-2 country code | [optional] |
| **level** | **int**| Filter by administrative level | [optional] |
| **population_min** | **int**| Minimum population filter | [optional] |
| **population_max** | **int**| Maximum population filter | [optional] |
| **cursor** | **string**| Pagination cursor from a previous response | [optional] |
| **limit** | **int**| Number of results per page (1-100, default 25) | [optional] [default to 25] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |
| **sort** | **string**| Sort field. Allowed: name, population. | [optional] |

### Return type

[**\GeoSearch\Model\RegionListResponse**](../Model/RegionListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `regionChildren()`

```php
regionChildren($id, $lang, $fields): \GeoSearch\Model\CityListResponse
```

List child cities of a region

Returns all cities that are direct children of the specified region in the administrative hierarchy.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoSearch\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoSearch\Api\RegionsApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$id = 5332921; // int | Region ID
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->regionChildren($id, $lang, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling RegionsApi->regionChildren: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **id** | **int**| Region ID | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoSearch\Model\CityListResponse**](../Model/CityListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)
