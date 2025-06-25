---
title: Seneki API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - http

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Seneki API
---

# Seneki Calories API

Seneki Calories API provides instant food recognition and calorie estimation through computer vision, Optical Character Recognition (OCR), and Large Language Models (LLMs) to deliver comprehensive food analysis. Our API processes food images to identify items, extract nutritional information, and calculate calories with industry-leading accuracy.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl -X POST "https://seneki-api.com/calories-pic" \
  -H "Ocp-Subscription-Key: <API Subscription key>" \
```


```http
POST https://seneki-api.com/calories-pic HTTP/1.1
Ocp-Subscription-Key: <API Subscription key>
```

> Make sure to replace `<API Subscription key>` with your API key.

Seneki Calories API uses Ocp Subscription keys to allow access to the API. You can register by contact us.

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Ocp-Subscription-Key: <API Subscription key>`

<aside class="notice">
You must replace <code>API Subscription key</code> with your personal API key.
</aside>

# Image-Based Calories Estimation API

You can submit images for generation requests using either of these methods:

 `Image URL`: Provide a full web address to an image file

`(Example: https://example.com/image.png)`

 `Base64 Data URL`: Encode the image as a Base64 string

`(Format: data:image/png;base64,...)`

## Image Input Requirements

Input images must meet the following requirements to be used in the Calories API.

### Supported file types	
`PNG (.png) `

`JPEG (.jpeg and .jpg)`

`WEBP (.webp)`

### Size limits	
Up to 5 MB total payload size per request.

Maximum image size: 1024×1024 pixels.

### Other requirements	
Picture need to be clear enough for a human to understand.

## Image URL


```shell
curl -X POST "https://seneki-api.com/calories-pic" \
  -H "Ocp-Subscription-Key: <API Subscription key>" \
  -d '{
    "image_url": "https://example.com/food.jpg"
  }'
```

```http
POST https://seneki-api.com/calories-pic HTTP/1.1
Ocp-Subscription-Key: <API Subscription key>

{"image_url":"https://example.com/food.jpg"}
```

> The above command returns JSON structured like this:

```json
{
  "result": "Your ·Cheeseburger· has approximately ·300· calories for ·1· serving.",
  "confidence": 0.9
}
```

Use Image URL in Seneki Calories API to estimate food calories.

### HTTP Request

`POST https://seneki-api.com/calories-pic`

### Request Header

Name | Required | Description
--------- | ------- | -----------
Ocp-Subscription-Key | true | API key which offers by Seneki

### Request Body

Name | Required | Description
--------- | ------- | -----------
image_url | true | A web address which could be accessed on Pulic Internet.

<aside class="success">
Remember — Must include API key for authentication.
</aside>

### Response Body

Name | Default | Description
--------- | ------- | -----------
Result | true | The estimated calorie analysis formatted for end-user display. Format:"Your ·[FOOD_ITEM]· has approximately ·[CALORIES]· calories for ·[SERVING_SIZE]· serving."
confidence | true | The system's confidence in the calorie estimation accuracy, represented as a probability value between 0.0 (lowest) and 1.0 (highest). Seneki API would only return result with confidence larger than 0.6.

## Base64 Image

```shell
curl -X POST "https://seneki-api.com/calories-pic" \
  -H "Ocp-Subscription-Key: <API Subscription key>" \
  -d '{
    "image_url": "data:image/png;base64,..."
  }'
```

```http
POST https://seneki-api.com/calories-pic HTTP/1.1
Ocp-Subscription-Key: <API Subscription key>

{"image_url": "data:image/png;base64,..."}
```

> The above command returns JSON structured like this:

```json
{
  "result": "Your ·Cheeseburger· has approximately ·300· calories for ·1· serving.",
  "confidence": 0.9
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Because of the large amount of characters in the base64 image, it may cause the payload to exceed the size it can carry. We recommend using the <code>&lt;Image URL&gt;</code>.</aside>

Use Base64 format in Seneki Calories API to estimate food calories.

### HTTP Request

`POST https://seneki-api.com/calories-pic`

### Request Header

Name | Required | Description
--------- | ------- | -----------
Ocp-Subscription-Key | true | API key which offers by Seneki

### Request Body

Name | Required | Description
--------- | ------- | -----------
image_url | true | A Base64 format image.

### Response Body

Name | Default | Description
--------- | ------- | -----------
Result | true | The estimated calorie analysis formatted for end-user display. Format:"Your ·[FOOD_ITEM]· has approximately ·[CALORIES]· calories for ·[SERVING_SIZE]· serving."
confidence | true | The system's confidence in the calorie estimation accuracy, represented as a probability value between 0.0 (lowest) and 1.0 (highest). Seneki API would only return result with confidence larger than 0.6.



