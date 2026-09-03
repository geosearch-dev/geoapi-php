# Boundary

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**geoname_id** | **int** | The area the polygon belongs to, read back from the source row rather than echoed from the request. |
**name** | **string** | The area&#39;s name, resolved through &#x60;?lang&#x3D;&#x60; when supplied. |
**type** | **string** | Which kind of area this is. |
**geometry** | [**\GeoSearch\Model\GeoJSONGeometry**](GeoJSONGeometry.md) |  |
**simplify** | **float** | The tolerance that was ACTUALLY APPLIED, or &#x60;null&#x60; for full precision.  THIS IS NOT YOUR &#x60;?simplify&#x3D;&#x60; ECHOED BACK. A requested tolerance of &#x60;0&#x60; is dropped rather than executed, so &#x60;?simplify&#x3D;0&#x60; returns &#x60;null&#x60; here — that is the truthful answer, because no simplification was performed. Read this field rather than assuming the request was honoured verbatim. |

[[Back to Model list]](../../README.md#models) [[Back to API list]](../../README.md#endpoints) [[Back to README]](../../README.md)
