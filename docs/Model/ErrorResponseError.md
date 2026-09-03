# ErrorResponseError

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**code** | **string** |  |
**message** | **string** |  |
**details** | [**\GeoSearch\Model\ErrorResponseErrorDetailsInner[]**](ErrorResponseErrorDetailsInner.md) |  | [optional]
**request_id** | **string** | Correlation identifier present on every error response. Quote this when contacting support. |
**trace_id** | **string** | W3C trace ID of the distributed trace for this request, when tracing is enabled. Omitted entirely when no span was recording, so clients must treat it as optional. It complements rather than replaces &#x60;request_id&#x60;. | [optional]
**quota** | [**\GeoSearch\Model\QuotaDetail**](QuotaDetail.md) |  | [optional]
**upgrade** | [**\GeoSearch\Model\UpgradeDetail**](UpgradeDetail.md) |  | [optional]

[[Back to Model list]](../../README.md#models) [[Back to API list]](../../README.md#endpoints) [[Back to README]](../../README.md)
