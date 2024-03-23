# Import Cost ![Build Status](https://github.com/wix/import-cost/workflows/build/badge.svg) [![Stand With Ukraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/badges/StandWithUkraine.svg)](https://www.wix.com/stands-with-ukraine)
[![](https://vsmarketplacebadge.apphb.com/version/wix.vscode-import-cost.svg)](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost) [![](https://vsmarketplacebadge.apphb.com/installs/wix.vscode-import-cost.svg)](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost)

This extension will display inline in the editor the size of the imported package.
The extension utilizes webpack in order to detect the imported size.

![Example Image](https://citw.dev/posts/import-cost/1quov3TFpgG2ur7myCLGtsA.gif)

This project includes implementation of:
 * Import Cost [VSCode extension](packages/vscode-import-cost) - install it from [VSCode Marketplace](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost)
 * Import Cost [Node module](packages/import-cost) - use freely to implement extensions for other IDE (or contribute them to this repository)

Enjoy!

#### Third-Party Editor Plugin Links

* [Jetbrains IDE Plugin](https://github.com/denofevil/import-cost)
* [Atom Package](https://atom.io/packages/import-cost-atom)
* [Vim Plugin](https://github.com/wix/import-cost/tree/master/packages/coc-import-cost) ([coc.nvim](https://github.com/neoclide/coc.nvim) extension)
* [Vim Plugin](https://github.com/yardnsm/vim-import-cost)


## Why & How
We detail the why and how in this blog post:
https://citw.dev/posts/import-cost

## Developer guidelines

In this project we use [npm workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces) for managing the multiple packages.

### Getting started

In order to start working all you need to do is:
```sh
$ git clone git@github.com:wix/import-cost.git
$ npm install
$ code packages/import-cost
$ code packages/vscode-import-cost
```

Once VSCode workspaces are open:
* Hit `F5` to run tests in `import-cost`
* Hit `F5` to run the `vscode-import-cost` extension in debug mode

### Applying changes

Thanks to npm workspaces, we have a symbolic link in the `vscode-import-cost` node modules folder to the local `import-cost`, which makes applying changes very easy. You can verify that link exists by running the following command:

```sh
$ ls -la packages/vscode-import-cost/node_modules | grep import-cost
lrwxr-xr-x    1 shahar  staff    17 Aug  6 09:38 import-cost -> ../../import-cost
```

If anything goes wrong and link does not exist, just run the following commands at the root of this project and npm will sort it out:
```sh
$ git clean -xdf
$ npm install
```

After you make any changes to the `import-cost` node module, don't forget to trigger transpilation in order to see those changes when running the `vscode-import-cost` extension:
```sh
$ npm test
```

### Publishing changes

When you are ready to publish a new version of the extension, you first need to publish a new version of `import-cost` (unless nothing changed there). This is done by first commiting all your changes, then simply run the following commands:
```sh
$ cd packages/import-cost
$ npm version patch | minor | major
$ git commit -a -m "releasing version X.X.X"
$ git push
$ npm publish
```

Then go ahead and release the extension with almost same steps (except for last one):
```sh
$ cd packages/vscode-import-cost
$ npm version patch | minor | major
$ git commit -a -m "releasing version X.X.X"
$ git push
$ vsce publish
```

Don't forget to update README.md with details of what is new in the released version...
