# "Get Docker Image Last Layer" Github Action

This Github action inspects a given Docker image and returns the SHA of the last layer.

## Example workflow

````yaml
# …
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
# …
      - name: Determine SHA of last source image layer
        id: source_last_layer
        uses: tobiasge/action-docker-get-last-layer@v1
        with:
          image: netboxcommunity/netbox:latest
          registry_username: github
          registry_password: ${{ secrets.GITHUB_BOT_TOKEN }}
          registry_endpoint: https://docker.pkg.github.com/v2/

      - name: Build Docker image
        uses: docker/build-push-action@v3
        env:
          SOURCE_LAST_LAYER: ${{ steps.source_last_layer.outputs.value }}
        with:
# …        
````
Inspired by https://github.com/flownative/action-docker-get-label