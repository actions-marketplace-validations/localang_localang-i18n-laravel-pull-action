# I18n Laravel Pull Action

> ⚠️ **Deprecated — no longer functional.** This action synchronized translations with the
> hosted Localang service, which has been **discontinued**. It is kept for reference only.
> The [localang-i18n-js](https://github.com/pavelpilyak/localang-i18n-js) library and its
> ESLint plugin remain usable standalone.

This action pulls i18n keysets from the hosted Localang service to your Laravel project.

## Inputs

### `api-key`

**Required** API Key to update translations on [localang.xyz](https://localang.xyz). [See documentation](https://docs.localang.xyz/docs/localang/api#obtaining-a-token)

### `project-id`

**Required** ID of project on [localang.xyz](https://localang.xyz). [See documentation](https://docs.localang.xyz/docs/localang/api#project-id)

## Example workflow

**.github/workflows/pull-translations.yaml**:

```yaml
name: Pull Translations from Localang

on:
  schedule:
    - cron:  '0 * * * *'

jobs:
  push-translations:
    runs-on: ubuntu-latest

    steps:
      - name: Check out the repository
        uses: actions/checkout@v3

      - name: Pull translations
        uses: pavelpilyak/localang-i18n-laravel-pull-action@v0.0.1
        with:
          api-key: ${{ secrets.LOCALANG_API_KEY }}
          project-id: 1

      - name: Commit translations
        run: |
          git config --global user.name 'Localang'
          git config --global user.email 'localang@users.noreply.github.com'
          git commit -am "Automatic translation merge"
          git push
```