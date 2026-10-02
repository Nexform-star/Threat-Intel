# Threat Intelligence Report: Discord Inject Logger

## 1. Objective

Analyze a Lua script identified in a GitHub repository to determine its behavior, collected information, external communication mechanisms, and relevant technical indicators.

The analysis was performed through static analysis and Git history review. The obfuscated script was not executed.

## 2. Sample

* Language: Lua
* Obfuscator: MoonVeil 2.0.25
* File size: approximately 217 KB
* Format: heavily obfuscated Lua script
* https://github.com/FF3MOD/87UT

The script explicitly identifies itself as being generated using:

`MoonVeil 2.0.25`

## 3. Inject Logger

A component explicitly labelled:

`-- Inject Logger`

was identified in the source code.

The component initializes Roblox services including:

* `HttpService`
* `Players`
* `MarketplaceService`

It then obtains the local player through:

`Players.LocalPlayer`

## 4. Collected Information

The logger collects several pieces of information:

| Data            | Method                                                 |
| --------------- | ------------------------------------------------------ |
| Roblox username | `player.Name`                                          |
| Game name       | `MarketplaceService:GetProductInfo(game.PlaceId).Name` |
| Key             | `getgenv().KEY`                                        |
| Timestamp       | `os.date("!%Y-%m-%d %H:%M:%S")`                        |

If the `KEY` value is unavailable, the script uses:

`Unknown`

## 5. Data Transmission

The collected information is encoded using:

`HttpService:JSONEncode()`

The resulting JSON data is then transmitted using:

`HttpService:PostAsync()`

The destination is a hardcoded Discord webhook.

The generated Discord embed contains the following fields:

* `👤 Username`
* `🎮 Game`
* `🔑 Key`
* `🕒 Time (UTC)`

The embed title is:

`📥 New Inject`

## 6. Discord Webhook

A Discord webhook URL is embedded directly in the source code.

During analysis, the endpoint was found to still accept requests.

The complete webhook URL is omitted from this report to avoid republishing an exposed credential.

The webhook therefore functions as an external destination for the information collected by the logger.

## 7. Historical Analysis

Git history shows previous versions of the logger component.

An earlier version contains the same functionality in a more readable form, making the collection and transmission mechanisms directly observable.

The historical version explicitly constructs the Discord payload and calls `HttpService:PostAsync()`.

This provides additional evidence for the behavior identified in the current source.

## 8. Obfuscation

The main Lua script is heavily obfuscated.

Observed characteristics include:

* very large source file;
* heavily compressed code;
* one-character variable names;
* indirect table indexing;
* nested functions;
* obfuscated control flow;
* encoded values;
* extensive use of function wrappers.

The file identifies MoonVeil 2.0.25 as the tool used to generate the obfuscated code.

## 9. Technical Indicators

### Roblox APIs

* `HttpService`
* `Players`
* `MarketplaceService`

### Network

* Discord webhook
* HTTP POST through `HttpService:PostAsync()`

### Collected Data

* Roblox username
* Game name
* `KEY` value
* UTC timestamp

### Obfuscation

* MoonVeil 2.0.25

## 10. MITRE ATT&CK Mapping

| Technique | Description                     |
| --------- | ------------------------------- |
| T1027     | Obfuscated Files or Information |
| T1041     | Exfiltration Over C2 Channel    |

The mapping is based on behavior directly observable in the analyzed source.

## 11. Technical Assessment

The analyzed code contains a data-collection component capable of collecting Roblox session information and transmitting it to an external Discord webhook.

The collection fields and transmission mechanism are directly observable in the source code.

The presence of the webhook and `PostAsync()` call demonstrates the transmission capability. Static analysis alone does not establish that the code was successfully executed against a specific user.

## 12. Conclusion

The investigation identified an `Inject Logger` component embedded within a heavily obfuscated Lua script.

The component collects a Roblox username, game name, executor/environment `KEY`, and UTC timestamp before transmitting the information to an external Discord webhook.

Historical Git content provides a less-obfuscated version of the same functionality, making the data collection and transmission behavior directly verifiable.

The findings are based on publicly available source code and Git history. No execution of the obfuscated script was performed during the analysis.

## 13. Limitations

This analysis is based on publicly available repository content, static analysis, and Git history.

The report documents observable code capabilities and does not establish successful execution against a specific user.

No attribution to a specific individual or organization is made solely from these findings.
