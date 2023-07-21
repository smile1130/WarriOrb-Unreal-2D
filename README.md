## About

WarriOrb is an action platformer where you play as a mighty demon trapped in an unlikely body! Make your way through the ravaged world to regain your freedom and sanity – meeting demons, giants, mutants and all sorts of magical and crazy creatures along the way.

Key Features:
- Trapped in a Ball: Explore a tragic story of loss and desperation hidden behind a comic tale.
- Sweet Freedom: Run, jump, bounce and roll your way to freedom!
- Platforming Skills: It feels like everything is out to get you … - You got that right! Challenge your skills and reflexes against the deadliest of traps.
- Think, Think, Think: Solve challenging puzzles in between traps!
- Get Social: The world is ending! Chat with friendly and unfriendly fellows along the way about it.

![WarriOrb fithing monsters](https://user-images.githubusercontent.com/1269608/110970459-73564780-8362-11eb-8ce1-aa880362cbd9.jpg)

## Building

We provide these sources for our customers, and as a reference for Unreal Engine developers. **You won't be able to run the game from this repository alone**, as the game contents are not included. Building from source is only useful if you want to replace the game executable with your modifications.

### Required dependencies

You will need the following tools to build WarriOrb from the source code:
- **[Unreal Engine 4](https://www.unrealengine.com/)** as the game engine.  You will need to sign up and download the Epic Games launcher. In the launcher library for Unreal Engine, install version **4.22**.
- [Setup Visual Studio 2017 for Unreal Engine](https://docs.unrealengine.com/en-US/Programming/Development/VisualStudioSetup/index.html) - You can download Visual Studio 2017 Community edition from [here](https://visualstudio.microsoft.com/vs/older-downloads/)
  - or after you sign in, directly from [this link](https://my.visualstudio.com/Downloads?q=visual%20studio%202017&wt.mc_id=o~msft~vscom~older-downloads) as Microsoft makes it hard to download VS 2017 (for some reason).
- [Download the **FMOD** plugin (version 1.10.19)](https://www.fmod.com/download) for UE 4.22 and copy the libs Binaries from it, inside `Plugins/FMODStudio/Binaries` directory.
  - You should copy `FMODStudio/Binaries` (after downloading and unzipping) to `Plugins/FMODStudio/Binaries`

### Build


#### 1. Run UnrealBuildTool

The Build command looks like this:
```sh
<engine_install_path>/Engine/Binaries/DotNET/UnrealBuildTool.exe <project_name><target_type> <platform> <build_type> -project=<uproject_absolute_file_path> -progress
```

To build just the Game for Windows 64 run for example:
```sh
"c:/dev/UE/UE_4.22/Engine/Binaries/DotNET/UnrealBuildTool.exe" Warriorb Win64 Development -project="C:/dev/WarriOrb/Warriorb.uproject" -progress
```

NOTE: If you want clean the project before you build, just add the `-clean` flag.

For example:
```sh
"c:/dev/UE/UE_4.22/Engine/Binaries/DotNET/UnrealBuildTool.exe" Warriorb Win64 Development -project="C:/dev/WarriOrb/Warriorb.uproject" -progress -clean
```

NOTE: You can also build the game by opening the `.sln` file in Visual Studio 2017 and building the `Development Game` target.

#### 2. Copy Binaries

The resulting binaries and debug files will be generated inside `Binaries/Win64/` and can replace the equivalent files in your existing game folder (located at `<install_path>/Warriorb/Binaries/Win64/`)

### Run

#### 1. Unarchive pak

The game has the Content inside a `.pak` file which is just an archive. You need to unarchive it with the `UnrealPak` utility.

The pak command utility can be found here:
```sh
<engine_install_path>/Engine/Binaries/Win64/UnrealPak.exe
```

The pak file can be located here:
```sh
<install_path>/Warriorb/Content/Paks/Warriorb-WindowsNoEditor.pak
```

Extract the pak file:
```sh
<engine_install_path>/Engine/Binaries/Win64/UnrealPak.exe <install_path>/Warriorb/Content/Paks/Warriorb-WindowsNoEditor.pak -Extract <install_path>
```

NOTE: All paths must be absolute otherwise this won't work.

For Example:
```sh
"c:/dev/UE/UE_4.22/Engine/Binaries/Win64/UnrealPak.exe" "C:/Program Files (x86)/Steam/steamapps/common/WarriOrb/Warriorb/Content/Paks/Warriorb-WindowsNoEditor.pak" -Extract "C:/Program Files (x86)/Steam/steamapps/common/WarriOrb/"
```
#### 2. Rename paks folder

This is required so that the executable only reads the unarchived files but not the archive itself.

Rename the `<install_path>/Warriorb/Content/Paks/` directory to something like `<install_path>/Warriorb/Content/_OLD_Paks/`

#### 3. Disable `AuraSDKPlugin`

Open the `<install_path>/Warriorb/Warriorb.uproject` file and set the `Enabled` field for the `AuraSDKPlugin` plugin to `false`.

The section should look like this:
```json
{
	"Name": "AuraSDKPlugin",
	"Enabled": false
}
```

#### 4. Run the game
Now you can run the game with the modified executable you built above.

`<install_path>/Warriorb/Binaries/Win64/Warriorb.exe`

Or just the launcher executable in the root directory which calls the above path:
`<install_path>/Warriorb.exe`
