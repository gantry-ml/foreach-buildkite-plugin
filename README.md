# buildkite-plugin-foreach

A plugin for reducing duplication in buildkite pipelines.
After producing the pipeline, a `buildkite-agent pipeline upload` will be performed to ship the generated pipeline.

## Example
Add the following to your `pipeline.yml`:

```yml
steps:
  - plugins:
    - gantry-ml/foreach#v1.0.0:
        steps: my-steps.yml
        key: env
        foreach:
          - qa
          - stage
          - prod
        wait_between: true
```

## Configuration

### `steps` (Required, string)
The path to a file which will be used as the template. 
This should be just the steps themselves, without the `steps:` mapping.
```yml
- label: Step for {key}
  command: "my-command --input {key}

```

### `foreach` (required, array of string)
The list of values to iterate over.

###  `key` (optiona, string)
The key which will be passed as the current value of the `foreach` array. Your pipeline definition will replace `{key}` with the value of each iteration.
> Default: "key"

### `wait_between` (optional, boolean)
> Default: true