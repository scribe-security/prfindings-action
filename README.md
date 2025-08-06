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
