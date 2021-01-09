# tool-new-release process

At the moment, the tool only handles minor version bumps and requires you to specify the version:

```bash
# Going from 3.23 (current) to 3.24 (new)
tool-new-release --version 3.24.0

To start the release process using `tool-new-release`:

1. Go to the [releases page](https://github.com/ember-learn/tool-new-release/releases)
2. Find the most recent **draft**

   <img width="900" alt="The top of the page shows the most recent draft" src="https://user-images.githubusercontent.com/16869656/104086072-db9a8700-5254-11eb-84af-6319f59254d4.png">
3. Expand the **Assets** panel

    <img width="900" alt="Click Assets to see a binary for each operating system" src="https://user-images.githubusercontent.com/16869656/104086120-41870e80-5255-11eb-8500-8102684db40f.png">

4. Download the binary that corresponds to your operating system
5. Run the binary. If you are on macOS, you will need to right-click on the binary file, then click **Open** to bypass security check (the binary is not signed).

    <img width="900" alt="On Mac, right-click on the binary file and click Open" src="https://user-images.githubusercontent.com/16869656/104086195-ed305e80-5255-11eb-97e1-00388e2ba85c.png">
6. Carefully follow the instructions presented in the terminal

For more information about tool-new-release, please see [README](https://github.com/ember-learn/tool-new-release).
