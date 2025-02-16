# Sample Interview App - Full Stack

## Reservation Management System

This repo is a barebones Reservation Management system that (almost)
allows guests to book rooms.

## Running the App

Ensure you have the following software installed:

> [!NOTE]
> Links to everything used are in the bottom [References](#References) section

- git
- dotnet 8 (tested with sdk 8.0.104 / 8.0.204 / 8.0.303 / 8.0.400)
- node (v20)
- caddy

<details>

<summary>MacOS Instructions</summary>

If you are on a mac, get homebrew so you can quickly install everything:

```sh
brew install git
brew install dotnet-sdk
dotnet --list-sdks

# I recommend fnm to manage node
brew install fnm
fnm install 20
node --version # expect at least v20

brew install caddy
```

</details>

<details>

<summary>Windows Instructions</summary>

If you are on a windows, get chocolatey so you can quickly install everything:

```ps1
choco install git
choco install dotnet
dotnet --list-sdks

# I recommend fnm to manage node
choco install fnm
fnm install 20
node --version # expect at least v20

choco install caddy
```

</details>

<details>

<summary>GNU/Linux Instructions</summary>

If you are on GNU/Linux, use your preferred package manager to quickly install everything:

```sh
# Using apt for Ubuntu, but you get the idea

apt install git

# Will include dependencies: https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-install?tabs=dotnet8&pivots=os-linux-ubuntu-2404#dependencies
apt install dotnet-sdk-8.0
dotnet --list-sdks

# I recommend fnm to manage node
# Instructions here: https://github.com/Schniz/fnm#installation
# See if your package manage has fnm by searching for it, or fallback on the bash/zsh/fish script
curl -fsSL https://fnm.vercel.app/install | bash
fnm install 20
node --version # expect at least v20

apt install caddy
```

</details>

In a terminal, install the project's dependencies in the backend and fronted portions:

```sh
cd api
dotnet build

cd ../ui
npm install

cd ..
caddy adapt
```

Caddy's doc say to run `caddy adapt`, so that was included in the above code block.

With all that done, run the start shell script at the root of this repository to initiate
the api (dotnet), the router (caddy), and the ui (rspack dev server).

```
./start.sh
```

Then navigate to [port 4000](http://localhost:4000) to see the app.
If you go to [/api/swagger](http://localhost:4000/api/swagger) you can see
the interactive swagger docs to test the API.

> [!TIP]
> Sometimes the dotnet watcher gets confused, so we have concurrently configured to forward
> input to the dotnet watcher, so you can press `Ctrl + R` in the terminal to restart the api
> which usually fixes most problems. This only works because we put concurrently in 'raw' mode, so we
> lose the ability to name and color each output in a nice way, unfortunately.

**Seed some data**

Add 5 rooms using the api via [the swagger ui](http://localhost:4000/api/swagger) by
using the `POST /room` endpoint and the "try it out" mode. Feel free to add more data.

<details>
<summary>Expected Rooms JSON</summary>

You can use the `GET /room` to check if the DB has these saved:

```json
[
  {
    "number": "001",
    "state": 0
  },
  {
    "number": "002",
    "state": 0
  },
  {
    "number": "003",
    "state": 0
  },
  {
    "number": "004",
    "state": 0
  },
  {
    "number": "005",
    "state": 0
  }
]
```

</details>

## Backlog

In `/backlog` you will find 'tickets' to pick up to submit, please indicate in the PR
which tickets are closed or partially completed. The tickets use 'must' and 'should' to distinguish
between minimum and ideal experiences.

## API

The API is a C# .NET 8 simple web api, living in api/

The API uses:

- SQLite
- Dapper
- Swagger
- CSharpier (VSCode extension for formatting)

## UI

The UI is a React + TS app, living in ui/

The UI uses:

- TypeScript (Types!)
- React (rendering library)
- Radix UI (headless, accessible component library)
- Radis Theme (more built out components)
- Styled Components (css-in-js library)
- Sonner (toast notifications)
- TanStack Router (manual code style)
- TanStack Query (automatic remote data caching)
- Ky (http client)
- Zod (schema validation)
- RSBuild / RSpack (rust version of webpack)
- Prettier (VSCode extension for formatting)

## References

**CLI Tools**

Things that mostly exist at build time or in the terminal.

- [Git](https://git-scm.com/docs)
- [dotnet cli](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet)
- [Caddy](https://caddyserver.com/docs/)
- [Homebrew](https://brew.sh/)
- [Chocolatey](https://community.chocolatey.org/)
- [fnm](https://github.com/Schniz/fnm)
- [Concurrently](https://github.com/open-cli-tools/concurrently)
- [RSBuild](https://rsbuild.dev/)

**Foundations**

Languages, frameworks, runtimes, and storage engines.

- [C# Language Reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/)
- [Typescript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [.NET](https://learn.microsoft.com/en-us/dotnet/)
- [Nodejs Docs](https://nodejs.org/en)
- [SQLite](https://sqlite.org/docs.html)

**Libraries**

Libraries that have APIs you consume in the codebase.

- [React Docs](https://react.dev/)
- [Dapper](https://www.learndapper.com/)
- [TanStack Router](https://tanstack.com/router/latest/docs/framework/react/overview)
- [TanStack Query](https://tanstack.com/query/latest/docs/react/overview)
- [Ky](https://github.com/sindresorhus/ky)
- [Zod](https://zod.dev/)
- [Styled Components](https://styled-components.com/)
- [Radix UI](https://www.radix-ui.com/)
- [Radix UI Theme](https://www.radix-ui.com/themes/docs/overview/getting-started)
- [Sonner](https://sonner.emilkowal.ski/)
  - See our wrapper in [SuccessToast](./ui/src/components/SuccessToast.tsx)

<details>

<summary>VSCode Extensions</summary>

We purposefully kept most/all editor config outside of this repo,
but if you happen to use VSCode we recommend these extensions for
this repo:

- [Todo Tree](https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree)
- [C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)
- [CSharpier](https://marketplace.visualstudio.com/items?itemName=csharpier.csharpier-vscode)
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [Error Lens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens)
- [Pretty Typescript Errors](https://marketplace.visualstudio.com/items?itemName=yoavbls.pretty-ts-errors)

</details>
