---
title: Translation Service API Reference

language_tabs:
  - shell

toc_footers:

search: true
---

# Introduction

## translate.content-service.org
Service is used for text translation and caching translation. Translation Service contains a single endpoint for translation with the following parameters: text for translation, source and destination languages, an engine that will be called to translate text. Currently, supported engines are Google and Deepl. If text provided for translation is already cached it will be sent back without calling engine for translation, otherwise, the specified engine is called and translated text is returned and also cached for future calls. Authorization is done using an Access Token provided in 'Authorization' header.<br />
Service returns a translated text with additionals data in JSON format (see Examples below).

## Base URL

  https://translate.content-service.org

## Translation endpoint (URL)

  https://translate.content-service.org/api/process_translation

## HTTP Method Call
`GET` method is used to request translation from a service.

# Authentication

Authorization is done using Access Token provided by us.<br />
Provided token has to be present in _'Authorization'_ header for each request (see examples below).<br />

Example of specifing access token in header: <br />
`Authorization: [access_token]`

<aside class="notice">
You must replace <code>[access_token]</code> with your personal API key.
</aside>


> To test authentication, you can use follwing endpoint:

```shell
# With shell, you can just pass the correct header with each request
curl "https://translate.content-service.org/api/ping" \
  -H "Authorization: XXXX"

# Response
{"data":{"message":"TUI Translations Service"}}
```

> Make sure to replace `XXXX` with your API key.

# URL Params

Required params for translation for each request:

  `sentence=[string]`<br />
  Sentence for translation
  
  `source=[string]`<br />
  Source language, depends on on translation engine.
  
  `target=[string]`<br />
  Target language, depends on on translation engine.
  
  `engine=[string]`<br />
  This could be google, deepl or bing.

# HTTP Responses

## Success Response
HTTP Status Code of successful response <br />

* **Code:** 200 <br />

## Error Response
HTTP Status Codes of unsuccessful response (see examples below) <br />

  * **Code:** 401 UNAUTHORIZED <br />
  * **Code:** 401 TOKEN IS MISSING <br />
  * **Code:** 401 INVALID TOKEN <br />
  * **Code:** 422 UNPROCESSABLE ENTITY  Often caused by missing required parameters<br />
  * **Code:** 500 INTERNAL SERVER ERROR <br />

# Supported Languages

## Google Supported Languages
List of supported languages by Google engine.

<table><tbody><tr style="font-weight:bold"><td>Language Name</td><td>Code</td><td>Language Name</td><td>Language Code</td></tr><tr><td>Afrikaans</td><td>af</td><td>Irish</td><td>ga</td></tr><tr><td>Albanian</td><td>sq</td><td>Italian</td><td>it</td></tr><tr><td>Arabic</td><td>ar</td><td>Japanese</td><td>ja</td></tr><tr><td>Azerbaijani</td><td>az</td><td>Kannada</td><td>kn</td></tr><tr><td>Basque</td><td>eu</td><td>Korean</td><td>ko</td></tr><tr><td>Bengali</td><td>bn</td><td>Latin</td><td>la</td></tr><tr><td>Belarusian</td><td>be</td><td>Latvian</td><td>lv</td></tr><tr><td>Bulgarian</td><td>bg</td><td>Lithuanian</td><td>lt</td></tr><tr><td>Catalan</td><td>ca</td><td>Macedonian</td><td>mk</td></tr><tr><td>Chinese Simplified</td><td>zh-CN</td><td>Malay</td><td>ms</td></tr><tr><td>Chinese Traditional</td><td>zh-TW</td><td>Maltese</td><td>mt</td></tr><tr><td>Croatian</td><td>hr</td><td>Norwegian</td><td>no</td></tr><tr><td>Czech</td><td>cs</td><td>Persian</td><td>fa</td></tr><tr><td>Danish</td><td>da</td><td>Polish</td><td>pl</td></tr><tr><td>Dutch</td><td>nl</td><td>Portuguese</td><td>pt</td></tr><tr><td>English</td><td>en</td><td>Romanian</td><td>ro</td></tr><tr><td>Esperanto</td><td>eo</td><td>Russian</td><td>ru</td></tr><tr><td>Estonian</td><td>et</td><td>Serbian</td><td>sr</td></tr><tr><td>Filipino</td><td>tl</td><td>Slovak</td><td>sk</td></tr><tr><td>Finnish</td><td>fi</td><td>Slovenian</td><td>sl</td></tr><tr><td>French</td><td>fr</td><td>Spanish</td><td>es</td></tr><tr><td>Galician</td><td>gl</td><td>Swahili</td><td>sw</td></tr><tr><td>Georgian</td><td>ka</td><td>Swedish</td><td>sv</td></tr><tr><td>German</td><td>de</td><td>Tamil</td><td>ta</td></tr><tr><td>Greek</td><td>el</td><td>Telugu</td><td>te</td></tr><tr><td>Gujarati</td><td>gu</td><td>Thai</td><td>th</td></tr><tr><td>Haitian Creole</td><td>ht</td><td>Turkish</td><td>tr</td></tr><tr><td>Hebrew</td><td>iw</td><td>Ukrainian</td><td>uk</td></tr><tr><td>Hindi</td><td>hi</td><td>Urdu</td><td>ur</td></tr><tr><td>Hungarian</td><td>hu</td><td>Vietnamese</td><td>vi</td></tr><tr><td>Icelandic</td><td>is</td><td>Welsh</td><td>cy</td></tr><tr><td>Indonesian</td><td>id</td><td>Yiddish</td><td>yi</td></tr></tbody></table>

## Deepl Supported Languages
List of supported languages by Deepl engine |
--------- |
EN,  DE,  FR,  ES,  IT,  NL,  PL |

# Examples

## Testing API endpoint
Endpoint for testing API response from online service. Just for testing purpose.

#### HTTP Request

`GET https://translate.content-service.org/api/ping`

#### JSON Response
`{"data":{"message":"Translations Service"}}`


<aside class="success">
Remember — access token has to be set in a `Authorization` header!
</aside>

```shell
curl -H 'Authorization: XXXX' https://translate.content-service.org/api/ping

# JSON Response
{"data":{"message":"Translations Service"}}
```

> Make sure to replace `XXXX` with your API key.

## Translate using Deepl engine
Examples of different types of calls to the Translation Service when Deepl engine is used.

<aside class="success">
Remember — access token has to be set in a `Authorization` header!
</aside>

### Example 1
Translating text when the English language is a source language and German language is a target language.

```shell
# Example 1
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=de&engine=deepl' \
--header 'Authorization: XXXX'

# JSON Response
{"data":{"cache_miss":0,"cache_hit":4,"translated_chars":0,"translation":"Zehn"}}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=de&engine=deepl`

#### JSON Response
`{"data":{"cache_miss":0,"cache_hit":4,"translated_chars":0,"translation":"Zehn"}}`

### Example 2
Translating text when the English language is a source language and French language is a target language.

```shell
# Example 2
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=fr&engine=deepl' \
--header 'Authorization: XXXX'

# JSON Response
{"data":{"cache_miss":0,"cache_hit":3,"translated_chars":0,"translation":"Dix"}}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=fr&engine=deepl`

#### JSON Response
`{"data":{"cache_miss":0,"cache_hit":3,"translated_chars":0,"translation":"Dix"}}`

### Example 3
Translating long sentence when the English language is a source language and German language is a target language.

```shell
# Example 3
curl -G "https://translate.content-service.org/api/process_translation?source=en&target=de&engine=deepl" \
--data-urlencode "sentence=The accomplishment of an aim or purpose" \
--header 'Authorization: XXXX'

# JSON Response
{"data":{"cache_miss":0,"cache_hit":38,"translated_chars":0,"translation":"Die Erreichung eines Ziels oder Zwecks"}}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence="The accomplishment of an aim or purpose"&source=en&target=de&engine=deepl`

#### JSON Response
`{"data":{"cache_miss":0,"cache_hit":38,"translated_chars":0,"translation":"Die Erreichung eines Ziels oder Zwecks"}}`

### Example 4
Translation Service response when _'sentence'_ params is missing in URL.

```shell
# Example 4
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?source=en&target=fr&engine=deepl' \
--header 'Authorization: XXXX'

# Response headers
HTTP/1.1 422 Unprocessable Entity
# JSON Response
{"message":"Required params are missing"}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?source=en&target=fr&engine=deepl`

#### JSON Response
{"message":"Required params are missing"}

### Example 5
Translation Service response when _'engine'_ params is missing in URL.

```shell
# Example 5
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=fr' \
--header 'Authorization: XXXX'

# Response headers
HTTP/1.1 422 Unprocessable Entity
# JSON Response
{"message":"Required params are missing"}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=fr`

#### JSON Response
{"message":"Required params are missing"}

### Example 6
Translation Service response when _'source'_ params is missing in URL.

```shell
# Example 6
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?sentence=Ten&target=fr&engine=deepl' \
--header 'Authorization: XXXX'

# Response headers
HTTP/1.1 422 Unprocessable Entity
# JSON Response
{"message":"Required params are missing"}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Ten&target=fr&engine=deepl`

#### JSON Response
{"message":"Required params are missing"}

### Example 7
Translation Service response when _'target'_ params is missing in URL.

```shell
# Example 7
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&engine=deepl' \
--header 'Authorization: XXXX'

# Response headers
HTTP/1.1 422 Unprocessable Entity
# JSON Response
{"message":"Required params are missing"}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&engine=deepl`

#### JSON Response
{"message":"Required params are missing"}

## Translate using Google engine
Examples of different types of calls to the Translation Service when Google engine is used.

<aside class="success">
Remember — access token has to be set in a `Authorization` header!
</aside>

### Example 1
Translating text when the English language is a source language and German language is a target language.

```shell
# Example 1
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=de&engine=google' \
--header 'Authorization: XXXX'

# JSON Response
{"data":{"cache_miss":0,"cache_hit":4,"translated_chars":0,"translation":"Zehn"}}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=de&engine=google`

#### JSON Response
`{"data":{"cache_miss":0,"cache_hit":4,"translated_chars":0,"translation":"Zehn"}}`

### Example 2
Translating text when the English language is a source language and French language is a target language.

```shell
# Example 2
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=fr&engine=google' \
--header 'Authorization: XXXX'

# JSON Response
{"data":{"cache_miss":0,"cache_hit":3,"translated_chars":0,"translation":"Dix"}}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=fr&engine=google`

#### JSON Response
`{"data":{"cache_miss":0,"cache_hit":3,"translated_chars":0,"translation":"Dix"}}`

### Example 3
Translating long sentence when the English language is a source language and German language is a target language.

```shell
# Example 3
curl -G "https://translate.content-service.org/api/process_translation?source=en&target=de&engine=google" \
--data-urlencode "sentence=The accomplishment of an aim or purpose" \
--header 'Authorization: XXXX'

# JSON Response
{"data":{"cache_miss":0,"cache_hit":38,"translated_chars":0,"translation":"Die Erreichung eines Ziels oder Zwecks"}}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?source=en&target=de&engine=google`

#### JSON Response
`{"data":{"cache_miss":0,"cache_hit":38,"translated_chars":0,"translation":"Die Erreichung eines Ziels oder Zwecks"}}`

### Example 4
Translation Service response when _'sentence'_ params is missing in URL.

```shell
# Example 4
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?source=en&target=fr&engine=google' \
--header 'Authorization: XXXX'

# Response headers
HTTP/1.1 422 Unprocessable Entity
# JSON Response
{"message":"Required params are missing"}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?source=en&target=fr&engine=google`

#### JSON Response
`{"message":"Required params are missing"}`

### Example 5
Translation Service response when _'engine'_ params is missing in URL.

```shell
# Example 5
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=fr' \
--header 'Authorization: XXXX'

# Response headers
HTTP/1.1 422 Unprocessable Entity
# JSON Response
{"message":"Required params are missing"}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Ten&source=en&target=fr`

#### JSON Response
`{"message":"Required params are missing"}`

### Example 6
Translation Service response when _'source'_ params is missing in URL.

```shell
# Example 7
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?sentence=Ten&target=fr&engine=google' \
--header 'Authorization: XXXX'

# Response headers
HTTP/1.1 422 Unprocessable Entity
# JSON Response
{"message":"Required params are missing"}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Ten&target=fr&engine=google`

#### JSON Response
`{"message":"Required params are missing"}`

### Example 7
Translation Service response when _'target'_ params is missing in URL.

```shell
# Example 7
curl --request GET \
--url 'https://translate.content-service.org/api/process_translation?sentence=Ten&source=fr&engine=google' \
--header 'Authorization: XXXX'

# Response headers
HTTP/1.1 422 Unprocessable Entity
# JSON Response
{"message":"Required params are missing"}
```
> Make sure to replace `XXXX` with your API key.

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Ten&source=fr&engine=google`

#### JSON Response
`{"message":"Required params are missing"}`

## Unauthorized Request

### Token is Missing
Translation Service response when Access Token is not provided in '_Authorization_' header.

```shell
# Token is Missing
curl -i -H "Accept: aplication/json" 'https://translate.content-service.org/api/process_translation?sentence=Hello&source=en&target=de&engine=deepl'

# Response headers
HTTP/1.1 401 Unauthorized
# JSON Response  
{"message":"Token is missing"}
```

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Hello&source=en&target=de&engine=deepl`

#### JSON Response
`{"message":"Token is missing"}`

### Invalid Token
Translation Service response when provided Access Token is not valid.

```shell
# Invalid Token
curl -i -H "Accept: aplication/json" 'https://translate.content-service.org/api/process_translation?sentence=Hello&source=en&target=de&engine=deepl' \
--header 'Authorization: 123'

# Response headers
HTTP/1.1 401 Unauthorized
# JSON Response  
{"message":"Invalid token"}
```

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Hello&source=en&target=de&engine=deepl`

#### JSON Response
`{"message":"Invalid token"}`

## Internal Server Error
Translation Service response when internal server occurs.

```shell
# Internal Server Error
curl -i -H "Accept: aplication/json" 'https://translate.content-service.org/api/process_translation?sentence=Hello&source=en&target=de&engine=deepl' \
--header 'Authorization: 1234'

# Response headers
HTTP/1.1 500 Internal server error
# JSON Response  
{"message": "Internal server error"}
```

#### HTTP Request

`GET https://translate.content-service.org/api/process_translation?sentence=Hello&source=en&target=de&engine=deepl`

#### JSON Response
`{"message": "Internal server error"}`

# FAQ

<p><b>As far as I can see each request can only be done for one pair of source language – target language. Is it correct? Or could we eventually send in a single request one source language and more than one target languages? If not, are you considering it for future developments?</b>
<p>Yes, on pair. But it is already on our feature wishlist.</p>

<p><b>Since we still need access to be able to do our own tests, could you please send us a sample response? Or does it just contain the translated string?</b></p>
<p>You can see a sample response on the right side: <a href="https://translate-documentation.content-service.org/#translate-using-deepl-engine">https://translate-documentation.content-service.org/#translate-using-deepl-engine</a></p>

<p><b>What are the availability (uptime) SLOs of the service? We would need to have it online at any given time.</b></p>
<p>Always on.</p>

<p><b>How is the performance of the service? What are the mean response times?</b></p>
<p>We are adding 20ms on top of external translation services. The response time of external services vary. If we already have that translation, its only 20ms.</p>

<p><b>Using a single account, could we launch several requests in parallel? Or would we need to send them sequentially?</b></p>
<p>You can do this parallel. Restrictions and rate limits may impact you. Don't do more than 4-6 translations in parallel.</p>

<p><b>If there is any, what is the maximum size of a string to be translated? I am asking this because we currently have some descriptions for Orlando with around 10k characters.</b></p>
<p>There is no limit. However we have a maximum processing time of 30s - if an external translation service take longer than 30s the connection is killed.</p>
