# null-schema

A JSON schema that allows everything.

## Why is this needed?

The [RedHat YAML Language Support](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml) extension on VSCode does not have the option to enable the [JSON Schema Store](http://schemastore.org/json/) and also disable JSON Schema validation (e.g. there is no "none" option in the extension.)

I ran into an issue where my Kyverno policy files would trigger an incorrect JSON Scheme. []Setting the schema to `none` was suggested](https://github.com/redhat-developer/vscode-yaml/discussions/768#discussioncomment-3890247), but this caused the error `Unable to load schema from '/none': No content.` in my linter. 

If the extension won't provide a "none" option, we can point it to a valid schema that allows all valid properties--a null schema.

## Usage

In your `settings.json` for VSCode, add the null-schema to your `yaml.schemas` configuration, along with an appropriate glob for your use case. This will override any ill-suited schemas from the JSON Schema Store.

```json
"yaml.schemas": {    
  "https://raw.githubusercontent.com/dbowling/null-schema/refs/heads/main/null.schema.json": [
    "**/kyverno/**/*"   
  ]
}
```

## Community discussion

The following is a list of some of the community discussions around the issue:

* [How to set Schema to No JSON Schema #768](https://github.com/redhat-developer/vscode-yaml/discussions/768)
* [Ability to specify schema as a comment in the YAML file #401](https://github.com/redhat-developer/vscode-yaml/issues/401#issuecomment-1398783128)
