# Bolero Simple Template

[![Build](https://github.com/fsbolero/Template/actions/workflows/build.yml/badge.svg)](https://github.com/fsbolero/Template/actions/workflows/build.yml)
[![Nuget](https://img.shields.io/nuget/vpre/Bolero.Templates?logo=nuget)](https://nuget.org/packages/Bolero.Templates)


This template can be used as a base to create a [Bolero](https://github.com/intellifactory/bolero) application.

To learn more, you can check [the documentation](https://fsbolero.io/docs).

## Requirements

To get started, you need the following installed:

* .NET SDK 8.0. Download it [here](https://dotnet.microsoft.com/download/dotnet/8.0).

## Creating a project based on this template

To create a project based on this template, first install the template to your local dotnet:

```
dotnet new -i Bolero.Templates
```

Then, you can create a project like so:

```
dotnet new bolero-app -o YourAppName
```

This will create a project in a new folder named `YourAppName`.

## Template options

You can use the following options to customize the project being created:

* Project content options:

    * `--minimal`, `-m`:

        If `true`, the created project is a minimal application skeleton with empty content.

        If `false` (the default), the created project includes Bolero features such as routed pages, HTML templates and remoting.

    * `--render`, `-r`:

        Determines the render mode. Can be one of:

        * `InteractiveWebAssembly` (the default) for client-side interactive render mode.

        * `InteractiveServer` for server-side interactive render mode (see https://learn.microsoft.com/en-us/aspnet/core/blazor/components/render-modes?view=aspnetcore-8.0).

        * `InteractiveAuto` for automatic interactive render mode (client-side if available, otherwise server-side while downloading the client-side runtime in the background).

        * `WebAssembly` for client-only WebAssembly without a server project.

        * `LegacyServer` for classic (pre-.NET 8) server-side mode.

        * `LegacyWebAssembly` for classic (pre-.NET 8) client-side mode.

    * `--hostpage`, `-hp`:

        Determines how the server-side HTML page content is written for `LegacyServer`. Can be one of:

        * `bolero` (the default): using Bolero.Html functions.

        * `razor`: using a dynamically-compiled Razor page.

        * `html`: using a plain .html file.

        This is ignored if `render` is not `LegacyServer`.

    * `--html`, `-ht`:

        If `true` (the default), use HTML templates.

        If `false`, use F# functions for HTML content.

        This is ignored if `minimal=true`, because the minimal project doesn't contain any HTML content.

    * `--hotreload`, `-hr`:

        Enable hot reloading for HTML templates.

        The default is `true`.

        This is ignored if `server=false`, because hot reloading requires a server side.

    * `--pwa`, `-pwa`:

        Create the client side as a progressive web app.

* Package management options:

    * `--paket`, `-p`:

        Use [Paket](https://fsprojects.github.io/paket) for package management.

    * `--nightly`, `-ni`:

        Reference the "nightly" prerelease of Bolero.

        Starting with version 0.18, prereleases are published through GitHub Packages, and therefore require authentication.
        Make sure that you have set it up before creating your project:

        * Create a GitHub Personal Access Token [on this page](https://github.com/settings/tokens) with permission "read:packages".

        * If you use the default NuGet for package management, add the source with the following command:

            ```sh
            dotnet nuget add source https://nuget.pkg.github.com/fsbolero/index.json -n "Bolero nightly" -u GITHUB_USERNAME -p GITHUB_TOKEN
            ```

        * If you use Paket, use the following command instead:

            ```sh
            dotnet paket config add-credentials https://nuget.pkg.github.com/fsbolero/index.json --username GITHUB_USERNAME --password GITHUB_TOKEN
            ```

## Using this template

Visual Studio Code or Visual Studio is recommended to edit this project.

To compile the project, you can run:

```shell
dotnet build
```

To run it:

```shell
dotnet run -p src/YourAppName.Server

# Or if you created the project with --server=false:
dotnet run -p src/YourAppName.Client
```

## Project structure

* `src/YourAppName.Client` is the project that gets compiled to WebAssembly, and contains your client-side code.

    * `Startup.fs` sets up Blazor to get the application started.

    * `Main.fs` contains the main body of the page.

* `src/YourAppName.Server` is the host ASP.NET Core application, and contains your server-side code.

## Learn more about Bolero

To learn more about Bolero, you can check [the documentation](https://fsbolero.io/docs).
