# Mini Cozy Room: Lo-Fi BepInEx Template

- [Mini Cozy Room: Lo-Fi BepInEx Template](#mini-cozy-room-lo-fi-bepinex-template)
  - [Installing](#installing)
    - [From NuGet (Recommended)](#from-nuget-recommended)
    - [Manually](#manually)
  - [Creating a Project](#creating-a-project)
    - [Project Structure](#project-structure)
    - [Setting Up The Config File](#setting-up-the-config-file)
    - [Thunderstore Packaging](#thunderstore-packaging)
    - [GitHub Actions Publishing](#github-actions-publishing)

This repository provides a `dotnet new` template tailored for **Mini Cozy Room: Lo-Fi** BepInEx plugin development.

## Installing

.NET templates must be installed before they can be used. Installing the template adds it to `dotnet new`; it does not create a project by itself.

> [!NOTE]
> You must use .NET SDK 10 or newer to use this template. Check your SDK version with `dotnet --version`. To download .NET SDK, see: <https://dotnet.microsoft.com/en-us/download>

### From NuGet (Recommended)

Run:

```bash
dotnet new install MiniCozyRoomLoFiModding.BepInExTemplate
```

> [!TIP]
> You can run `dotnet new update` to update installed templates.

### Manually

If you are contributing to the template or prefer a local install:

1. Clone or download this repository.
2. Open a terminal at the repository root.
3. Run:

```bash
dotnet new install .
```

To update a locally installed copy:

```bash
dotnet new install . --force
```

To uninstall:

```bash
dotnet new uninstall .
```

Once installed, the template appears as `Mini Cozy Room: Lo-Fi BepInEx Plugin` with short name `mcrlfmod`.

## Creating a Project

Open a terminal in your Mini Cozy Room: Lo-Fi modding workspace and run:

> [!NOTE]
> If you plan to publish to Thunderstore, create a Thunderstore team first so you can pass its name with `--ts-team`.

```sh
dotnet new mcrlfmod --output ModName --guid com.github.YourAccount.ModName --ts-team YourThunderstoreTeam
```

> [!TIP]
> If you are developing a public API, add `--library` to include NuGet metadata scaffolding.
>
> You can also use `--no-tutorial` to remove tutorial comments.
>
> Run `dotnet new mcrlfmod --help` to see all options.

This creates a new directory containing your plugin project.

### Project Structure

Example:

```sh
~/Workspace/MiniCozyRoomLoFi$ dotnet new mcrlfmod --output MyCoolMod --guid com.github.YourAccount.MyCoolMod --ts-team YourThunderstoreTeam
The template "Mini Cozy Room: Lo-Fi BepInEx Plugin" was created successfully.

~/Workspace/MiniCozyRoomLoFi$ cd MyCoolMod/
~/Workspace/MiniCozyRoomLoFi/MyCoolMod$ tree
.
├── CHANGELOG.md
├── Config.Build.user.props.template
├── Directory.Build.props
├── Directory.Build.targets
├── icon.png
├── LICENSE
├── MyCoolMod.slnx
├── README.md
└── src
    └── MyCoolMod
        ├── MyCoolMod.csproj
        ├── Plugin.cs
        └── thunderstore.toml

3 directories, 12 files
```

Your mod source files live in `./src/<project-name>/`. Files above that level contain shared project configuration.

### Setting Up The Config File

At the root of your generated project, copy `Config.Build.user.props.template` to `Config.Build.user.props`.

That file controls optional deployment to your local BepInEx plugins directory and the local game assembly references used for development.

> [!IMPORTANT]
> This template deliberately does **not** hardcode a presumed Mini Cozy Room: Lo-Fi install path, executable name, or `*_Data` directory name.
> You must update the generated `Config.Build.user.props` values to match your real installation before relying on local deployment or local game references.
> In particular, `MiniCozyRoomLoFiManagedDir` currently must be set explicitly for local game references.
> `MiniCozyRoomLoFiGameRootDir` is currently only a reserved root path for your own configuration and does **not** auto-derive `MiniCozyRoomLoFiManagedDir`.

If `DeployModFilesEnabled` stays `true`, make sure your configured plugins directory already exists, typically under your game's `BepInEx/plugins/` folder.

You may still configure `MiniCozyRoomLoFiPluginsDir` separately if you want build output copied to a local `BepInEx/plugins/` directory.

### Thunderstore Packaging

This template includes Thunderstore packaging via [TCLI](<https://github.com/thunderstore-io/thunderstore-cli>).

Before publishing, review `src/<project-name>/thunderstore.toml` and replace placeholder values such as your package description, repository URL, and the Thunderstore community identifier if applicable.

The community slug for Mini Cozy Room: Lo-Fi is intentionally left as a placeholder in this repository because it has not been safely confirmed.

You can build a Thunderstore package by running:

```sh
dotnet build -c Release -v d
```

The built package will be placed in `artifacts/thunderstore/`.

You can also publish with TCLI by adding `-property:PublishTS=true`, once the Thunderstore metadata is configured correctly.

### GitHub Actions Publishing

Coming soon.
