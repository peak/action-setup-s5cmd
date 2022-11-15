# action-setup-s5cmd

Action to install [`s5cmd`](https://github.com/peak/s5cmd) to use with GitHub Actions.

## Usage

```yml
name: Sync assets to S3
on:
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    name: Sync
    steps:
      - name: Set-up s5cmd
        uses: peak/action-setup-s5cmd@main
        with:
          version: v2.0.0

      - name: Checkout
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Sync files
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        run: | 
          s5cmd sync 'static/*' 's3://bucket/prefix/'
```

### Inputs

| Input   | type     | required | default  | description                       |
| ------- | ---      | -------- | -------  | -----------                       |
| version | `string` | `false`  | `v2.0.0` | Release tag of binary to download. |

