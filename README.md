# Build Raycast Extension

This simple __GitHub Action__ builds and (optionally!) lints a [custom extension](https://github.com/raycast/extensions) for [Raycast](https://raycast.com/), making sure that it passes Raycast's basic checks and is ready to publish.

## Getting started

Create a `.github/workflows/build.yml` file in your repo with the following contents:

```yaml
name: Build Raycast extension

on:
  - push

jobs:
  build:
    # We use the `macos-latest` GitHub Actions runner, because Raycast's `ray` CLI only works on macOS.
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v2
      # You don't have to specify any options here, although there are some non-mandatory options - see below!
      - uses: timrogers/build-raycast-extension@1.0.0
```

Commit this to `main`, and your Raycast extension will be automatically built and linted whenever you push to GitHub.

## Options

| Name           | Description                                                                                                                                                                                                                                                                                                                        | Required | Default |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------|
| extension_path | The relative path within your repo where the Raycast extension is located. We will expect `package.json` and `package-lock.json` files to be found here. This is useful if you have multiple extensions in one repo - for example if you're using Raycast for Teams (<https://developers.raycast.com/teams-beta/getting-started>). | false    | .       |
| lint           | Whether the code should be linted to check its style and formatting.                                                                                                                                                                                                                                                               | false    | true    |

You can set options using `with:`, like follows:

```yaml
name: Build Raycast extension

on:
  - push

jobs:
  build:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v2
      - uses: timrogers/build-raycast-extension@v1.0.0
        with:
          extension_path: my_second_extension
```

## Limitations

This action does not allow you to log in to your Raycast developer account, so some linting checks are skipped (namely making sure that you have access to the `owner` team, if you're building for Raycast for Teams (<https://developers.raycast.com/teams-beta/getting-started>).
