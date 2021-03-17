---
title: Backprop API v1.0.0
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

<h1 id="backprop-api">Backprop API v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

Welcome to our API documentation! Things to note:

  - Most task endpoints can take both single and batched requests. This is so you can save time on round trip times speed up your inference when working with more data. The different `body` and `response` variants are shown in the respective `single` and `batch` schemas.
  
  - All endpoints require authentication with your API key in the `x-api-key` header.
  
  - Some task endpoints may have multiple `model` options. This is useful to know if your task is in a language other than English.
  
  - Every account gets `1000` seconds of free inference every month. Seconds are calculated only for compute time when using the endpoints.
  
If anything is unclear or you find that something is not working as intended, please get in touch!

Base URLs:

* <a href="https://api.backprop.co">https://api.backprop.co</a>

Email: <a href="mailto:hello@backprop.co">Support</a> 
License: <a href="http://www.apache.org/licenses/LICENSE-2.0.html">Apache 2.0</a>

# Authentication

* API Key (ApiKeyAuth)
    - Parameter Name: **x-api-key**, in: header. 

<h1 id="backprop-api-tasks">Tasks</h1>

Endpoints to call tasks that implement various models for your use cases.

## text vectorisation

<a id="opIdtext-vectorisation"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.backprop.co/text-vectorisation \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"text":"iPhone 12 128GB","model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

payload = "{\"text\":\"iPhone 12 128GB\",\"model\":\"english\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/text-vectorisation", payload, headers)

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

xhr.open("POST", "https://api.backprop.co/text-vectorisation");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /text-vectorisation`

vectorises string or list of strings

> Body parameter

```json
{
  "text": "iPhone 12 128GB",
  "model": "english"
}
```

<h3 id="text-vectorisation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[TextVectorisationBody](#schematextvectorisationbody)|true|text or list of text to vectorise|

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

<h3 id="text-vectorisation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successfully vectorised|[TextVectorisationResponse](#schematextvectorisationresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## question answering

<a id="opIdqa"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.backprop.co/qa \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"question":"What is the meaning of life?","context":"The meaning of life is 42.","prev_q":["What is not the meaning of life?"],"prev_a":["unknown"],"model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

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

xhr.open("POST", "https://api.backprop.co/qa");
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

## text classification

<a id="opIdtext-classification"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.backprop.co/text-classification \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"text":"I am really mad because my product broke.","labels":["product issue","furniture","space"],"model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

payload = "{\"text\":\"I am really mad because my product broke.\",\"labels\":[\"product issue\",\"furniture\",\"space\"],\"model\":\"english\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/text-classification", payload, headers)

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

xhr.open("POST", "https://api.backprop.co/text-classification");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /text-classification`

Performs classification on provided text and labels.

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

<h3 id="text-classification-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[TextClassificationBody](#schematextclassificationbody)|true|none|

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

<h3 id="text-classification-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful classification|[TextClassificationResponse](#schematextclassificationresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## zero shot image classification

<a id="opIdimage-classification"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.backprop.co/image-classification \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"image":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABpUAAATOCAYAAAA","labels":["healthy brain","brain with tumor"],"model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

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

xhr.open("POST", "https://api.backprop.co/image-classification");
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

<a id="opIdtext-generation"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.backprop.co/text-generation \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"text":"Geralt knew the signs, the monster was a","min_length":10,"max_length":20,"temperature":1,"top_k":0,"top_p":1,"repetition_penalty":1,"length_penalty":1,"num_beams":1,"num_generations":1,"model":"gpt2-large"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

payload = "{\"text\":\"Geralt knew the signs, the monster was a\",\"min_length\":10,\"max_length\":20,\"temperature\":1,\"top_k\":0,\"top_p\":1,\"repetition_penalty\":1,\"length_penalty\":1,\"num_beams\":1,\"num_generations\":1,\"model\":\"gpt2-large\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/text-generation", payload, headers)

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

xhr.open("POST", "https://api.backprop.co/text-generation");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /text-generation`

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
|body|body|[TextGenerationBody](#schematextgenerationbody)|true|none|

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
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful generation|[TextGenerationResponse](#schematextgenerationresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## text summarisation

<a id="opIdsummarisation"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.backprop.co/summarisation \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"text":"Some long text to summarise","model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

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

xhr.open("POST", "https://api.backprop.co/summarisation");
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
  --url https://api.backprop.co/emotion \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"text":"I hope this works","model":"english"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

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

xhr.open("POST", "https://api.backprop.co/emotion");
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

<h1 id="backprop-api-models">Models</h1>

Endpoints to view, upload and delete models

## get models

<a id="opIdget-models"></a>

> Code samples

```shell
curl --request GET \
  --url https://api.backprop.co/models \
  --header 'Accept: application/json' \
  --header 'x-api-key: API_KEY'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

headers = {
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("GET", "/models", headers=headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = null;

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("GET", "https://api.backprop.co/models");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`GET /models`

Gets a list of global and user models. Some info about global models is hidden.

<h3 id="get-models-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|include_global|query|boolean|false|Whether to include global models in the list|

> Example responses

> 200 Response

```json
[
  {
    "id": "model_model-name",
    "name": "model-name",
    "description": "Some description about model-name",
    "tasks": [
      "text-generation",
      "qa"
    ],
    "build_status": "building",
    "last_deployment": "2021-03-05T10:31:16Z"
  }
]
```

<h3 id="get-models-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of models|[ModelsResponse](#schemamodelsresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## get model

<a id="opIdget-model"></a>

> Code samples

```shell
curl --request GET \
  --url https://api.backprop.co/models/string \
  --header 'Accept: application/json' \
  --header 'x-api-key: API_KEY'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

headers = {
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("GET", "/models/string", headers=headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = null;

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("GET", "https://api.backprop.co/models/string");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`GET /models/{model}`

Gets detailed information about a model. Cannot query global models.

<h3 id="get-model-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|model|path|string|true|Name of the model|

> Example responses

> 200 Response

```json
{
  "id": "model_model-name",
  "name": "model-name",
  "description": "Some description about model-name",
  "tasks": [
    "text-generation",
    "qa"
  ],
  "build_status": "building",
  "build_message": "some build related message",
  "last_deployment": "2021-03-05T10:31:16Z",
  "model_url": "https://kiri-user-models.s3.eu-central-1.amazonaws.com/acc_id/some-model/model.bin",
  "config_url": "https://kiri-user-models.s3.eu-central-1.amazonaws.com/acc_id/some-model/config.json",
  "requirements_url": "https://kiri-user-models.s3.eu-central-1.amazonaws.com/acc_id/some-model/requirements.txt"
}
```

<h3 id="get-model-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|detailed information about a model|[ModelResponse](#schemamodelresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|model not found|[ModelResponse404](#schemamodelresponse404)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## delete model

<a id="opIddelete-model"></a>

> Code samples

```shell
curl --request DELETE \
  --url https://api.backprop.co/models/string \
  --header 'Accept: application/json' \
  --header 'x-api-key: API_KEY'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

headers = {
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("DELETE", "/models/string", headers=headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = null;

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("DELETE", "https://api.backprop.co/models/string");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`DELETE /models/{model}`

deletes a model

<h3 id="delete-model-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|model|path|string|true|Name of the model|

> Example responses

> 200 Response

```json
null
```

<h3 id="delete-model-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|model deleted|[DeleteModelResponse](#schemadeletemodelresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|model not found|[ModelResponse404](#schemamodelresponse404)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## get upload url for model

<a id="opIdupload-url"></a>

> Code samples

```shell
curl --request POST \
  --url https://api.backprop.co/upload-url \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: API_KEY' \
  --data '{"model_name":"some-model"}'
```

```python
import http.client

conn = http.client.HTTPSConnection("api.backprop.co")

payload = "{\"model_name\":\"some-model\"}"

headers = {
    'Content-Type': "application/json",
    'Accept': "application/json",
    'x-api-key': "API_KEY"
    }

conn.request("POST", "/upload-url", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```javascript
const data = JSON.stringify({
  "model_name": "some-model"
});

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.backprop.co/upload-url");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
xhr.setRequestHeader("x-api-key", "API_KEY");

xhr.send(data);
```

`POST /upload-url`

(BETA) Gets an upload url for a model. The upload url is valid for an hour and takes a PUT request with a .zip file.
  The zip file must contain exactly three files (no folders) with the specified names:
  
  * model.bin (an initiated model on CPU pickled with dill)
  * config.json (with description (value is string) and task (value is list of strings) keys)
  * requirements.txt (a python requirements file with any runtime dependencies)
  
  The maximum supported size of the zip file is 5GB.
  
It is the simplest to use our [python library](https://github.com/backprop-ai/backprop) for this functionality.

> Body parameter

```json
{
  "model_name": "some-model"
}
```

<h3 id="get-upload-url-for-model-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[UploadUrlBody](#schemauploadurlbody)|true|none|

> Example responses

> 200 Response

```json
"https://kiri-user-uploads.s3.eu-central-1.amazonaws.com/acc_id/some-model.zip"
```

<h3 id="get-upload-url-for-model-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|link for PUT request with the zip file|[UploadUrlResponse](#schemauploadurlresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

# Schemas

<h2 id="tocS_TextVectorisationBody">TextVectorisationBody</h2>
<!-- backwards compatibility -->
<a id="schematextvectorisationbody"></a>
<a id="schema_TextVectorisationBody"></a>
<a id="tocStextvectorisationbody"></a>
<a id="tocstextvectorisationbody"></a>

```json
{
  "text": "iPhone 12 128GB",
  "model": "english"
}

```

Text vectorisation body

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Text vectorisation body|any|false|none|Text vectorisation body variants for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextVectorisationSingle](#schematextvectorisationsingle)|false|none|Single item vectorisation|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextVectorisationBatch](#schematextvectorisationbatch)|false|none|Batch text vectorisation|

<h2 id="tocS_TextVectorisationSingle">TextVectorisationSingle</h2>
<!-- backwards compatibility -->
<a id="schematextvectorisationsingle"></a>
<a id="schema_TextVectorisationSingle"></a>
<a id="tocStextvectorisationsingle"></a>
<a id="tocstextvectorisationsingle"></a>

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
|model|string|false|none|Model to use:<br>  * `english` - English optimised vectorisation<br>  * `multilingual` - Multilingual vectorisation in 50+ languages: ar, bg, ca, cs, da, de, el, es, et, fa, fi, fr, fr-ca, gl, gu, he, hi, hr, hu, hy, id, it, ja, ka, ko, ku, lt, lv, mk, mn, mr, ms, my, nb, nl, pl, pt, pt, pt-br, ro, ru, sk, sl, sq, sr, sv, th, tr, uk, ur, vi, zh-cn, zh-tw.<br>  * Name of your own uploaded model|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|
|model|multilingual|

<h2 id="tocS_TextVectorisationBatch">TextVectorisationBatch</h2>
<!-- backwards compatibility -->
<a id="schematextvectorisationbatch"></a>
<a id="schema_TextVectorisationBatch"></a>
<a id="tocStextvectorisationbatch"></a>
<a id="tocstextvectorisationbatch"></a>

```json
{
  "text": [
    "iPhone 12 128GB",
    "RTX 3090"
  ],
  "model": "english"
}

```

Batch text vectorisation

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|[string]|true|none|none|
|model|string|false|none|Model to use:<br>  * `english` - English optimised vectorisation<br>  * `multilingual` - Multilingual vectorisation in 50+ languages: ar, bg, ca, cs, da, de, el, es, et, fa, fi, fr, fr-ca, gl, gu, he, hi, hr, hu, hy, id, it, ja, ka, ko, ku, lt, lv, mk, mn, mr, ms, my, nb, nl, pl, pt, pt, pt-br, ro, ru, sk, sl, sq, sr, sv, th, tr, uk, ur, vi, zh-cn, zh-tw.<br>  * Name of your own uploaded model|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|
|model|multilingual|

<h2 id="tocS_TextVectorisationResponse">TextVectorisationResponse</h2>
<!-- backwards compatibility -->
<a id="schematextvectorisationresponse"></a>
<a id="schema_TextVectorisationResponse"></a>
<a id="tocStextvectorisationresponse"></a>
<a id="tocstextvectorisationresponse"></a>

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
|*anonymous*|[TextVectorisationSingleResponse](#schematextvectorisationsingleresponse)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextVectorisationBatchResponse](#schematextvectorisationbatchresponse)|false|none|none|

<h2 id="tocS_TextVectorisationSingleResponse">TextVectorisationSingleResponse</h2>
<!-- backwards compatibility -->
<a id="schematextvectorisationsingleresponse"></a>
<a id="schema_TextVectorisationSingleResponse"></a>
<a id="tocStextvectorisationsingleresponse"></a>
<a id="tocstextvectorisationsingleresponse"></a>

```json
{
  "vector": [
    0.92949192,
    0.2312301
  ]
}

```

Single item text vectorisation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|vector|[number]|false|none|none|

<h2 id="tocS_TextVectorisationBatchResponse">TextVectorisationBatchResponse</h2>
<!-- backwards compatibility -->
<a id="schematextvectorisationbatchresponse"></a>
<a id="schema_TextVectorisationBatchResponse"></a>
<a id="tocStextvectorisationbatchresponse"></a>
<a id="tocstextvectorisationbatchresponse"></a>

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

Batch text vectorisation response

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
|model|string|false|none|Model to use:<br>  * `english` - English only QA<br>  * Name of your own uploaded model|

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
|model|string|false|none|Model to use:<br>  * `english` - English only QA<br>  * Name of your own uploaded model|

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

<h2 id="tocS_TextClassificationBody">TextClassificationBody</h2>
<!-- backwards compatibility -->
<a id="schematextclassificationbody"></a>
<a id="schema_TextClassificationBody"></a>
<a id="tocStextclassificationbody"></a>
<a id="tocstextclassificationbody"></a>

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

Text classification body

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Text classification body|any|false|none|Text classification body variants for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextClassificationSingle](#schematextclassificationsingle)|false|none|Single item Text Classification|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextClassificationBatch](#schematextclassificationbatch)|false|none|Batch Text Classification|

<h2 id="tocS_TextClassificationSingle">TextClassificationSingle</h2>
<!-- backwards compatibility -->
<a id="schematextclassificationsingle"></a>
<a id="schema_TextClassificationSingle"></a>
<a id="tocStextclassificationsingle"></a>
<a id="tocstextclassificationsingle"></a>

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

Single item Text Classification

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|string|true|none|text to classify|
|labels|[string]|true|none|labels to predict probabilities for|
|model|string|false|none|Model to use:<br>  * `english` - English only classification<br>  * `multilingual` - Multilingual classification in 100+ languages: Afrikaans, Albanian, Amharic, Arabic, Armenian, Assamese, Azerbaijani, Basque, Belarusian, Bengali, Bengali Romanized, Bosnian, Breton, Bulgarian, Burmese, Burmese, Catalan, Chinese (Simplified), Chinese (Traditional), Croatian, Czech, Danish, Dutch, English, Esperanto, Estonian, Filipino, Finnish, French, Galician, Georgian, German, Greek, Gujarati, Hausa, Hebrew, Hindi, Hindi Romanized, Hungarian, Icelandic, Indonesian, Irish, Italian, Japanese, Javanese, Kannada, Kazakh, Khmer, Korean, Kurdish (Kurmanji), Kyrgyz, Lao, Latin, Latvian, Lithuanian, Macedonian, Malagasy, Malay, Malayalam, Marathi, Mongolian, Nepali, Norwegian, Oriya, Oromo, Pashto, Persian, Polish, Portuguese, Punjabi, Romanian, Russian, Sanskri, Scottish, Gaelic, Serbian, Sindhi, Sinhala, Slovak, Slovenian, Somali, Spanish, Sundanese, Swahili, Swedish, Tamil, Tamil Romanized, Telugu, Telugu Romanized, Thai, Turkish, Ukrainian, Urdu, Urdu Romanized, Uyghur, Uzbek, Vietnamese, Welsh, Western, Frisian, Xhosa, Yiddish.<br>  * Name of your own uploaded model|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|
|model|multilingual|

<h2 id="tocS_TextClassificationBatch">TextClassificationBatch</h2>
<!-- backwards compatibility -->
<a id="schematextclassificationbatch"></a>
<a id="schema_TextClassificationBatch"></a>
<a id="tocStextclassificationbatch"></a>
<a id="tocstextclassificationbatch"></a>

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

Batch Text Classification

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|text|[string]|true|none|list text to classify|
|labels|[array]|true|none|list of list of labels to predict probabilities for|
|model|string|false|none|Model to use:<br>  * `english` - English only classification<br>  * `multilingual` - Multilingual classification in 100+ languages: Afrikaans, Albanian, Amharic, Arabic, Armenian, Assamese, Azerbaijani, Basque, Belarusian, Bengali, Bengali Romanized, Bosnian, Breton, Bulgarian, Burmese, Burmese, Catalan, Chinese (Simplified), Chinese (Traditional), Croatian, Czech, Danish, Dutch, English, Esperanto, Estonian, Filipino, Finnish, French, Galician, Georgian, German, Greek, Gujarati, Hausa, Hebrew, Hindi, Hindi Romanized, Hungarian, Icelandic, Indonesian, Irish, Italian, Japanese, Javanese, Kannada, Kazakh, Khmer, Korean, Kurdish (Kurmanji), Kyrgyz, Lao, Latin, Latvian, Lithuanian, Macedonian, Malagasy, Malay, Malayalam, Marathi, Mongolian, Nepali, Norwegian, Oriya, Oromo, Pashto, Persian, Polish, Portuguese, Punjabi, Romanian, Russian, Sanskri, Scottish, Gaelic, Serbian, Sindhi, Sinhala, Slovak, Slovenian, Somali, Spanish, Sundanese, Swahili, Swedish, Tamil, Tamil Romanized, Telugu, Telugu Romanized, Thai, Turkish, Ukrainian, Urdu, Urdu Romanized, Uyghur, Uzbek, Vietnamese, Welsh, Western, Frisian, Xhosa, Yiddish.<br>  * Name of your own uploaded model|

#### Enumerated Values

|Property|Value|
|---|---|
|model|english|
|model|multilingual|

<h2 id="tocS_TextClassificationResponse">TextClassificationResponse</h2>
<!-- backwards compatibility -->
<a id="schematextclassificationresponse"></a>
<a id="schema_TextClassificationResponse"></a>
<a id="tocStextclassificationresponse"></a>
<a id="tocstextclassificationresponse"></a>

```json
{
  "probabilities": {
    "product issue": 0.98,
    "furniture": 0.1,
    "space": 0.05
  }
}

```

Text classification response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Text classification response|any|false|none|Text classification responses for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextClassificationSingleResponse](#schematextclassificationsingleresponse)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextClassificationBatchResponse](#schematextclassificationbatchresponse)|false|none|none|

<h2 id="tocS_TextClassificationSingleResponse">TextClassificationSingleResponse</h2>
<!-- backwards compatibility -->
<a id="schematextclassificationsingleresponse"></a>
<a id="schema_TextClassificationSingleResponse"></a>
<a id="tocStextclassificationsingleresponse"></a>
<a id="tocstextclassificationsingleresponse"></a>

```json
{
  "probabilities": {
    "product issue": 0.98,
    "furniture": 0.1,
    "space": 0.05
  }
}

```

Single item text classification response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|probabilities|object|false|none|dictionary where the keys are your labels and values are probabilities|

<h2 id="tocS_TextClassificationBatchResponse">TextClassificationBatchResponse</h2>
<!-- backwards compatibility -->
<a id="schematextclassificationbatchresponse"></a>
<a id="schema_TextClassificationBatchResponse"></a>
<a id="tocStextclassificationbatchresponse"></a>
<a id="tocstextclassificationbatchresponse"></a>

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

Batch text classification response

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
|model|string|false|none|Model to use:<br>  * `english` - Classification with English labels<br>  * Name of your own uploaded model|

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

<h2 id="tocS_TextGenerationBody">TextGenerationBody</h2>
<!-- backwards compatibility -->
<a id="schematextgenerationbody"></a>
<a id="schema_TextGenerationBody"></a>
<a id="tocStextgenerationbody"></a>
<a id="tocstextgenerationbody"></a>

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

Text generation body

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Text generation body|any|false|none|Generation body variants for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextGenerationSingle](#schematextgenerationsingle)|false|none|Single item text generation|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextGenerationBatch](#schematextgenerationbatch)|false|none|Batch text generation|

<h2 id="tocS_TextGenerationSingle">TextGenerationSingle</h2>
<!-- backwards compatibility -->
<a id="schematextgenerationsingle"></a>
<a id="schema_TextGenerationSingle"></a>
<a id="tocStextgenerationsingle"></a>
<a id="tocstextgenerationsingle"></a>

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

Single item text generation

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
|model|string|false|none|Model to use:<br>  * `gpt2-large` - An optimised large version of gpt2.<br>  * `t5-base-qa-summary-emotion` - The T5 base model trained for question answering, summarisation and emotion detection.<br>  * Name of your own uploaded model|

#### Enumerated Values

|Property|Value|
|---|---|
|model|gpt2-large|
|model|t5-base-qa-summary-emotion|

<h2 id="tocS_TextGenerationBatch">TextGenerationBatch</h2>
<!-- backwards compatibility -->
<a id="schematextgenerationbatch"></a>
<a id="schema_TextGenerationBatch"></a>
<a id="tocStextgenerationbatch"></a>
<a id="tocstextgenerationbatch"></a>

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

Batch text generation

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
|model|string|false|none|Model to use:<br>  * `gpt2-large` - An optimised large version of gpt2.<br>  * `t5-base-qa-summary-emotion` - The T5 base model trained for question answering, summarisation and emotion detection.<br>  * Name of your own uploaded model|

#### Enumerated Values

|Property|Value|
|---|---|
|model|gpt2-large|
|model|t5-base-qa-summary-emotion|

<h2 id="tocS_TextGenerationResponse">TextGenerationResponse</h2>
<!-- backwards compatibility -->
<a id="schematextgenerationresponse"></a>
<a id="schema_TextGenerationResponse"></a>
<a id="tocStextgenerationresponse"></a>
<a id="tocstextgenerationresponse"></a>

```json
{
  "output": "Geralt knew the signs, the monster was a vampire that day; after the siege her companions"
}

```

Text generation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Text generation response|any|false|none|Text generation responses for single and batch requests|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextGenerationSingleResponse](#schematextgenerationsingleresponse)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TextGenerationBatchResponse](#schematextgenerationbatchresponse)|false|none|none|

<h2 id="tocS_TextGenerationSingleResponse">TextGenerationSingleResponse</h2>
<!-- backwards compatibility -->
<a id="schematextgenerationsingleresponse"></a>
<a id="schema_TextGenerationSingleResponse"></a>
<a id="tocStextgenerationsingleresponse"></a>
<a id="tocstextgenerationsingleresponse"></a>

```json
{
  "output": "Geralt knew the signs, the monster was a vampire that day; after the siege her companions"
}

```

Single item text generation response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|output|string|false|none|none|

<h2 id="tocS_TextGenerationBatchResponse">TextGenerationBatchResponse</h2>
<!-- backwards compatibility -->
<a id="schematextgenerationbatchresponse"></a>
<a id="schema_TextGenerationBatchResponse"></a>
<a id="tocStextgenerationbatchresponse"></a>
<a id="tocstextgenerationbatchresponse"></a>

```json
{
  "output": [
    "Geralt knew the signs, the monster was a vampire that day; after the siege her companions",
    "1971"
  ]
}

```

Batch text generation response

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

<h2 id="tocS_ModelsResponse">ModelsResponse</h2>
<!-- backwards compatibility -->
<a id="schemamodelsresponse"></a>
<a id="schema_ModelsResponse"></a>
<a id="tocSmodelsresponse"></a>
<a id="tocsmodelsresponse"></a>

```json
[
  {
    "id": "model_model-name",
    "name": "model-name",
    "description": "Some description about model-name",
    "tasks": [
      "text-generation",
      "qa"
    ],
    "build_status": "building",
    "last_deployment": "2021-03-05T10:31:16Z"
  }
]

```

Get models response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Get models response|[[ModelsResponse_inner](#schemamodelsresponse_inner)]|false|none|none|

<h2 id="tocS_ModelResponse">ModelResponse</h2>
<!-- backwards compatibility -->
<a id="schemamodelresponse"></a>
<a id="schema_ModelResponse"></a>
<a id="tocSmodelresponse"></a>
<a id="tocsmodelresponse"></a>

```json
{
  "id": "model_model-name",
  "name": "model-name",
  "description": "Some description about model-name",
  "tasks": [
    "text-generation",
    "qa"
  ],
  "build_status": "building",
  "build_message": "some build related message",
  "last_deployment": "2021-03-05T10:31:16Z",
  "model_url": "https://kiri-user-models.s3.eu-central-1.amazonaws.com/acc_id/some-model/model.bin",
  "config_url": "https://kiri-user-models.s3.eu-central-1.amazonaws.com/acc_id/some-model/config.json",
  "requirements_url": "https://kiri-user-models.s3.eu-central-1.amazonaws.com/acc_id/some-model/requirements.txt"
}

```

Get model response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|none|
|name|string|false|none|none|
|description|string|false|none|none|
|tasks|[string]|false|none|none|
|build_status|string|false|none|none|
|build_message|string|false|none|none|
|last_deployment|string|false|none|none|
|model_url|string|false|none|none|
|config_url|string|false|none|none|
|requirements_url|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|build_status|success|
|build_status|building|
|build_status|fail|

<h2 id="tocS_ModelResponse404">ModelResponse404</h2>
<!-- backwards compatibility -->
<a id="schemamodelresponse404"></a>
<a id="schema_ModelResponse404"></a>
<a id="tocSmodelresponse404"></a>
<a id="tocsmodelresponse404"></a>

```json
"model some-model not found"

```

Model 404 response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Model 404 response|string|false|none|none|

<h2 id="tocS_DeleteModelResponse">DeleteModelResponse</h2>
<!-- backwards compatibility -->
<a id="schemadeletemodelresponse"></a>
<a id="schema_DeleteModelResponse"></a>
<a id="tocSdeletemodelresponse"></a>
<a id="tocsdeletemodelresponse"></a>

```json
null

```

Delete model response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Delete model response|any|false|none|none|

<h2 id="tocS_UploadUrlBody">UploadUrlBody</h2>
<!-- backwards compatibility -->
<a id="schemauploadurlbody"></a>
<a id="schema_UploadUrlBody"></a>
<a id="tocSuploadurlbody"></a>
<a id="tocsuploadurlbody"></a>

```json
{
  "model_name": "some-model"
}

```

Upload url response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|model_name|string|true|none|3-100 characters. Lowercase ascii with numbers, dashes (-) and underscores (_).|

<h2 id="tocS_UploadUrlResponse">UploadUrlResponse</h2>
<!-- backwards compatibility -->
<a id="schemauploadurlresponse"></a>
<a id="schema_UploadUrlResponse"></a>
<a id="tocSuploadurlresponse"></a>
<a id="tocsuploadurlresponse"></a>

```json
"https://kiri-user-uploads.s3.eu-central-1.amazonaws.com/acc_id/some-model.zip"

```

Upload url response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Upload url response|string|false|none|none|

<h2 id="tocS_ModelsResponse_inner">ModelsResponse_inner</h2>
<!-- backwards compatibility -->
<a id="schemamodelsresponse_inner"></a>
<a id="schema_ModelsResponse_inner"></a>
<a id="tocSmodelsresponse_inner"></a>
<a id="tocsmodelsresponse_inner"></a>

```json
{
  "id": "model_model-name",
  "name": "model-name",
  "description": "Some description about model-name",
  "tasks": [
    "text-generation",
    "qa"
  ],
  "build_status": "building",
  "last_deployment": "2021-03-05T10:31:16Z"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|none|
|name|string|false|none|none|
|description|string|false|none|none|
|tasks|[string]|false|none|none|
|build_status|string|false|none|none|
|last_deployment|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|build_status|success|
|build_status|building|
|build_status|fail|

