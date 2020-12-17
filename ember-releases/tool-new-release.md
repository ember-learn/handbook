# tool-new-release process

At the moment the tool only handles minor version bumps and requires the user to specify the version, like so:

```bash
tool-new-release --version 3.24.0
```

To start the release process using `tool-new-release`, do the following:

1. Go to the [releases page](https://github.com/ember-learn/tool-new-release/releases)
2. Find the most recent draft
3. Expand the "Assets" panel
4. Download the binary that corresponds to your operating system
5. Run the binary
5.1. If you are on macOS you will need to right-click and "Open" the binary to get around the security check, since the binary is not signed
6. Follow the instructions presented carefully

For more detailed information refer to the [README](https://github.com/ember-learn/tool-new-release).