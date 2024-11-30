# Documentation for the Serlo Editor format stored into AMB

## 1. The content format of the serlo editor

The content format of the [Serlo Editor](https://serlo.org/editor) is a structured system that organizes educational materials into distinct, logical components called "plugins." Each plugin represents a specific type of content—such as text, equations, or interactive elements — and is defined in JSON format with two key attributes:

- **Plugin name**: Identifies the type of content (e.g., "text," "geogebra").
- **State**: Contains the data necessary to render the plugin, which varies based on the plugin type.

For example, embedding a GeoGebra applet with the ID `nnrmthf4` is represented as:

```json
{
  "plugin": "geogebra",
  "state": "nnrmthf4"
}
```

Multiple plugins are combined using a "rows" plugin, allowing for the creation of complex educational content by nesting various plugin types. This modular approach enables flexibility and scalability in content creation, facilitating the integration of diverse educational resources. In the following structure describes a list of a text plugin followed by a geogebra plugin:

```json
{
  "plugin": "rows",
  "state": [
    {
      "plugin": "text",
      "state": [
        {
          "type": "p",
          "children": [ { "text": "Hello World!" }]
        }
      ]
    },
    {
      "plugin": "geogebra",
      "state": "nnrmthf4"
    }
  ]
}
```

For a comprehensive overview, please refer to the [content format documentation of the serlo editor](https://github.com/serlo/documentation/wiki/Content-format).

## 2. Integration into AMB

This structure can be stored into AMB via the `content` property. In order to define it in JSON-LD we use the [`@json`](https://w3c.github.io/json-ld-syntax/#dfn-json-literal) literal:

```json
{
  "@context": [
    "https://w3id.org/kim/amb/context.jsonld",
    {
      "@language": "de",
      "content": "@json"
    }
  ],
  "id": "https://serlo.org/1495",
  "type": [
    "LearningResource",
    "Article"
  ],
  "content": {
    "plugin": "rows",
    "state": [
      {
        "plugin": "text",
        "state": [
          { "type": "p", "children": [{ "text": "Hello World!" }] }
        ]
      },
      {
        "plugin": "geogebra",
        "state": "nnrmthf4"
      }
    ]
  }
}
```
    
