# Region

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **int** |  | [optional]
**geoname_id** | **int** |  | [optional]
**country_code** | **string** |  | [optional]
**admin_code** | **string** |  | [optional]
**name** | **string** |  | [optional]
**ascii_name** | **string** |  | [optional]
**level** | **int** |  | [optional]
**parent_geoname_id** | **int** |  | [optional]
**population** | **int** |  | [optional]
**latitude** | **float** |  | [optional]
**longitude** | **float** |  | [optional]
**country** | [**\GeoSearch\Model\CountryRef**](CountryRef.md) |  | [optional]
**geometry** | [**\GeoSearch\Model\GeoJSONMultiPolygon**](GeoJSONMultiPolygon.md) | Region boundary. Returned by default on &#x60;GET /v1/regions/{id}&#x60;, and on request via &#x60;?fields&#x3D;geometry&#x60; on &#x60;GET /v1/regions&#x60; and &#x60;GET /v1/countries/{code}/regions&#x60;.  REQUIRES A PAID PLAN. On all three of those routes this key is OMITTED ENTIRELY for a Free-tier key — absent, not null, with a 200 status and no error. A client reading &#x60;data.geometry.type&#x60; unconditionally will fail on a null dereference.  To be told explicitly rather than silently, request the polygon from &#x60;GET /v1/boundaries/{geoname_id}&#x60;, which answers a Free key with a 403 and an upgrade link. | [optional]

[[Back to Model list]](../../README.md#models) [[Back to API list]](../../README.md#endpoints) [[Back to README]](../../README.md)
