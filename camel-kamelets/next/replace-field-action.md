# ![replace field action](_images/kamelets/replace-field-action.svg) Replace Field Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Renames fields of each message that is a JSON object, and can also keep only some fields or remove others.

Use it to match the field names another system expects, such as `name` to `fullName`, and to leave out the fields it should not get. To remove a single field, `drop-field-action` is simpler; to hide a value but keep the field, use `mask-field-action`.

Input: a JSON object, as JSON text or as parsed JSON (a Map or a Jackson `JsonNode`). Only the fields at the top level of the object are renamed, kept or removed; nested objects are left as they are. A JSON array, or a body that is not JSON, fails.

Output: the object with the renamed fields, without the removed ones; the order of its fields can change. When the `Content-Type` header is `application/json`, the body is JSON text again; otherwise it is parsed JSON (a Jackson `JsonNode`), which `json-serialize-action` turns into JSON text.

Good to know: `renames` is required, even when you only want to keep or remove fields. A rename of a field the object does not have is ignored. When `enabled` and `disabled` together would remove every field, the object is passed on unchanged.

## Configuration Options

The following table summarizes the configuration options available for the `replace-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **renames** | Renames | **Required** The fields to rename, as `old:new` pairs separated by commas. Only top-level fields are renamed; naming a field nested inside an object has no effect. A pair without `:` makes every message fail. | string |  | name:fullName,zip:postalCode |
| **disabled** | Disabled | The names of the top-level fields to remove, separated by commas. The default, `none`, removes nothing. | string | none | card,password |
| **enabled** | Enabled | The names of the top-level fields to keep, separated by commas; all the other fields are removed. The default, `all`, keeps every field. | string | all | id,name |

## Dependencies

At runtime, the `replace-field-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:kafka
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:replace-field-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Replace Field Action Kamelet Description

### Scope

Only top level fields are considered. Fields nested inside an object are passed through untouched, so a rename that names a nested field has no effect.

The `enabled` and `disabled` properties filter on the same top level keys.

For example, with a body of `{"message":{"Hola":"mundo"}}`, renaming `message` works while renaming `Hola` does nothing.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/replace-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/replace-field-action.kamelet.yaml)