# GeoJSONGeometry

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**type** | **string** | &#x60;MultiPolygon&#x60; for most areas, &#x60;Polygon&#x60; for areas with a single ring — including areas that BECOME single-ring under &#x60;?simplify&#x3D;&#x60;. Do not pin this to one value. |
**coordinates** | **mixed[]** | Nesting depth depends on &#x60;type&#x60;: three levels for &#x60;Polygon&#x60;, four for &#x60;MultiPolygon&#x60;. Positions are &#x60;[longitude, latitude]&#x60; in EPSG:4326, per the GeoJSON specification. |

[[Back to Model list]](../../README.md#models) [[Back to API list]](../../README.md#endpoints) [[Back to README]](../../README.md)
