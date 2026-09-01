# GeoAPI\SearchApi

Cross-type fuzzy text search

All URIs are relative to https://geosearch.dev, except if the operation defines another base path.

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**autocomplete()**](SearchApi.md#autocomplete) | **GET** /v1/autocomplete | Autocomplete search |
| [**resolveCoordinate()**](SearchApi.md#resolveCoordinate) | **GET** /v1/resolve | Resolve coordinates to their containing administrative areas |
| [**reverseGeocode()**](SearchApi.md#reverseGeocode) | **GET** /v1/reverse | Reverse geocode coordinates |
| [**search()**](SearchApi.md#search) | **GET** /v1/search | Cross-type search |


## `autocomplete()`

```php
autocomplete($q, $lang, $limit, $fields): \GeoAPI\Model\AutocompleteListResponse
```

Autocomplete search

Returns autocomplete suggestions matching a query string across cities, regions, and countries. Results are ranked by relevance and population. Minimum 2 characters required.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\SearchApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$q = San Fran; // string | Search query (minimum 2 characters)
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$limit = 10; // int | Maximum results to return (1-25, default 10)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->autocomplete($q, $lang, $limit, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling SearchApi->autocomplete: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **q** | **string**| Search query (minimum 2 characters) | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **limit** | **int**| Maximum results to return (1-25, default 10) | [optional] [default to 10] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoAPI\Model\AutocompleteListResponse**](../Model/AutocompleteListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `resolveCoordinate()`

```php
resolveCoordinate($lat, $lon, $lang): \GeoAPI\Model\HierarchyListResponse
```

Resolve coordinates to their containing administrative areas

Returns the administrative areas whose BOUNDARY POLYGONS CONTAIN the given coordinate, ordered country first.  ## How this differs from `/v1/reverse`  These two endpoints take the same parameters and answer different questions, and the difference is the reason both exist.  `/v1/reverse` returns the NEAREST city. It always returns something, and for a point near a border that something is sometimes in the neighbouring country.  `/v1/resolve` returns the areas that actually CONTAIN the point. It is never wrong about which country a point is in — and it sometimes returns nothing at all, because no polygon covers the point or because we hold no polygon for that country. Choose this endpoint when correctness at borders matters and choose `/v1/reverse` when you always need an answer.  ## `depth` RUNS THE OPPOSITE DIRECTION FROM `/v1/cities/{id}/hierarchy`  Read this before writing code that consumes both endpoints.  Both return the same node SHAPE — `geoname_id`, `name`, `type`, `depth` — so one rendering path can accept either. The `depth` SEMANTICS are inverted between them:  - On **this** endpoint `depth` is POSITIONAL, counting outward-in from   the largest area: **`depth: 0` is the COUNTRY**, `depth: 1` is the   region inside it, and so on. - On **`/v1/cities/{id}/hierarchy`** `depth` counts up from the entity   that was asked about: `depth: 0` is the CITY, and the country is at the   highest depth in the list.  So `data[0]` is the country here and the city there. Code that sorts or indexes on `depth` across both endpoints without accounting for this will silently invert the hierarchy rather than fail.  ## Cost and availability  One quota unit, on every plan including Free. This is a single indexed point-in-polygon probe returning names, not a geometry transfer, so it carries no premium and no tier gate.  `?fields=` IS NOT SUPPORTED on this endpoint and is ignored if sent. The four node fields are all small, so selection would save nothing.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\SearchApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$lat = 37.7749; // float | Latitude (-90 to 90). Must be a finite number: `NaN` and `Infinity` are rejected with a 400 rather than being passed to the spatial index, which would answer them with an ordinary \"not found\".
$lon = -122.4194; // float | Longitude (-180 to 180). Must be a finite number; see `lat`.
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)

try {
    $result = $apiInstance->resolveCoordinate($lat, $lon, $lang);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling SearchApi->resolveCoordinate: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **lat** | **float**| Latitude (-90 to 90). Must be a finite number: &#x60;NaN&#x60; and &#x60;Infinity&#x60; are rejected with a 400 rather than being passed to the spatial index, which would answer them with an ordinary \&quot;not found\&quot;. | |
| **lon** | **float**| Longitude (-180 to 180). Must be a finite number; see &#x60;lat&#x60;. | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |

### Return type

[**\GeoAPI\Model\HierarchyListResponse**](../Model/HierarchyListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `reverseGeocode()`

```php
reverseGeocode($lat, $lon, $fields): \GeoAPI\Model\ReverseGeocodeSingleResponse
```

Reverse geocode coordinates

Returns the nearest city for a given latitude/longitude. Uses PostGIS spatial index for fast reverse geocoding.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\SearchApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$lat = 37.7749; // float | Latitude (-90 to 90)
$lon = -122.4194; // float | Longitude (-180 to 180)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->reverseGeocode($lat, $lon, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling SearchApi->reverseGeocode: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **lat** | **float**| Latitude (-90 to 90) | |
| **lon** | **float**| Longitude (-180 to 180) | |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoAPI\Model\ReverseGeocodeSingleResponse**](../Model/ReverseGeocodeSingleResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `search()`

```php
search($q, $lang, $type, $limit, $fields): \GeoAPI\Model\SearchListResponse
```

Cross-type search

Performs a fuzzy text search across countries, regions, and cities using trigram matching. Results are ranked by relevance and population. Uses simple limit pagination (no cursor).

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\SearchApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$q = San Fran; // string | Search query (minimum 2 characters)
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$type = city; // string | Filter by entity type (comma-separated). Allowed: country, region, city.
$limit = 10; // int | Maximum results to return (1-100, default 25)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->search($q, $lang, $type, $limit, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling SearchApi->search: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **q** | **string**| Search query (minimum 2 characters) | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **type** | **string**| Filter by entity type (comma-separated). Allowed: country, region, city. | [optional] |
| **limit** | **int**| Maximum results to return (1-100, default 25) | [optional] [default to 25] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoAPI\Model\SearchListResponse**](../Model/SearchListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)
