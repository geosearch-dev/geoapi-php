# Country

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **int** |  | [optional]
**geoname_id** | **int** |  | [optional]
**iso_code** | **string** |  | [optional]
**iso3_code** | **string** |  | [optional]
**iso_numeric** | **int** |  | [optional]
**fips_code** | **string** |  | [optional]
**name** | **string** |  | [optional]
**capital** | **string** |  | [optional]
**area_sq_km** | **float** |  | [optional]
**population** | **int** |  | [optional]
**continent_code** | **string** |  | [optional]
**tld** | **string** |  | [optional]
**currency_code** | **string** |  | [optional]
**currency_name** | **string** |  | [optional]
**phone** | **string** |  | [optional]
**postal_code_format** | **string** |  | [optional]
**postal_code_regex** | **string** |  | [optional]
**languages** | **string[]** |  | [optional]
**neighbours** | **string[]** |  | [optional]
**latitude** | **float** |  | [optional]
**longitude** | **float** |  | [optional]
**flag_emoji** | **string** |  | [optional]
**geometry** | [**\GeoAPI\Model\GeoJSONMultiPolygon**](GeoJSONMultiPolygon.md) | Country boundary. Returned by default on &#x60;GET /v1/countries/{code}&#x60; and on request via &#x60;?fields&#x3D;geometry&#x60; on &#x60;GET /v1/countries&#x60;.  NOT TIER-GATED. Country geometry is served on every plan, including Free. Region geometry is gated — see the &#x60;Region&#x60; schema. | [optional]

[[Back to Model list]](../../README.md#models) [[Back to API list]](../../README.md#endpoints) [[Back to README]](../../README.md)
