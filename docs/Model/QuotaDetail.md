# QuotaDetail

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**limit** | **int** | Monthly request allowance for the account&#39;s current plan. |
**used** | **int** | Requests consumed in the current quota period. |
**resets_at** | **\DateTime** | Start of the next quota period, when &#x60;used&#x60; returns to zero. Matches the &#x60;X-RateLimit-Reset&#x60; header on the same response, expressed as RFC 3339 rather than an epoch second. |
**upgrade_url** | **string** | Absolute URL of the billing page where the plan can be raised. Derived server-side from configuration and never reflected from a request header or parameter. |

[[Back to Model list]](../../README.md#models) [[Back to API list]](../../README.md#endpoints) [[Back to README]](../../README.md)
