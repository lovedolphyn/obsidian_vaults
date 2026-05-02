## Updating The CLI Data For Future Runs

You will likely want to re-run the CLI tool at some point. The instructions below can be used to update the data so you can re-run the process.

>[!danger] This was written for Windows, **NOT** Linux...so check back on the Linux instructions to apply these updates. (Obsidian TTRPG Tutorials website)

#### Update The 5eT Data

Navigate to your `bin/5etools-src` folder. Click in the `Address Bar` and type `cmd` and press `Enter`. This will open the Command Prompt from this location.  
Type: `git pull` and press enter. This will update to the latest release.

#### Update The 5eT Images

Navigate to your `bin/5etools-img` folder. Click in the `Address Bar` and type `cmd` and press `Enter`. This will open the Command Prompt from this location.  
Type: `git pull` and press enter. This will update to the latest release.

#### Update the CLI Executable

Navigate to the [ttrpg-convert-cli/releases](https://github.com/ebullient/ttrpg-convert-cli/releases) page and check for the latest release (do not use the Pre-release unless you know what you are doing). Download the latest windows release (ttrpg-convert-cli-X.X.X-windows-x86_64.zip).  
Export the downloaded zip file and copy the `ttrpg-convert.exe` into your `bin` folder. This will over-ride the old version.

#### Make Changes To Your Config File

Assuming the reason you want to re-run the process is there's a new book you would like to add to your vault; don't forget to add the book to your config file.

#### Rerun the CLI

Go back to [TTRPG-Convert-CLI 5e > Are You Ready?](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Plugin+Tutorials/Community+Plugins/TTRPG-Convert-CLI/TTRPG-Convert-CLI+5e#Are%20You%20Ready?) and re-run the CLI command.