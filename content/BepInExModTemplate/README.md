# BepInExModTemplate

Describe your project here!

## Template Instructions

You can remove this section after you've set up your project.

Next steps:

- Create a copy of the `Config.Build.user.props.template` file and name it `Config.Build.user.props`
  - This will automate copying your plugin assembly to `BepInEx/plugins/`
  - Configure `MiniCozyRoomLoFiGameRootDir`, `MiniCozyRoomLoFiPluginsDir`, and `MiniCozyRoomLoFiManagedDir` to match your real Mini Cozy Room: Lo-Fi installation
  - `MiniCozyRoomLoFiManagedDir` is currently required for local game assembly references and is not derived automatically from `MiniCozyRoomLoFiGameRootDir`
  - Game assembly references will work once the managed assemblies path is configured correctly
- Search `TODO` in the whole project to see what you should configure or modify

> [!IMPORTANT]
> This template intentionally avoids guessing the Mini Cozy Room: Lo-Fi install directory, executable name, or `*_Data` directory. Update the generated local paths before relying on auto-deploy or local game references.
> `MiniCozyRoomLoFiGameRootDir` is currently only a reserved root path for your own configuration and does not auto-derive `MiniCozyRoomLoFiManagedDir`.

### Thunderstore Packaging

This template comes with Thunderstore packaging built-in, using [TCLI](<https://github.com/thunderstore-io/thunderstore-cli>).

You can build Thunderstore packages by building with release configuration:

```sh
dotnet build -c Release -v d
```

> [!NOTE]  
> You can learn about different build options with `dotnet build --help`.  
> `-c` is short for `--configuration` and `-v d` is `--verbosity detailed`.

The built package will be found at `artifacts/thunderstore/`.
