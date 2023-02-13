# balena.yml Action

A basic GitHub action for automating changes to balena.yml.

- sync_readme: Mirror the GitHub README into the Balena Hub README.
- sync_tag: Match the Balena Hub version number with the pushed tag.

```
name: Deploy to BCR

on:
  push:
    tags:
      - "*.*.*"

jobs:
  deploy-to-bcr:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Update balena.yml
        uses: balena-io-experimental/balena.yml-action@main
        with:
          path: ./
          sync_readme: true
          sync_tag: true

      - name: Deploy to Balena
        uses: balena-io/deploy-to-balena-action@master
        with:
          balena_token: ${{ secrets.BALENA_TOKEN }}
          fleet: maggie0002/test-block
```
