# angular-material-tools

[Angular-Material](http://github.com/angular/material) deploys standard builds to NPM and Bower using the [Bower-Material](http://github.com/angular/bower-material) deployment repository.

The **standard** build contains all material components, all themes, and all layout features... packaged for easy installs and usages.

Now developers can use `material-tools` to generate their own custom [Angular-Material v1.x](http://github.com/angular/material) builds:

*  Using only a subset of components.
*  Using only 1 specific theme.
*  Using only the Layout API.

> Support for Angular Material v2 may be added in the future.

## Quick Links
- [Installation](#installation)
- [CLI Usage](#cli-usage)
- [NodeJS Usage](#nodejs-usage)
- [NodeJS with TypeScript Usage](#ts-usage)

## Installation

- `npm install angular-material-tools --save`

## Usage

`material-tools` can be easily used from the **command-line** or from your own custom **NodeJS** code. The build tools also include a CLI, which can be used by installing the tools globally.
- `npm install -g angular-material-tools`

#### CLI usage

To create a custom Angular Material build with the command-line interface (CLI), you can pass the following [options](#options) as CLI arguments. All possible options in the CLI can be listed with the command:

  - `material-tools --help`

The CLI includes the following commands:

|                Name                 |              Arguments              |                             Description                                     |
| ----------------------------------- | ----------------------------------- | --------------------------------------------------------------------------- |
| `<arguments>`                       | Everything from [options](#options) | Default command that builds all files.                                      |
| `material-tools js <arguments>`     | Everything from [options](#options) | Only builds the JS files.                                                   |
| `material-tools css <arguments>`    | Everything from [options](#options) | Only builds the CSS files                                                   |
| `material-tools theme <arguments>`  | Everything from [options](#options) <br/> `--primary-palette` <br/> `--accent-palette` <br/> `--warn-palette` <br/> `--background-palette` <br/> `--dark` | Only builds the theme files.             |


##### Options

|          Name           |    Type    |                             Description                                    |
| ----------------------- | ---------- | -------------------------------------------------------------------------- |
| `destination` (*)       | `string`   | Target location for the Material build.                                    |
| `modules`               | `string[]` | Modules that should be part of the build.<br/> All modules will be built if nothing is specified.                                                                                                          |
| `version`               | `string`   | Version of Angular Material.<br/> If set to local, it will take the local installed Angular Material version from the node modules                                                                              |
| `theme`                 | `MdTheme`  | Palettes, which will be used to generate a static theme stylesheet.        |
| `cache`                 | `string`   | Directory for caching the downloads                                        |
| `mainFilename`          | `string`   | Name of the entry file that will be loaded to figure out the dependencies. |
| `destinationFilename`   | `string`   | Name to be used as a base for the output files.                            |

> **Note:** The options can also be set in a JSON file whose path can be passed to the tools module.


**Examples**
```bash
material-tools --destination ./output --modules list datepicker autocomplete --version 1.0.0
```

When a version is not specified, the CLI will automatically use the installed Angular Material version from your local `node_modules` directories.
```bash
material-tools -d ./output -m list
```

<br/>

----

#### NodeJS usage

```js
const MaterialTools = require('angular-material-tools');

let tools = new MaterialTools({
  destination: './output',
  version: '1.0.0',
  modules: ['menu', 'checkbox'],
  theme: {
    primaryPalette: 'indigo',
    accentPalette: 'purple',
    warnPalette: 'deep-orange',
    backgroundPalette: 'grey'
  }
});

const successHandler = () => console.log('Build was successful.');
const errorHandler = (error) => console.error(error);

tools.build().then(successHandler).catch(errorHandler);         // Build all JS/CSS/themes

tools.build('js').then(successHandler).catch(errorHandler);     // Only build the JS.
tools.build('theme').then(successHandler).catch(errorHandler);  // Only build the theme.
tools.build('css').then(successHandler).catch(errorHandler);    // Only build the CSS

// You can also build a subset of files.
tools.build('css', 'js');   // Builds both the CSS and the JS.
```


##### Output
|                   File                   |                                   Description                                        |
| ---------------------------------------- | ------------------------------------------------------------------------------------ |
| `angular-material.js`                    | Contains the modules that you specified, as well as their dependencies.              |
| `angular-material.css`                   | CSS files that has the modules you selected, as well as the layout CSS and core CSS. |
| `angular-material.layout-none.css`       | Only contains the modules that you selected, in addition to the core structural CSS. |
| `angular-material.theme.css`             | Static generated theme stylesheet, if it was specified in the options.               |
| `angular-material.layouts.css`           | Standalone Layout stylesheet with class selectors                                    |
| `angular-material.layout-attributes.css` | Standalone Layout stylesheet with attribute selectors                                |


----

#### NodeJS with TypeScript Usage

If you've cloned the repo, a quick way to explore NodeJS usages is to *directly* run TypeScript without precompiling processes. Developers can use [ts-node](https://github.com/TypeStrong/ts-node) which is installed with:

```bash
# Install a TypeScript compiler (requires `typescript` by default).
npm install -g ts-node typescript
```

Then use the command-line to directly run the `debug.ts` sample from the project root:

```bash
ts-node debug.ts
```

which will generate the output:

```bash
[13:37:00]: Successfully built list, core, animate, layout, gestures, theming, palette,
            datepicker, icon, virtualRepeat, showHide.
```


## Authors
* [Paul Gschwendtner](https://github.com/DevVersion)
* [Kristiyan Kostadinov](https://github.com/crisbeto)
