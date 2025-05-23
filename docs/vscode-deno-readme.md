# Deno for Visual Studio Code

This extension adds support for using [Deno](https://deno.com/) with Visual
Studio Code, powered by the Deno language server.

> ⚠️ **Important:** You need to have a version of Deno CLI installed (v1.13.0 or
> later). The extension requires the executable and by default will use the
> environment path. You can explicitly set the path to the executable in Visual
> Studio Code Settings for `deno.path`.
>
> [Check here](https://docs.deno.com/runtime/) for instructions on how to
> install the Deno CLI.

![Basic Usage of the Extension](./screenshots/basic_usage.gif)

## Features

- Type checking for JavaScript and TypeScript, including quick fixes, hover
  cards, intellisense, and more.
- Integrates with the version of the Deno CLI you have installed, ensuring there
  is alignment between your editor and the Deno CLI.
- Resolution of modules in line with Deno CLI's module resolution strategy
  allows caching of remote modules in Deno CLI's cache.
- Integration to Deno CLI's linting functionality, including inline diagnostics
  and hover cards.
- Integration to Deno CLI's formatting functionality.
- Allow specifying of import maps and TypeScript configuration files that are
  used with the Deno CLI.
- [Auto completion for imports](./docs/ImportCompletions.md).
- [Workspace folder configuration](./docs/workspaceFolders.md).
- [Testing Code Lens](./docs/testing.md).
- [Provides Tasks for the Deno CLI](./docs/tasks.md).

## Configuration

You can control the settings for this extension through your VS Code settings
page. You can open the settings page using the `Ctrl+,` keyboard shortcut. The
extension has the following configuration options:

- `deno.enable`: Controls if the Deno Language Server is enabled. When enabled,
  the extension will disable the built-in VSCode JavaScript and TypeScript
  language services, and will use the Deno Language Server (`deno lsp`) instead.
  _boolean, default `false`_
- `deno.disablePaths`: Controls if the Deno Language Server is disabled for
  specific paths of the workspace folder. Defaults to an empty list.
- `deno.enablePaths`: Controls if the Deno Language Server is enabled for only
  specific paths of the workspace folder.
- `deno.path`: A path to the `deno` executable. If unset, the extension will use
  the environment path to resolve the `deno` executable. If set, the extension
  will use the supplied path. The path should include the executable name (e.g.
  `/usr/bin/deno`, `C:\Program Files\deno\deno.exe`).
- `deno.cache`: Controls the location of the cache (`DENO_DIR`) for the Deno
  language server. This is similar to setting the `DENO_DIR` environment
  variable on the command line.
- `deno.cacheOnSave`: Controls if the extension should cache the active
  document's dependencies on save.
- `deno.codeLens.implementations`: Enables or disables the display of code lens
  information for implementations for items in the code. _boolean, default
  `false`_
- `deno.codeLens.references`: Enables or disables the display of code lens
  information for references of items in the code. _boolean, default `false`_
- `deno.codeLens.referencesAllFunctions`: Enables or disables the display of
  code lens information for all functions in the code. Requires
  `deno.codeLens.references` to be enabled as well. _boolean, default `false`_
- `deno.codeLens.test`: Enables or disables the display of test code lens on
  Deno tests. _boolean, default `false`_. _This feature is deprecated, see
  `deno.testing` below_
- `deno.codeLens.testArgs`: Provides additional arguments that should be set
  when invoking the Deno CLI test from a code lens. _array of strings, default
  `[ "--allow-all" ]`_.
- `deno.config`: The file path to a configuration file. This is the equivalent
  to using `--config` on the command line. The path can be either be relative to
  the workspace, or an absolute path. It is recommended you name this file
  either `deno.json` or `deno.jsonc`. _string, default `null`, examples:
  `./deno.jsonc`, `/path/to/deno.jsonc`, `C:\path\to\deno.jsonc`_
- `deno.documentPreloadLimit`: Maximum number of file system entries to traverse
  when finding scripts to preload into TypeScript on startup. Set this to `0` to
  disable document preloading.
- `deno.importMap`: The file path to an import map. This is the equivalent to
  using `--import-map` on the command line.
  [Import maps](https://docs.deno.com/runtime/fundamentals/configuration/#dependencies)
  provide a way to "relocate" modules based on their specifiers. The path can
  either be relative to the workspace, or an absolute path. _string, default
  `null`, examples: `./import_map.json`, `/path/to/import_map.json`,
  `C:\path\to\import_map.json`_
- `deno.inlayHints.enumMemberValues.enabled` - Enable/disable inlay hints for
  enum values.
- `deno.inlayHints.functionLikeReturnTypes.enabled` - Enable/disable inlay hints
  for implicit function return types.
- `deno.inlayHints.parameterNames.enabled` - Enable/disable inlay hints for
  parameter names. Values can be `"none"`, `"literals"`, `"all"`.
- `deno.inlayHints.parameterNames.suppressWhenArgumentMatchesName` - Do not
  display an inlay hint when the argument name matches the parameter.
- `deno.inlayHints.parameterTypes.enabled` - Enable/disable inlay hints for
  implicit parameter types.
- `deno.inlayHints.propertyDeclarationTypes.enabled` - Enable/disable inlay
  hints for implicit property declarations.
- `deno.inlayHints.variableTypes.enabled` - Enable/disable inlay hints for
  implicit variable types.
- `deno.inlayHints.variableTypes.suppressWhenTypeMatchesName` - Suppress type
  hints where the variable name matches the implicit type.
- `deno.internalDebug`: If enabled the Deno Language Server will log additional
  internal diagnostic information.
- `deno.internalInspect`: Enables the inspector server for the JS runtime used
  by the Deno Language Server to host its TS server.
- `deno.lint`: Controls if linting information will be provided by the Deno
  Language Server. _boolean, default `true`_
- `deno.maxTsServerMemory`: Maximum amount of memory the TypeScript isolate can
  use. Defaults to 3072 (3GB).
- `deno.suggest.imports.hosts`: A map of domain hosts (origins) that are used
  for suggesting import auto completions. (See:
  [ImportCompletions](./docs/ImportCompletions.md) for more information.)
- `deno.testing.args`: Arguments to use when running tests via the Test
  Explorer. Defaults to `[ \"--allow-all\" ]`.
- `deno.unstable`: Controls if code will be executed with Deno's unstable APIs.
  Affects execution which is triggered through the extension, such as test code
  lenses. This is the equivalent to using `--unstable` on the command line.
  _boolean, default `false`_

## Compatibility

To see which versions of this extension can be used with each version of the
Deno CLI, consult the following table.

| Deno CLI        | vscode-deno     |
| --------------- | --------------- |
| 1.40.0 onwards  | 3.40.0 onwards  |
| 1.37.2 - 1.39.4 | 3.34.0 - 3.39.0 |
| 1.37.1          | 3.32.0 - 3.33.3 |
| 1.37.0          | 3.28.0 - 3.31.0 |
| ? - 1.36.4      | 3.27.0          |

Version ranges are inclusive. Incompatibilities prior to 3.27.0 were not tracked.
