# GeoAPI\CitiesApi

City data with geographic coordinates

All URIs are relative to https://geosearch.dev, except if the operation defines another base path.

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**cityHierarchy()**](CitiesApi.md#cityHierarchy) | **GET** /v1/cities/{id}/hierarchy | Get administrative hierarchy for a city |
| [**getCity()**](CitiesApi.md#getCity) | **GET** /v1/cities/{id} | Get city by ID |
| [**listCities()**](CitiesApi.md#listCities) | **GET** /v1/cities | List cities |
| [**nearbyCities()**](CitiesApi.md#nearbyCities) | **GET** /v1/cities/nearby | Find nearby cities |


## `cityHierarchy()`

```php
cityHierarchy($id, $lang): \GeoAPI\Model\HierarchyListResponse
```

Get administrative hierarchy for a city

Returns the full administrative hierarchy for a city, ordered from the city itself up through region, country, and continent.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\CitiesApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$id = 5391959; // int | City ID
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)

try {
    $result = $apiInstance->cityHierarchy($id, $lang);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling CitiesApi->cityHierarchy: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **id** | **int**| City ID | |
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

## `getCity()`

```php
getCity($id, $lang, $fields): \GeoAPI\Model\CitySingleResponse
```

Get city by ID

Returns a single city by its numeric ID.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\CitiesApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$id = 5391959; // int | City ID
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->getCity($id, $lang, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling CitiesApi->getCity: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **id** | **int**| City ID | |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoAPI\Model\CitySingleResponse**](../Model/CitySingleResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `listCities()`

```php
listCities($lang, $country, $admin1, $name, $population_min, $population_max, $timezone, $min_elevation, $max_elevation, $within, $bbox, $cursor, $limit, $fields, $sort): \GeoAPI\Model\CityListResponse
```

List cities

Returns a paginated list of cities with optional filtering by country, admin code, name, population, timezone, and elevation.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\CitiesApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$country = US,CA; // string | Filter by ISO alpha-2 country codes (comma-separated)
$admin1 = CA; // string | Filter by admin1 code (state/province)
$name = San Fran; // string | Filter by city name (trigram fuzzy search)
$population_min = 1000000; // int | Minimum population filter
$population_max = 10000000; // int | Maximum population filter
$timezone = America/Los_Angeles; // string | Filter by IANA timezone ID
$min_elevation = 500; // int | Minimum elevation in meters
$max_elevation = 3000; // int | Maximum elevation in meters
$within = 6252001; // int | Return only results whose coordinates fall geometrically inside the boundary of the given area, identified by its GeoNames id. Countries and administrative regions are valid areas; a city id is not.  Accepts exactly one id. A COMMA-SEPARATED LIST IS REJECTED with a 422 naming the limit — a deliberate departure from the comma-separated convention `country` uses, because each value would be a separate polygon intersection. Ask for one area per request.  COST: a request using this parameter consumes 2 quota units instead of 1, on every plan including Free. Combining it with `bbox` still costs 2, not 3 — the highest multiplier applies rather than the sum, and adding a box makes the query cheaper to serve, so it is never penalised.  This asks a GEOMETRIC question and can therefore return a different set of cities than `/v1/regions/{id}/cities`, which asks an administrative one. See that endpoint's description for when and why the two disagree.  Two failures are reported with distinct 400 codes so a typo is distinguishable from a coverage gap: `area_not_an_area` means the id does not name a country or region at all, and `area_no_boundary` means it does but no boundary polygon is available for it yet.
$bbox = -122.6,37.6,-122.2,37.9; // string | Return only results inside the bounding box, given as four comma-separated numbers in the order `w,s,e,n` — west longitude, south latitude, east longitude, north latitude.  Longitudes must be within [-180, 180] and latitudes within [-90, 90].  A box where WEST IS GREATER THAN EAST wraps the antimeridian and is fully supported: `bbox=170,-20,-170,-10` is a box around Fiji, evaluated as the union of the two halves it spans. Latitude has no equivalent wrap-around meaning, so `s` greater than `n` is a validation error rather than a wrapped box.  Charged at the standard request cost of 1 unit. Adding it to a `within` query narrows the candidate set before the polygon test and does not raise the charge.
$cursor = eyJpZCI6MjV9; // string | Pagination cursor from a previous response
$limit = 25; // int | Number of results per page (1-100, default 25)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response
$sort = -population; // string | Sort field. Allowed: name, population, elevation, id.

try {
    $result = $apiInstance->listCities($lang, $country, $admin1, $name, $population_min, $population_max, $timezone, $min_elevation, $max_elevation, $within, $bbox, $cursor, $limit, $fields, $sort);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling CitiesApi->listCities: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **lang** | **string**| ISO 639-1 language code for localized names (e.g., de, fr, ja) | [optional] |
| **country** | **string**| Filter by ISO alpha-2 country codes (comma-separated) | [optional] |
| **admin1** | **string**| Filter by admin1 code (state/province) | [optional] |
| **name** | **string**| Filter by city name (trigram fuzzy search) | [optional] |
| **population_min** | **int**| Minimum population filter | [optional] |
| **population_max** | **int**| Maximum population filter | [optional] |
| **timezone** | **string**| Filter by IANA timezone ID | [optional] |
| **min_elevation** | **int**| Minimum elevation in meters | [optional] |
| **max_elevation** | **int**| Maximum elevation in meters | [optional] |
| **within** | **int**| Return only results whose coordinates fall geometrically inside the boundary of the given area, identified by its GeoNames id. Countries and administrative regions are valid areas; a city id is not.  Accepts exactly one id. A COMMA-SEPARATED LIST IS REJECTED with a 422 naming the limit — a deliberate departure from the comma-separated convention &#x60;country&#x60; uses, because each value would be a separate polygon intersection. Ask for one area per request.  COST: a request using this parameter consumes 2 quota units instead of 1, on every plan including Free. Combining it with &#x60;bbox&#x60; still costs 2, not 3 — the highest multiplier applies rather than the sum, and adding a box makes the query cheaper to serve, so it is never penalised.  This asks a GEOMETRIC question and can therefore return a different set of cities than &#x60;/v1/regions/{id}/cities&#x60;, which asks an administrative one. See that endpoint&#39;s description for when and why the two disagree.  Two failures are reported with distinct 400 codes so a typo is distinguishable from a coverage gap: &#x60;area_not_an_area&#x60; means the id does not name a country or region at all, and &#x60;area_no_boundary&#x60; means it does but no boundary polygon is available for it yet. | [optional] |
| **bbox** | **string**| Return only results inside the bounding box, given as four comma-separated numbers in the order &#x60;w,s,e,n&#x60; — west longitude, south latitude, east longitude, north latitude.  Longitudes must be within [-180, 180] and latitudes within [-90, 90].  A box where WEST IS GREATER THAN EAST wraps the antimeridian and is fully supported: &#x60;bbox&#x3D;170,-20,-170,-10&#x60; is a box around Fiji, evaluated as the union of the two halves it spans. Latitude has no equivalent wrap-around meaning, so &#x60;s&#x60; greater than &#x60;n&#x60; is a validation error rather than a wrapped box.  Charged at the standard request cost of 1 unit. Adding it to a &#x60;within&#x60; query narrows the candidate set before the polygon test and does not raise the charge. | [optional] |
| **cursor** | **string**| Pagination cursor from a previous response | [optional] |
| **limit** | **int**| Number of results per page (1-100, default 25) | [optional] [default to 25] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |
| **sort** | **string**| Sort field. Allowed: name, population, elevation, id. | [optional] |

### Return type

[**\GeoAPI\Model\CityListResponse**](../Model/CityListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `nearbyCities()`

```php
nearbyCities($lat, $lon, $radius, $limit, $fields): \GeoAPI\Model\NearbyCityListResponse
```

Find nearby cities

Returns cities near a given latitude/longitude within a specified radius. Results are ordered by distance. Uses PostGIS spatial index for fast lookups.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\CitiesApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$lat = 37.7749; // float | Latitude (-90 to 90)
$lon = -122.4194; // float | Longitude (-180 to 180)
$radius = 50; // float | Search radius in kilometers (default 50, max 200)
$limit = 10; // int | Maximum results to return (1-250, default 10)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->nearbyCities($lat, $lon, $radius, $limit, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling CitiesApi->nearbyCities: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **lat** | **float**| Latitude (-90 to 90) | |
| **lon** | **float**| Longitude (-180 to 180) | |
| **radius** | **float**| Search radius in kilometers (default 50, max 200) | [optional] [default to 50] |
| **limit** | **int**| Maximum results to return (1-250, default 10) | [optional] [default to 10] |
| **fields** | **string**| Comma-separated list of fields to include in the response | [optional] |

### Return type

[**\GeoAPI\Model\NearbyCityListResponse**](../Model/NearbyCityListResponse.md)

### Authorization

[apiKeyAuth](../../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)
