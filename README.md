# JSON Schema to Array Shape Converter
[![Node.js CI](https://github.com/koriym/json-schema-to-array-shape/actions/workflows/nodejs.yml/badge.svg)](https://github.com/koriym/json-schema-to-array-shape/actions/workflows/nodejs.yml)

<img src="images/json-schema-to-array-shape.png" width="250px" alt="logo">

Converts JSON schemas to PHP PHPStan or Psalm compatible `array-shape` format.

## Features

- Convert JSON schemas to `array-shape` format
- Accept multiple schemas.
- Resolve `$ref` references within schemas

## Online Service

You can use the online version of this converter without installing anything on your local machine. Visit the following URL:

[JSON Schema to Array Shape Converter](https://koriym.github.io/json-schema-to-array-shape/)

## Installation

First, clone the repository and navigate into the project directory:

```bash
git clone https://github.com/koriym/json-schema-to-array-shape.git
cd json-schema2array-shape
```

Then, install the dependencies:

```bash
npm install
```
## Option 2: Using External Script

Alternatively, you can use the external script directly in your HTML file without any local installation.

Include the following script in your HTML file:

```
<script src="https://koriym.github.io/json-schema-to-array-shape/array-shape.js"></script>
```

## Usage

To use the converter, include your JSON schemas in a textarea with the ID `jsonSchemas`. The converted array shapes will be displayed in a pre element with the ID `result`.

Here is an example of how you might use this in an HTML file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JSON Schema to Array Shape Converter</title>
    <script src="path/to/array-shape.js"></script>
</head>
<body>
    <textarea id="jsonSchemas"></textarea>
    <button onclick="convertJsonSchemasToArrayShapes()">Convert</button>
    <pre id="result"></pre>
</body>
</html>
```

### Example

You can pass multiple JSON schemas to resolve `$ref` references. Below is an example of how to use this functionality:

#### Input JSON Schemas

```json
{
  "$id": "address.json",
  "type": "object",
  "properties": {
    "street": { "type": "string" },
    "city": { "type": "string" }
  }
}
{
  "$id": "person.json",
  "type": "object",
  "properties": {
    "name": { "type": "string" },
    "address": { "$ref": "address.json" }
  }
}
{
  "$id": "company.json",
  "type": "object",
  "properties": {
    "company_name": { "type": "string" },
    "employees": {
      "type": "array",
      "items": { "$ref": "person.json" }
    }
  }
}
```

#### Output Array Shapes

```php
array{street:string,city:string}
array{name:string,address:array{street:string,city:string}}
array{company_name:string,employees:array<array{name:string,address:array{street:string,city:string>}}
```

## Testing

This project uses Jest for testing. To run the tests, simply use the following command:

```bash
npm test
```
