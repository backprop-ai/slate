---
title: Kiri Model API v1.0.0
language_tabs:
  - shell: shell
  - python: python
  - javascript: javascript
language_clients:
  - shell: ""
  - python: ""
  - javascript: ""
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="kiri-model-api">Kiri Model API v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

Welcome to our API documentation! Things to note:

  - Most endpoints can take both single and batched requests. This is so you can save time on round trip times speed up your inference when working with more data. The different `body` and `response` variants are shown in the respective `single` and `batch` schemas.
  
  - All endpoints require authentication with your API key in the `x-api-key` header.
  
  - Some endpoints may have multiple `model` options. This is useful to know if your task is in a language other than English.
  
  - Every account gets `2000` seconds of free inference every month. Seconds are calculated only for compute time when using the endpoints.
  
If anything is unclear or you find that something is not working as intended, please get in touch!

Base URLs:

* <a href="https://api.kiri.ai">https://api.kiri.ai</a>

Email: <a href="mailto:hello@kiri.ai">Support</a> 
License: <a href="http://www.apache.org/licenses/LICENSE-2.0.html">Apache 2.0</a>

# Authentication

* API Key (ApiKeyAuth)
    - Parameter Name: **x-api-key**, in: header. 

<h1 id="kiri-model-api-tasks">Tasks</h1>

Endpoints to call tasks that implement various models for your use cases.

## vectorisation

<a id="opIdvectorisation"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.kiri.ai/vectorisation \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"text":"iPhone 12 128GB","model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.kiri.ai")

payload = "{\"text\":\"iPhone 12 128GB\",\"model\":\"english\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/vectorisation", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = JSON.stringify({
  "text": "iPhone 12 128GB",
  "model": "english"
});

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.kiri.ai/vectorisation");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /vectorisation`

vectorises string or list of strings

> Body parameter

```json
{
  "text": "iPhone 12 128GB",
  "model": "english"
}
```

<h3 id="vectorisation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[VectorisationBody](#schemavectorisationbody)|true|text or list of text to vectorise|

> Example responses

> 200 Response

```json
{
  "vector": [
    0.92949192,
    0.2312301
  ]
}
```

<h3 id="vectorisation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successfully vectorised|[VectorisationResponse](#schemavectorisationresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## question answering

<a id="opIdqa"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.kiri.ai/qa \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"question":"What is the meaning of life?","context":"The meaning of life is 42.","prev_q":["What is not the meaning of life?"],"prev_a":["unknown"],"model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.kiri.ai")

payload = "{\"question\":\"What is the meaning of life?\",\"context\":\"The meaning of life is 42.\",\"prev_q\":[\"What is not the meaning of life?\"],\"prev_a\":[\"unknown\"],\"model\":\"english\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/qa", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = JSON.stringify({
  "question": "What is the meaning of life?",
  "context": "The meaning of life is 42.",
  "prev_q": [
    "What is not the meaning of life?"
  ],
  "prev_a": [
    "unknown"
  ],
  "model": "english"
});

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.kiri.ai/qa");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /qa`

Performs QA on question, context, previous questions and previous answers. Answers "unknown" if the question cannot be answered.

> Body parameter

```json
{
  "question": "What is the meaning of life?",
  "context": "The meaning of life is 42.",
  "prev_q": [
    "What is not the meaning of life?"
  ],
  "prev_a": [
    "unknown"
  ],
  "model": "english"
}
```

<h3 id="question-answering-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[QABody](#schemaqabody)|true|none|

> Example responses

> 200 Response

```json
{
  "answer": "42"
}
```

<h3 id="question-answering-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful QA|[QAResponse](#schemaqaresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## zero shot classification

<a id="opIdclassification"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.kiri.ai/classification \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"text":"I am really mad because my product broke.","labels":["product issue","furniture","space"],"model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.kiri.ai")

payload = "{\"text\":\"I am really mad because my product broke.\",\"labels\":[\"product issue\",\"furniture\",\"space\"],\"model\":\"english\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/classification", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = JSON.stringify({
  "text": "I am really mad because my product broke.",
  "labels": [
    "product issue",
    "furniture",
    "space"
  ],
  "model": "english"
});

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.kiri.ai/classification");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /classification`

Performs zero shot classification on provided text and labels.

> Body parameter

```json
{
  "text": "I am really mad because my product broke.",
  "labels": [
    "product issue",
    "furniture",
    "space"
  ],
  "model": "english"
}
```

<h3 id="zero-shot-classification-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ClassificationBody](#schemaclassificationbody)|true|none|

> Example responses

> 200 Response

```json
{
  "probabilities": {
    "product issue": 0.98,
    "furniture": 0.1,
    "space": 0.05
  }
}
```

<h3 id="zero-shot-classification-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful classification|[ClassificationResponse](#schemaclassificationresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## zero shot image classification

<a id="opIdimage-classification"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.kiri.ai/image-classification \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"image":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABpUAAATOCAYAAAA","labels":["healthy brain","brain with tumor"],"model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.kiri.ai")

payload = "{\"image\":\"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABpUAAATOCAYAAAA\",\"labels\":[\"healthy brain\",\"brain with tumor\"],\"model\":\"english\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/image-classification", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = JSON.stringify({
  "image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABpUAAATOCAYAAAA",
  "labels": [
    "healthy brain",
    "brain with tumor"
  ],
  "model": "english"
});

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.kiri.ai/image-classification");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /image-classification`

Performs zero shot image classification on provided base64 encoded image and labels. The probabilities predicted for the labels will always sum to 100%.

> Body parameter

```json
{
  "image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABpUAAATOCAYAAAA",
  "labels": [
    "healthy brain",
    "brain with tumor"
  ],
  "model": "english"
}
```

<h3 id="zero-shot-image-classification-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ImageClassificationBody](#schemaimageclassificationbody)|true|none|

> Example responses

> 200 Response

```json
{
  "probabilities": {
    "brain with tumor": 0.98,
    "healthy brain": 0.02
  }
}
```

<h3 id="zero-shot-image-classification-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful classification|[ImageClassificationResponse](#schemaimageclassificationresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## text generation

<a id="opIdgeneration"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.kiri.ai/generation \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"text":"Geralt knew the signs, the monster was a","min_length":10,"max_length":20,"temperature":1,"top_k":0,"top_p":1,"repetition_penalty":1,"length_penalty":1,"num_beams":1,"num_generations":1,"model":"gpt2-large"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.kiri.ai")

payload = "{\"text\":\"Geralt knew the signs, the monster was a\",\"min_length\":10,\"max_length\":20,\"temperature\":1,\"top_k\":0,\"top_p\":1,\"repetition_penalty\":1,\"length_penalty\":1,\"num_beams\":1,\"num_generations\":1,\"model\":\"gpt2-large\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/generation", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = JSON.stringify({
  "text": "Geralt knew the signs, the monster was a",
  "min_length": 10,
  "max_length": 20,
  "temperature": 1,
  "top_k": 0,
  "top_p": 1,
  "repetition_penalty": 1,
  "length_penalty": 1,
  "num_beams": 1,
  "num_generations": 1,
  "model": "gpt2-large"
});

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.kiri.ai/generation");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /generation`

Performs generation on the provided text with the specified parameters

> Body parameter

```json
{
  "text": "Geralt knew the signs, the monster was a",
  "min_length": 10,
  "max_length": 20,
  "temperature": 1,
  "top_k": 0,
  "top_p": 1,
  "repetition_penalty": 1,
  "length_penalty": 1,
  "num_beams": 1,
  "num_generations": 1,
  "model": "gpt2-large"
}
```

<h3 id="text-generation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[GenerationBody](#schemagenerationbody)|true|none|

> Example responses

> 200 Response

```json
{
  "output": "Geralt knew the signs, the monster was a vampire that day; after the siege her companions"
}
```

<h3 id="text-generation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful generation|[GenerationResponse](#schemagenerationresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## text summarisation

<a id="opIdsummarisation"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.kiri.ai/summarisation \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"text":"Some long text to summarise","model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.kiri.ai")

payload = "{\"text\":\"Some long text to summarise\",\"model\":\"english\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/summarisation", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = JSON.stringify({
  "text": "Some long text to summarise",
  "model": "english"
});

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.kiri.ai/summarisation");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /summarisation`

Performs summarisation on the provided text

> Body parameter

```json
{
  "text": "Some long text to summarise",
  "model": "english"
}
```

<h3 id="text-summarisation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[SummarisationBody](#schemasummarisationbody)|true|none|

> Example responses

> 200 Response

```json
{
  "output": "Summary of long text"
}
```

<h3 id="text-summarisation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful summarisation|[SummarisationResponse](#schemasummarisationresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## emotion detection

<a id="opIdemotion"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.kiri.ai/emotion \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"text":"I hope this works","model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.kiri.ai")

payload = "{\"text\":\"I hope this works\",\"model\":\"english\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/emotion", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = JSON.stringify({
  "text": "I hope this works",
  "model": "english"
});

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.kiri.ai/emotion");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /emotion`

Performs emotion detection on the provided text. The response is a string of comma separated emotions. The emotions are from: neutral, admiration, approval, annoyance, gratitude, disapproval, amusement, curiosity, love, optimism, disappointment, joy, realization, anger, sadness, confusion, caring, excitement, surprise, disgust, desire, fear, remorse, embarrassment, nervousness, pride, relief, grief.

> Body parameter

```json
{
  "text": "I hope this works",
  "model": "english"
}
```

<h3 id="emotion-detection-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[EmotionBody](#schemaemotionbody)|true|none|

> Example responses

> 200 Response

```json
{
  "output": "optimism"
}
```

<h3 id="emotion-detection-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful emotion detection|[EmotionResponse](#schemaemotionresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

# Schemas

<h2 id="tocS_VectorisationBody">VectorisationBody</h2>
<!-- backwards compatibility -->
<a id="schemavectorisationbody"></a>
<a id="schema_VectorisationBody"></a>
<a id="tocSvectorisationbody"></a>
<a id="tocsvectorisationbody"></a>

```json
{
  "text": "iPhone 12 128GB",
  "model": "english"
}

```

Vectorisation body

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Vectorisation body|any|false|none|Vectorisation body variants for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[VectorisationSingle](#schemavectorisationsingle)|false|none|Single item vectorisation|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[VectorisationBatch](#schemavectorisationbatch)|false|none|Batch vectorisation|

<h2 id="tocS_VectorisationSingle">VectorisationSingle</h2>
<!-- backwards compatibility -->
<a id="schemavectorisationsingle"></a>
<a id="schema_VectorisationSingle"></a>
<a id="tocSvectorisationsingle"></a>
<a id="tocsvectorisationsingle"></a>

```json
{
  "text": "iPhone 12 128GB",
  "model": "english"
}

```

Single item vectorisation

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|string|true|none|none|
|model|string|false|none|Model to use:<br>  * `english` - English optimised vectorisation<br>  * `multilingual` - Multilingual vectorisation in 50+ languages: ar, bg, ca, cs, da, de, el, es, et, fa, fi, fr, fr-ca, gl, gu, he, hi, hr, hu, hy, id, it, ja, ka, ko, ku, lt, lv, mk, mn, mr, ms, my, nb, nl, pl, pt, pt, pt-br, ro, ru, sk, sl, sq, sr, sv, th, tr, uk, ur, vi, zh-cn, zh-tw.|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|
|model|multilingual|

<h2 id="tocS_VectorisationBatch">VectorisationBatch</h2>
<!-- backwards compatibility -->
<a id="schemavectorisationbatch"></a>
<a id="schema_VectorisationBatch"></a>
<a id="tocSvectorisationbatch"></a>
<a id="tocsvectorisationbatch"></a>

```json
{
  "text": [
    "iPhone 12 128GB",
    "RTX 3090"
  ],
  "model": "english"
}

```

Batch vectorisation

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|[string]|true|none|none|
|model|string|false|none|Model to use:<br>  * `english` - English optimised vectorisation<br>  * `multilingual` - Multilingual vectorisation in 50+ languages: ar, bg, ca, cs, da, de, el, es, et, fa, fi, fr, fr-ca, gl, gu, he, hi, hr, hu, hy, id, it, ja, ka, ko, ku, lt, lv, mk, mn, mr, ms, my, nb, nl, pl, pt, pt, pt-br, ro, ru, sk, sl, sq, sr, sv, th, tr, uk, ur, vi, zh-cn, zh-tw.|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|
|model|multilingual|

<h2 id="tocS_VectorisationResponse">VectorisationResponse</h2>
<!-- backwards compatibility -->
<a id="schemavectorisationresponse"></a>
<a id="schema_VectorisationResponse"></a>
<a id="tocSvectorisationresponse"></a>
<a id="tocsvectorisationresponse"></a>

```json
{
  "vector": [
    0.92949192,
    0.2312301
  ]
}

```

Vectorisation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Vectorisation response|any|false|none|Vectorisation responses for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[VectorisationSingleResponse](#schemavectorisationsingleresponse)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[VectorisationBatchResponse](#schemavectorisationbatchresponse)|false|none|none|

<h2 id="tocS_VectorisationSingleResponse">VectorisationSingleResponse</h2>
<!-- backwards compatibility -->
<a id="schemavectorisationsingleresponse"></a>
<a id="schema_VectorisationSingleResponse"></a>
<a id="tocSvectorisationsingleresponse"></a>
<a id="tocsvectorisationsingleresponse"></a>

```json
{
  "vector": [
    0.92949192,
    0.2312301
  ]
}

```

Single item vectorisation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|vector|[number]|false|none|none|

<h2 id="tocS_VectorisationBatchResponse">VectorisationBatchResponse</h2>
<!-- backwards compatibility -->
<a id="schemavectorisationbatchresponse"></a>
<a id="schema_VectorisationBatchResponse"></a>
<a id="tocSvectorisationbatchresponse"></a>
<a id="tocsvectorisationbatchresponse"></a>

```json
{
  "vectorList": [
    [
      0.92949192,
      0.2312301
    ],
    [
      0.82939192,
      0.5312701
    ]
  ]
}

```

Batch vectorisation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|vectorList|[array]|false|none|none|

<h2 id="tocS_QABody">QABody</h2>
<!-- backwards compatibility -->
<a id="schemaqabody"></a>
<a id="schema_QABody"></a>
<a id="tocSqabody"></a>
<a id="tocsqabody"></a>

```json
{
  "question": "What is the meaning of life?",
  "context": "The meaning of life is 42.",
  "prev_q": [
    "What is not the meaning of life?"
  ],
  "prev_a": [
    "unknown"
  ],
  "model": "english"
}

```

QA body

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|QA body|any|false|none|QA body variants for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[QASingle](#schemaqasingle)|false|none|Single item QA|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[QABatch](#schemaqabatch)|false|none|Batch QA|

<h2 id="tocS_QASingle">QASingle</h2>
<!-- backwards compatibility -->
<a id="schemaqasingle"></a>
<a id="schema_QASingle"></a>
<a id="tocSqasingle"></a>
<a id="tocsqasingle"></a>

```json
{
  "question": "What is the meaning of life?",
  "context": "The meaning of life is 42.",
  "prev_q": [
    "What is not the meaning of life?"
  ],
  "prev_a": [
    "unknown"
  ],
  "model": "english"
}

```

Single item QA

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|question|string|true|none|question to answer|
|context|string|true|none|context to answer based on|
|prev_q|[string]|false|none|none|
|prev_a|[string]|false|none|none|
|model|string|false|none|Model to use:<br>  * `english` - English only QA|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|

<h2 id="tocS_QABatch">QABatch</h2>
<!-- backwards compatibility -->
<a id="schemaqabatch"></a>
<a id="schema_QABatch"></a>
<a id="tocSqabatch"></a>
<a id="tocsqabatch"></a>

```json
{
  "question": [
    "What is the meaning of life?",
    "Where does Sally live?"
  ],
  "context": [
    "The meaning of life is 42.",
    "Sally lives in London"
  ],
  "prev_q": [
    [
      "What is not the meaning of life?"
    ],
    [
      "Where did Sally go to school?"
    ]
  ],
  "prev_a": [
    [
      "unknown"
    ],
    [
      "unknown"
    ]
  ],
  "model": "english"
}

```

Batch QA

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|question|[string]|true|none|list of questions to answer|
|context|[string]|true|none|context to answer based on|
|prev_q|[array]|false|none|none|
|prev_a|[array]|false|none|none|
|model|string|false|none|Model to use:<br>  * `english` - English only QA|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|

<h2 id="tocS_QAResponse">QAResponse</h2>
<!-- backwards compatibility -->
<a id="schemaqaresponse"></a>
<a id="schema_QAResponse"></a>
<a id="tocSqaresponse"></a>
<a id="tocsqaresponse"></a>

```json
{
  "answer": "42"
}

```

QA response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|QA response|any|false|none|QA responses for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[QASingleResponse](#schemaqasingleresponse)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[QABatchResponse](#schemaqabatchresponse)|false|none|none|

<h2 id="tocS_QASingleResponse">QASingleResponse</h2>
<!-- backwards compatibility -->
<a id="schemaqasingleresponse"></a>
<a id="schema_QASingleResponse"></a>
<a id="tocSqasingleresponse"></a>
<a id="tocsqasingleresponse"></a>

```json
{
  "answer": "42"
}

```

Single item QA response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|answer|string|false|none|none|

<h2 id="tocS_QABatchResponse">QABatchResponse</h2>
<!-- backwards compatibility -->
<a id="schemaqabatchresponse"></a>
<a id="schema_QABatchResponse"></a>
<a id="tocSqabatchresponse"></a>
<a id="tocsqabatchresponse"></a>

```json
{
  "answer": [
    "42",
    "London"
  ]
}

```

Batch QA response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|answer|[string]|false|none|none|

<h2 id="tocS_ClassificationBody">ClassificationBody</h2>
<!-- backwards compatibility -->
<a id="schemaclassificationbody"></a>
<a id="schema_ClassificationBody"></a>
<a id="tocSclassificationbody"></a>
<a id="tocsclassificationbody"></a>

```json
{
  "text": "I am really mad because my product broke.",
  "labels": [
    "product issue",
    "furniture",
    "space"
  ],
  "model": "english"
}

```

Classification body

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Classification body|any|false|none|Classification body variants for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ClassificationSingle](#schemaclassificationsingle)|false|none|Single item Classification|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ClassificationBatch](#schemaclassificationbatch)|false|none|Batch Classification|

<h2 id="tocS_ClassificationSingle">ClassificationSingle</h2>
<!-- backwards compatibility -->
<a id="schemaclassificationsingle"></a>
<a id="schema_ClassificationSingle"></a>
<a id="tocSclassificationsingle"></a>
<a id="tocsclassificationsingle"></a>

```json
{
  "text": "I am really mad because my product broke.",
  "labels": [
    "product issue",
    "furniture",
    "space"
  ],
  "model": "english"
}

```

Single item Classification

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|string|true|none|text to classify|
|labels|[string]|true|none|labels to predict probabilities for|
|model|string|false|none|Model to use:<br>  * `english` - English only classification<br>  * `multilingual` - Multilingual classification in 100+ languages: Afrikaans, Albanian, Amharic, Arabic, Armenian, Assamese, Azerbaijani, Basque, Belarusian, Bengali, Bengali Romanized, Bosnian, Breton, Bulgarian, Burmese, Burmese, Catalan, Chinese (Simplified), Chinese (Traditional), Croatian, Czech, Danish, Dutch, English, Esperanto, Estonian, Filipino, Finnish, French, Galician, Georgian, German, Greek, Gujarati, Hausa, Hebrew, Hindi, Hindi Romanized, Hungarian, Icelandic, Indonesian, Irish, Italian, Japanese, Javanese, Kannada, Kazakh, Khmer, Korean, Kurdish (Kurmanji), Kyrgyz, Lao, Latin, Latvian, Lithuanian, Macedonian, Malagasy, Malay, Malayalam, Marathi, Mongolian, Nepali, Norwegian, Oriya, Oromo, Pashto, Persian, Polish, Portuguese, Punjabi, Romanian, Russian, Sanskri, Scottish, Gaelic, Serbian, Sindhi, Sinhala, Slovak, Slovenian, Somali, Spanish, Sundanese, Swahili, Swedish, Tamil, Tamil Romanized, Telugu, Telugu Romanized, Thai, Turkish, Ukrainian, Urdu, Urdu Romanized, Uyghur, Uzbek, Vietnamese, Welsh, Western, Frisian, Xhosa, Yiddish.|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|
|model|multilingual|

<h2 id="tocS_ClassificationBatch">ClassificationBatch</h2>
<!-- backwards compatibility -->
<a id="schemaclassificationbatch"></a>
<a id="schema_ClassificationBatch"></a>
<a id="tocSclassificationbatch"></a>
<a id="tocsclassificationbatch"></a>

```json
{
  "text": [
    "I am really mad because my product broke.",
    "I would like to collaborate with you on social media"
  ],
  "labels": [
    [
      "product issue",
      "furniture",
      "space"
    ],
    [
      "product issue",
      "furniture",
      "sales"
    ]
  ],
  "model": "english"
}

```

Batch Classification

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|[string]|true|none|list text to classify|
|labels|[array]|true|none|list of list of labels to predict probabilities for|
|model|string|false|none|Model to use:<br>  * `english` - English only classification<br>  * `multilingual` - Multilingual classification in 100+ languages: Afrikaans, Albanian, Amharic, Arabic, Armenian, Assamese, Azerbaijani, Basque, Belarusian, Bengali, Bengali Romanized, Bosnian, Breton, Bulgarian, Burmese, Burmese, Catalan, Chinese (Simplified), Chinese (Traditional), Croatian, Czech, Danish, Dutch, English, Esperanto, Estonian, Filipino, Finnish, French, Galician, Georgian, German, Greek, Gujarati, Hausa, Hebrew, Hindi, Hindi Romanized, Hungarian, Icelandic, Indonesian, Irish, Italian, Japanese, Javanese, Kannada, Kazakh, Khmer, Korean, Kurdish (Kurmanji), Kyrgyz, Lao, Latin, Latvian, Lithuanian, Macedonian, Malagasy, Malay, Malayalam, Marathi, Mongolian, Nepali, Norwegian, Oriya, Oromo, Pashto, Persian, Polish, Portuguese, Punjabi, Romanian, Russian, Sanskri, Scottish, Gaelic, Serbian, Sindhi, Sinhala, Slovak, Slovenian, Somali, Spanish, Sundanese, Swahili, Swedish, Tamil, Tamil Romanized, Telugu, Telugu Romanized, Thai, Turkish, Ukrainian, Urdu, Urdu Romanized, Uyghur, Uzbek, Vietnamese, Welsh, Western, Frisian, Xhosa, Yiddish.|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|
|model|multilingual|

<h2 id="tocS_ClassificationResponse">ClassificationResponse</h2>
<!-- backwards compatibility -->
<a id="schemaclassificationresponse"></a>
<a id="schema_ClassificationResponse"></a>
<a id="tocSclassificationresponse"></a>
<a id="tocsclassificationresponse"></a>

```json
{
  "probabilities": {
    "product issue": 0.98,
    "furniture": 0.1,
    "space": 0.05
  }
}

```

Classification response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Classification response|any|false|none|Classification responses for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ClassificationSingleResponse](#schemaclassificationsingleresponse)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ClassificationBatchResponse](#schemaclassificationbatchresponse)|false|none|none|

<h2 id="tocS_ClassificationSingleResponse">ClassificationSingleResponse</h2>
<!-- backwards compatibility -->
<a id="schemaclassificationsingleresponse"></a>
<a id="schema_ClassificationSingleResponse"></a>
<a id="tocSclassificationsingleresponse"></a>
<a id="tocsclassificationsingleresponse"></a>

```json
{
  "probabilities": {
    "product issue": 0.98,
    "furniture": 0.1,
    "space": 0.05
  }
}

```

Single item classification response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|probabilities|object|false|none|dictionary where the keys are your labels and values are probabilities|

<h2 id="tocS_ClassificationBatchResponse">ClassificationBatchResponse</h2>
<!-- backwards compatibility -->
<a id="schemaclassificationbatchresponse"></a>
<a id="schema_ClassificationBatchResponse"></a>
<a id="tocSclassificationbatchresponse"></a>
<a id="tocsclassificationbatchresponse"></a>

```json
{
  "probabilities": [
    {
      "product issue": 0.98,
      "furniture": 0.1,
      "space": 0.05
    },
    {
      "product issue": 0.2,
      "furniture": 0.03,
      "sales": 0.87
    }
  ]
}

```

Batch classification response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|probabilities|[object]|false|none|list of dictionaries where the keys are your labels and values are probabilities|

<h2 id="tocS_ImageClassificationBody">ImageClassificationBody</h2>
<!-- backwards compatibility -->
<a id="schemaimageclassificationbody"></a>
<a id="schema_ImageClassificationBody"></a>
<a id="tocSimageclassificationbody"></a>
<a id="tocsimageclassificationbody"></a>

```json
{
  "image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABpUAAATOCAYAAAA",
  "labels": [
    "healthy brain",
    "brain with tumor"
  ],
  "model": "english"
}

```

Image classification body

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Image classification body|[ImageClassificationSingle](#schemaimageclassificationsingle)|false|none|Image classification body|

<h2 id="tocS_ImageClassificationSingle">ImageClassificationSingle</h2>
<!-- backwards compatibility -->
<a id="schemaimageclassificationsingle"></a>
<a id="schema_ImageClassificationSingle"></a>
<a id="tocSimageclassificationsingle"></a>
<a id="tocsimageclassificationsingle"></a>

```json
{
  "image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABpUAAATOCAYAAAA",
  "labels": [
    "healthy brain",
    "brain with tumor"
  ],
  "model": "english"
}

```

Single item image classification

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image|string|true|none|base64 encoded image|
|labels|[string]|true|none|labels to predict probabilities for|
|model|string|false|none|Model to use:<br>  * `english` - Classification with English labels|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|

<h2 id="tocS_ImageClassificationResponse">ImageClassificationResponse</h2>
<!-- backwards compatibility -->
<a id="schemaimageclassificationresponse"></a>
<a id="schema_ImageClassificationResponse"></a>
<a id="tocSimageclassificationresponse"></a>
<a id="tocsimageclassificationresponse"></a>

```json
{
  "probabilities": {
    "brain with tumor": 0.98,
    "healthy brain": 0.02
  }
}

```

Image classification response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Image classification response|[ImageClassificationSingleResponse](#schemaimageclassificationsingleresponse)|false|none|Image classification response|

<h2 id="tocS_ImageClassificationSingleResponse">ImageClassificationSingleResponse</h2>
<!-- backwards compatibility -->
<a id="schemaimageclassificationsingleresponse"></a>
<a id="schema_ImageClassificationSingleResponse"></a>
<a id="tocSimageclassificationsingleresponse"></a>
<a id="tocsimageclassificationsingleresponse"></a>

```json
{
  "probabilities": {
    "brain with tumor": 0.98,
    "healthy brain": 0.02
  }
}

```

Single item image classification response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|probabilities|object|false|none|dictionary where the keys are your labels and values are probabilities. Probabilities always sum to 100%.|

<h2 id="tocS_GenerationBody">GenerationBody</h2>
<!-- backwards compatibility -->
<a id="schemagenerationbody"></a>
<a id="schema_GenerationBody"></a>
<a id="tocSgenerationbody"></a>
<a id="tocsgenerationbody"></a>

```json
{
  "text": "Geralt knew the signs, the monster was a",
  "min_length": 10,
  "max_length": 20,
  "temperature": 1,
  "top_k": 0,
  "top_p": 1,
  "repetition_penalty": 1,
  "length_penalty": 1,
  "num_beams": 1,
  "num_generations": 1,
  "model": "gpt2-large"
}

```

Generation body

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Generation body|any|false|none|Generation body variants for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[GenerationSingle](#schemagenerationsingle)|false|none|Single item generation|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[GenerationBatch](#schemagenerationbatch)|false|none|Batch generation|

<h2 id="tocS_GenerationSingle">GenerationSingle</h2>
<!-- backwards compatibility -->
<a id="schemagenerationsingle"></a>
<a id="schema_GenerationSingle"></a>
<a id="tocSgenerationsingle"></a>
<a id="tocsgenerationsingle"></a>

```json
{
  "text": "Geralt knew the signs, the monster was a",
  "min_length": 10,
  "max_length": 20,
  "temperature": 1,
  "top_k": 0,
  "top_p": 1,
  "repetition_penalty": 1,
  "length_penalty": 1,
  "num_beams": 1,
  "num_generations": 1,
  "model": "gpt2-large"
}

```

Single item generation

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|string|true|none|text to generate from|
|min_length|integer|false|none|minimum number of tokens to generate|
|max_length|integer|false|none|maximum number of tokens to generate|
|temperature|number|false|none|value that alters softmax probabilities. 0.0 is deterministic. As the temperature gets higher, the generated tokens get more random.|
|top_k|integer|false|none|sampling strategy in which probabilities are redistributed among top k most-likely tokens. 0 is a special value where all tokens are considered.|
|top_p|number|false|none|Sampling strategy in which probabilities are distributed among set of words with combined probability greater than p.|
|repetition_penalty|number|false|none|Penalty to be applied to tokens present in the text and tokens already generated in the sequence. Values higher than 1.0 penalise repetition, while lower than 1.0 encourage it.|
|length_penalty|number|false|none|Penalty applied to overall sequence length. Set to greater than 1.0 for longer sequences or smaller than 1.0 for shorter ones.|
|num_beams|integer|false|none|Number of beams to be used in beam search. (1 is no beam search)|
|num_generations|integer|false|none|Number of times to do generation for input.|
|model|string|false|none|Model to use:<br>  * `gpt2-large` - An optimised large version of gpt2.<br>  * `t5-base-qa-summary-emotion` - The T5 base model trained for question answering, summarisation and emotion detection.|

#### Enumerated Values

|Property|Value|
|---|---|
|model|gpt2-large|
|model|t5-base-qa-summary-emotion|

<h2 id="tocS_GenerationBatch">GenerationBatch</h2>
<!-- backwards compatibility -->
<a id="schemagenerationbatch"></a>
<a id="schema_GenerationBatch"></a>
<a id="tocSgenerationbatch"></a>
<a id="tocsgenerationbatch"></a>

```json
{
  "text": [
    "Geralt knew the signs, the monster was a",
    "c: Elon Musk is an entrepreneur born in 1971. q: Who is Elon Musk? a: an entrepreneur q: When was he born? a: "
  ],
  "min_length": 10,
  "max_length": 20,
  "temperature": 1,
  "top_k": 0,
  "top_p": 1,
  "repetition_penalty": 1,
  "length_penalty": 1,
  "num_beams": 1,
  "num_generations": 1,
  "model": "gpt2-large"
}

```

Batch generation

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|[string]|true|none|text to generate from|
|min_length|integer|false|none|minimum number of tokens to generate|
|max_length|integer|false|none|maximum number of tokens to generate|
|temperature|number|false|none|value that alters softmax probabilities. 0.0 is deterministic. As the temperature gets higher, the generated tokens get more random.|
|top_k|integer|false|none|sampling strategy in which probabilities are redistributed among top k most-likely tokens. 0 is a special value where all tokens are considered.|
|top_p|number|false|none|Sampling strategy in which probabilities are distributed among set of words with combined probability greater than p.|
|repetition_penalty|number|false|none|Penalty to be applied to tokens present in the text and tokens already generated in the sequence. Values higher than 1.0 penalise repetition, while lower than 1.0 encourage it.|
|length_penalty|number|false|none|Penalty applied to overall sequence length. Set to greater than 1.0 for longer sequences or smaller than 1.0 for shorter ones.|
|num_beams|integer|false|none|Number of beams to be used in beam search. (1 is no beam search)|
|num_generations|integer|false|none|Number of times to do generation for input.|
|model|string|false|none|Model to use:<br>  * `gpt2-large` - An optimised large version of gpt2.<br>  * `t5-base-qa-summary-emotion` - The T5 base model trained for question answering, summarisation and emotion detection.|

#### Enumerated Values

|Property|Value|
|---|---|
|model|gpt2-large|
|model|t5-base-qa-summary-emotion|

<h2 id="tocS_GenerationResponse">GenerationResponse</h2>
<!-- backwards compatibility -->
<a id="schemagenerationresponse"></a>
<a id="schema_GenerationResponse"></a>
<a id="tocSgenerationresponse"></a>
<a id="tocsgenerationresponse"></a>

```json
{
  "output": "Geralt knew the signs, the monster was a vampire that day; after the siege her companions"
}

```

Generation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Generation response|any|false|none|Generation responses for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[GenerationSingleResponse](#schemagenerationsingleresponse)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[GenerationBatchResponse](#schemagenerationbatchresponse)|false|none|none|

<h2 id="tocS_GenerationSingleResponse">GenerationSingleResponse</h2>
<!-- backwards compatibility -->
<a id="schemagenerationsingleresponse"></a>
<a id="schema_GenerationSingleResponse"></a>
<a id="tocSgenerationsingleresponse"></a>
<a id="tocsgenerationsingleresponse"></a>

```json
{
  "output": "Geralt knew the signs, the monster was a vampire that day; after the siege her companions"
}

```

Single item generation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|output|string|false|none|none|

<h2 id="tocS_GenerationBatchResponse">GenerationBatchResponse</h2>
<!-- backwards compatibility -->
<a id="schemagenerationbatchresponse"></a>
<a id="schema_GenerationBatchResponse"></a>
<a id="tocSgenerationbatchresponse"></a>
<a id="tocsgenerationbatchresponse"></a>

```json
{
  "output": [
    "Geralt knew the signs, the monster was a vampire that day; after the siege her companions",
    "1971"
  ]
}

```

Batch generation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|output|[string]|false|none|none|

<h2 id="tocS_SummarisationBody">SummarisationBody</h2>
<!-- backwards compatibility -->
<a id="schemasummarisationbody"></a>
<a id="schema_SummarisationBody"></a>
<a id="tocSsummarisationbody"></a>
<a id="tocssummarisationbody"></a>

```json
{
  "text": "Some long text to summarise",
  "model": "english"
}

```

Summarisation body

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Summarisation body|any|false|none|Summarisation body variants for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[SummarisationSingle](#schemasummarisationsingle)|false|none|Single item summarisation|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[SummarisationBatch](#schemasummarisationbatch)|false|none|Batch summarisation|

<h2 id="tocS_SummarisationSingle">SummarisationSingle</h2>
<!-- backwards compatibility -->
<a id="schemasummarisationsingle"></a>
<a id="schema_SummarisationSingle"></a>
<a id="tocSsummarisationsingle"></a>
<a id="tocssummarisationsingle"></a>

```json
{
  "text": "Some long text to summarise",
  "model": "english"
}

```

Single item summarisation

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|string|true|none|none|
|model|string|false|none|Model to use:<br>  * `english` - English text summarisation|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|

<h2 id="tocS_SummarisationBatch">SummarisationBatch</h2>
<!-- backwards compatibility -->
<a id="schemasummarisationbatch"></a>
<a id="schema_SummarisationBatch"></a>
<a id="tocSsummarisationbatch"></a>
<a id="tocssummarisationbatch"></a>

```json
{
  "text": [
    "Some long text to summarise",
    "Some more long text that needs summarising"
  ],
  "model": "english"
}

```

Batch summarisation

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|[string]|true|none|none|
|model|string|false|none|Model to use:<br>  * `english` - English text summarisation|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|

<h2 id="tocS_SummarisationResponse">SummarisationResponse</h2>
<!-- backwards compatibility -->
<a id="schemasummarisationresponse"></a>
<a id="schema_SummarisationResponse"></a>
<a id="tocSsummarisationresponse"></a>
<a id="tocssummarisationresponse"></a>

```json
{
  "output": "Summary of long text"
}

```

Summarisation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Summarisation response|any|false|none|Summarisation responses for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[SummarisationSingleResponse](#schemasummarisationsingleresponse)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[SummarisationBatchResponse](#schemasummarisationbatchresponse)|false|none|none|

<h2 id="tocS_SummarisationSingleResponse">SummarisationSingleResponse</h2>
<!-- backwards compatibility -->
<a id="schemasummarisationsingleresponse"></a>
<a id="schema_SummarisationSingleResponse"></a>
<a id="tocSsummarisationsingleresponse"></a>
<a id="tocssummarisationsingleresponse"></a>

```json
{
  "output": "Summary of long text"
}

```

Single item summarisation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|output|string|false|none|none|

<h2 id="tocS_SummarisationBatchResponse">SummarisationBatchResponse</h2>
<!-- backwards compatibility -->
<a id="schemasummarisationbatchresponse"></a>
<a id="schema_SummarisationBatchResponse"></a>
<a id="tocSsummarisationbatchresponse"></a>
<a id="tocssummarisationbatchresponse"></a>

```json
{
  "output": [
    "Summary of long text",
    "Summary of some more long text"
  ]
}

```

Batch summarisation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|output|[string]|false|none|none|

<h2 id="tocS_EmotionBody">EmotionBody</h2>
<!-- backwards compatibility -->
<a id="schemaemotionbody"></a>
<a id="schema_EmotionBody"></a>
<a id="tocSemotionbody"></a>
<a id="tocsemotionbody"></a>

```json
{
  "text": "I hope this works",
  "model": "english"
}

```

Emotion body

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Emotion body|any|false|none|Emotion body variants for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[EmotionSingle](#schemaemotionsingle)|false|none|Single item emotion detection|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[EmotionBatch](#schemaemotionbatch)|false|none|Batch emotion detection|

<h2 id="tocS_EmotionSingle">EmotionSingle</h2>
<!-- backwards compatibility -->
<a id="schemaemotionsingle"></a>
<a id="schema_EmotionSingle"></a>
<a id="tocSemotionsingle"></a>
<a id="tocsemotionsingle"></a>

```json
{
  "text": "I hope this works",
  "model": "english"
}

```

Single item emotion detection

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|string|true|none|none|
|model|string|false|none|Model to use:<br>  * `english` - English text emotion detection|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|

<h2 id="tocS_EmotionBatch">EmotionBatch</h2>
<!-- backwards compatibility -->
<a id="schemaemotionbatch"></a>
<a id="schema_EmotionBatch"></a>
<a id="tocSemotionbatch"></a>
<a id="tocsemotionbatch"></a>

```json
{
  "text": [
    "I hope this works",
    "I'll be most upset if things go wrong"
  ],
  "model": "english"
}

```

Batch emotion detection

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|[string]|true|none|none|
|model|string|false|none|Model to use:<br>  * `english` - English text emotion detection|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|

<h2 id="tocS_EmotionResponse">EmotionResponse</h2>
<!-- backwards compatibility -->
<a id="schemaemotionresponse"></a>
<a id="schema_EmotionResponse"></a>
<a id="tocSemotionresponse"></a>
<a id="tocsemotionresponse"></a>

```json
{
  "output": "optimism"
}

```

Emotion detection response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Emotion detection response|any|false|none|Emotion detection responses for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[EmotionSingleResponse](#schemaemotionsingleresponse)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[EmotionBatchResponse](#schemaemotionbatchresponse)|false|none|none|

<h2 id="tocS_EmotionSingleResponse">EmotionSingleResponse</h2>
<!-- backwards compatibility -->
<a id="schemaemotionsingleresponse"></a>
<a id="schema_EmotionSingleResponse"></a>
<a id="tocSemotionsingleresponse"></a>
<a id="tocsemotionsingleresponse"></a>

```json
{
  "output": "optimism"
}

```

Single item emotion detection response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|output|string|false|none|none|

<h2 id="tocS_EmotionBatchResponse">EmotionBatchResponse</h2>
<!-- backwards compatibility -->
<a id="schemaemotionbatchresponse"></a>
<a id="schema_EmotionBatchResponse"></a>
<a id="tocSemotionbatchresponse"></a>
<a id="tocsemotionbatchresponse"></a>

```json
{
  "output": [
    "optimism",
    "disappointment, sadness"
  ]
}

```

Batch emotion detection response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|output|[string]|false|none|none|

