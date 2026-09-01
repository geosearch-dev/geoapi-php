# geoapi-php

Geographic data REST API — modern replacement for GeoNames.

Serves countries, regions, cities, postal codes, timezones, and IP geolocation data
through a fast, well-documented JSON API with cursor-based pagination and field selection.

## Authentication
All endpoints (except health check) require an API key passed via the `X-API-Key` header.

## Rate Limiting
Two independent limits apply to every authenticated request: a per-second
throttle and a monthly quota. They fail with different error codes because
they call for different client behaviour — `rate_limit_exceeded` means back
off for a moment, `quota_exceeded` means the plan's monthly allowance is
exhausted until the period resets.

Responses include rate limit headers:
- `X-RateLimit-Limit` — requests per second allowed
- `X-RateLimit-Remaining` — requests remaining in current window
- `X-RateLimit-Reset` — **Unix epoch second** at which the applicable limit
  resets. This is an absolute timestamp, not a duration. On a
  `quota_exceeded` response it carries the end of the monthly quota period
  rather than the next second boundary.
- `X-Monthly-RateLimit-Limit` — monthly quota
- `X-Monthly-RateLimit-Remaining` — monthly requests remaining
- `X-RateLimit-Upgrade` — advisory message, present only once monthly usage
  passes 80% of the plan's quota
- `Retry-After` — seconds to wait before retrying. Present on both 429s and
  the unambiguous duration; prefer it over deriving one from
  `X-RateLimit-Reset`.

## Pagination
List endpoints use cursor-based pagination with `cursor` and `limit` parameters.
Maximum limit is 100. Responses include pagination metadata in the `meta` object.

## Field Selection
Use `?fields=name,population` on any endpoint to receive only the specified fields.



## Installation & Usage

### Requirements

PHP 8.1 and later.

### Composer

To install the bindings via [Composer](https://getcomposer.org/), add the following to `composer.json`:

```json
{
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/geosearch-dev/geoapi-php.git"
    }
  ],
  "require": {
    "geosearch-dev/geoapi-php": "*@dev"
  }
}
```

Then run `composer install`

### Manual Installation

Download the files and include `autoload.php`:

```php
<?php
require_once('/path/to/geoapi-php/vendor/autoload.php');
```

## Getting Started

Please follow the [installation procedure](#installation--usage) and then run the following:

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');



// Configure API key authorization: apiKeyAuth
$config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKey('X-API-Key', 'YOUR_API_KEY');
// Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
// $config = GeoAPI\Configuration::getDefaultConfiguration()->setApiKeyPrefix('X-API-Key', 'Bearer');


$apiInstance = new GeoAPI\Api\BatchApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$batch_request = {"ids":[5391959,5128581,4887398]}; // \GeoAPI\Model\BatchRequest
$lang = de; // string | ISO 639-1 language code for localized names (e.g., de, fr, ja)
$fields = name,population,iso_code; // string | Comma-separated list of fields to include in the response

try {
    $result = $apiInstance->batchCities($batch_request, $lang, $fields);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling BatchApi->batchCities: ', $e->getMessage(), PHP_EOL;
}

```

## API Endpoints

All URIs are relative to *https://geosearch.dev*

Class | Method | HTTP request | Description
------------ | ------------- | ------------- | -------------
*BatchApi* | [**batchCities**](docs/Api/BatchApi.md#batchcities) | **POST** /v1/batch/cities | Batch lookup cities by IDs
*BatchApi* | [**batchCountries**](docs/Api/BatchApi.md#batchcountries) | **POST** /v1/batch/countries | Batch lookup countries by IDs
*BatchApi* | [**batchRegions**](docs/Api/BatchApi.md#batchregions) | **POST** /v1/batch/regions | Batch lookup regions by IDs
*BoundariesApi* | [**getBoundary**](docs/Api/BoundariesApi.md#getboundary) | **GET** /v1/boundaries/{geoname_id} | Fetch an area&#39;s boundary polygon as GeoJSON
*CitiesApi* | [**cityHierarchy**](docs/Api/CitiesApi.md#cityhierarchy) | **GET** /v1/cities/{id}/hierarchy | Get administrative hierarchy for a city
*CitiesApi* | [**getCity**](docs/Api/CitiesApi.md#getcity) | **GET** /v1/cities/{id} | Get city by ID
*CitiesApi* | [**listCities**](docs/Api/CitiesApi.md#listcities) | **GET** /v1/cities | List cities
*CitiesApi* | [**nearbyCities**](docs/Api/CitiesApi.md#nearbycities) | **GET** /v1/cities/nearby | Find nearby cities
*CountriesApi* | [**countryNeighbors**](docs/Api/CountriesApi.md#countryneighbors) | **GET** /v1/countries/{code}/neighbors | List neighboring countries
*CountriesApi* | [**getCountry**](docs/Api/CountriesApi.md#getcountry) | **GET** /v1/countries/{code} | Get country by ISO code
*CountriesApi* | [**listCountries**](docs/Api/CountriesApi.md#listcountries) | **GET** /v1/countries | List countries
*CountriesApi* | [**listCountryRegions**](docs/Api/CountriesApi.md#listcountryregions) | **GET** /v1/countries/{code}/regions | List regions in a country
*HealthApi* | [**getStatus**](docs/Api/HealthApi.md#getstatus) | **GET** /v1/status | Health check
*IPGeolocationApi* | [**lookupIP**](docs/Api/IPGeolocationApi.md#lookupip) | **GET** /v1/ip/{address} | IP geolocation lookup
*IPGeolocationApi* | [**lookupMyIP**](docs/Api/IPGeolocationApi.md#lookupmyip) | **GET** /v1/ip/me | Caller&#39;s IP geolocation
*PostalCodesApi* | [**listPostalCodes**](docs/Api/PostalCodesApi.md#listpostalcodes) | **GET** /v1/postal-codes | List postal codes
*PostalCodesApi* | [**nearestPostalCode**](docs/Api/PostalCodesApi.md#nearestpostalcode) | **GET** /v1/postal-codes/nearest | Find nearest postal codes
*RegionsApi* | [**getRegion**](docs/Api/RegionsApi.md#getregion) | **GET** /v1/regions/{id} | Get region by ID
*RegionsApi* | [**listRegionCities**](docs/Api/RegionsApi.md#listregioncities) | **GET** /v1/regions/{id}/cities | List cities in a region
*RegionsApi* | [**listRegions**](docs/Api/RegionsApi.md#listregions) | **GET** /v1/regions | List regions
*RegionsApi* | [**regionChildren**](docs/Api/RegionsApi.md#regionchildren) | **GET** /v1/regions/{id}/children | List child cities of a region
*SearchApi* | [**autocomplete**](docs/Api/SearchApi.md#autocomplete) | **GET** /v1/autocomplete | Autocomplete search
*SearchApi* | [**resolveCoordinate**](docs/Api/SearchApi.md#resolvecoordinate) | **GET** /v1/resolve | Resolve coordinates to their containing administrative areas
*SearchApi* | [**reverseGeocode**](docs/Api/SearchApi.md#reversegeocode) | **GET** /v1/reverse | Reverse geocode coordinates
*SearchApi* | [**search**](docs/Api/SearchApi.md#search) | **GET** /v1/search | Cross-type search
*TimezonesApi* | [**getTimezone**](docs/Api/TimezonesApi.md#gettimezone) | **GET** /v1/timezones/{tzId} | Get timezone by IANA ID
*TimezonesApi* | [**listTimezones**](docs/Api/TimezonesApi.md#listtimezones) | **GET** /v1/timezones | List timezones

## Models

- [AutocompleteListResponse](docs/Model/AutocompleteListResponse.md)
- [AutocompleteResult](docs/Model/AutocompleteResult.md)
- [BatchRequest](docs/Model/BatchRequest.md)
- [Boundary](docs/Model/Boundary.md)
- [BoundarySingleResponse](docs/Model/BoundarySingleResponse.md)
- [City](docs/Model/City.md)
- [CityListResponse](docs/Model/CityListResponse.md)
- [CitySingleResponse](docs/Model/CitySingleResponse.md)
- [Country](docs/Model/Country.md)
- [CountryListResponse](docs/Model/CountryListResponse.md)
- [CountryRef](docs/Model/CountryRef.md)
- [CountrySingleResponse](docs/Model/CountrySingleResponse.md)
- [ErrorResponse](docs/Model/ErrorResponse.md)
- [ErrorResponseError](docs/Model/ErrorResponseError.md)
- [ErrorResponseErrorDetailsInner](docs/Model/ErrorResponseErrorDetailsInner.md)
- [GeoJSONGeometry](docs/Model/GeoJSONGeometry.md)
- [GeoJSONMultiPolygon](docs/Model/GeoJSONMultiPolygon.md)
- [GetStatus200Response](docs/Model/GetStatus200Response.md)
- [GetStatus200ResponseData](docs/Model/GetStatus200ResponseData.md)
- [HierarchyListResponse](docs/Model/HierarchyListResponse.md)
- [HierarchyNode](docs/Model/HierarchyNode.md)
- [IPResult](docs/Model/IPResult.md)
- [IPResultCity](docs/Model/IPResultCity.md)
- [IPResultContinent](docs/Model/IPResultContinent.md)
- [IPResultCountry](docs/Model/IPResultCountry.md)
- [IPResultLocation](docs/Model/IPResultLocation.md)
- [IPResultPostal](docs/Model/IPResultPostal.md)
- [IPResultRegion](docs/Model/IPResultRegion.md)
- [IPSingleResponse](docs/Model/IPSingleResponse.md)
- [NearbyCity](docs/Model/NearbyCity.md)
- [NearbyCityListResponse](docs/Model/NearbyCityListResponse.md)
- [PaginationMeta](docs/Model/PaginationMeta.md)
- [PostalCode](docs/Model/PostalCode.md)
- [PostalCodeListResponse](docs/Model/PostalCodeListResponse.md)
- [QuotaDetail](docs/Model/QuotaDetail.md)
- [Region](docs/Model/Region.md)
- [RegionListResponse](docs/Model/RegionListResponse.md)
- [RegionRef](docs/Model/RegionRef.md)
- [RegionSingleResponse](docs/Model/RegionSingleResponse.md)
- [ReverseGeocodeResult](docs/Model/ReverseGeocodeResult.md)
- [ReverseGeocodeSingleResponse](docs/Model/ReverseGeocodeSingleResponse.md)
- [SearchListResponse](docs/Model/SearchListResponse.md)
- [SearchResult](docs/Model/SearchResult.md)
- [Timezone](docs/Model/Timezone.md)
- [TimezoneListResponse](docs/Model/TimezoneListResponse.md)
- [TimezoneSingleResponse](docs/Model/TimezoneSingleResponse.md)
- [UpgradeDetail](docs/Model/UpgradeDetail.md)

## Authorization

Authentication schemes defined for the API:
### apiKeyAuth

- **Type**: API key
- **API key parameter name**: X-API-Key
- **Location**: HTTP header


## Tests

To run the tests, use:

```bash
composer install
vendor/bin/phpunit
```

## Author



## About this package

This PHP package is automatically generated by the [OpenAPI Generator](https://openapi-generator.tech) project:

- API version: `1.2.1`
    - Package version: `1.2.1`
    - Generator version: `7.21.0`
- Build package: `org.openapitools.codegen.languages.PhpClientCodegen`
