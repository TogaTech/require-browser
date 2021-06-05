# require-browser
Use node.js-style require and exports syntax in the browser

## Install
To use the require-browser tool in your front-end application, move the `require-browser.js` file into the root directory of your project and use the following script tag in all HTML files:
```html
<script type="text/javascript" src="/require-browser.js"></script>
```

## Documentation

### Paths
There are multiple different types of paths that can be used to require code.
 - Files: all file paths must include a `/` (easiest way to do this is to have the file path start with `/` or `./`) and end in `.js`.
 - Folders: `require-browser` will search for the folder with the name of the path if the file path is not a file (above conditions), if the file path contains a `/`, and if the file path does not contain `@`. `require-browser` will assume that you are requiring a file from the path specified.
 	 - By default, `index.js` in the folder will be used.
 	 - If `package.json` exists in the folder, the file in the `main` field will be used.
 	 - If the `browser` field exists in the `package.json`, whatever file was selected before will be mapped to the browser field's file if the mapping exists.
 - Node Modules: if none of the above conditions are met, `require-browser` will assume that you are requiring a node module and search in the default `node_modules` directory.
 	 - By default, `index.js` in the folder will be used.
 	 - If `package.json` exists in the folder, the file in the `main` field will be used.
 	 - If the `browser` field exists in the `package.json`, whatever file was selected before will be mapped to the browser field's file if the mapping exists.

### Installing Code
Due to the asynchronous nature of HTTP requests, all code that will be required must first be installed to the client. To install, use the following command:
```javascript
install(path, options);
```

If you would like to install multiple files, use the following command:
```javascript
installAll([path1, path2, path3], options);
```

#### Options
Options are an additional feature to change the configuration settings of the installation. If options are not included, the default settings are used.
 - `node_modules`: The path to the node_modules folder (default: `/node_modules/`)
 - `path`: a relative path to a certain file, best used with repetitive start paths in `installAll` (default: blank)
 - `reinstall`: reinstall a module in case it has already been installed (default: `false`)
 - `installDependencies`: install any modules listed in the `dependencies` portion of a `package.json` file (default: `true`)
 - `installDevDependencies`: install any modules listed in the `devDependencies` portion of a `package.json` file (default: `false`)
 - `name`: the name used to install that module later (default: path)

### Requiring Code
If you would like to require code, the code imported must use `module.exports`, `exports`, or browser code. If using `module.exports` or `exports`, write the following command:
```javascript
require(path_or_name);
```

If you use browser code or have the `browser` parameter in `package.json`, use the following command:
```javascript
requireBrowser(path_or_name);
```