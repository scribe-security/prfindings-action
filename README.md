GitHub Action to run [prfindings](https://github.com/scribe-security/prfindings) in Docker.

## Example

```yaml
- name: Run prfindings findings processor
  uses: scribe-security/prfindings-action@v1
  with:
    config_file: ./config.yml
    env_file: ./.env
    output_dir: ${{ github.workspace }}/prfindings-output
    params_envs: |
      GITHUB_TOKEN:${{ secrets.GITHUB_TOKEN }}
      OPENAI_TOKEN:${{ secrets.OPENAI_TOKEN }}
```

## Inputs

| Name          | Required | Description |
|---------------|----------|-------------|
| `config_file` | Yes      | Path to the prfindings `config.yml`. |
| `env_file`    | No       | Path to a `.env` file with key=value pairs. |
| `output_dir`  | Yes      | Directory where prfindings will write results. Mounted into the container. |
| `params_envs` | No       | Multiline string of `KEY:VALUE` pairs. Secrets should be passed through `${{ secrets.* }}`. |



## Outputs

All logs, tool results, and generated files are written to the directory specified in output_dir. 

## Permissions

If prfindings needs to interact with GitHub (for example creating pull requests), ensure the workflow has appropriate permissions:

```yaml
permissions:
  contents: write
  pull-requests: write
  packages: read
```


## Notes

The container runs as a non-root user. Ensure the output directory is writable in CI jobs:
```yaml
- run: mkdir -p ${{ github.workspace }}/prfindings-output && chmod -R 777 ${{ github.workspace }}/prfindings-output
```

