## Literate programming

The markdown source for this tutorial is not only used to generate the website that you're viewing,
it's also used to create the JavaScript in the live demo. We use a small Python script for weaving
(generating HTML) and tangling (generating JS). This ensures that the tutorial is kept up to date
and that the code is highly readable.

## Start your project

This first tutorial shows how to render a spinning triangle with baked colors and no lighting. The
live demo is [here]().

First, create a directory for your web project and download `filament.js` and `filament.wasm` from
the [latest Filament release](https://github.com/google/filament/releases). In the future, these
files will be available on npm, which will allow you to use [yarn](https://yarnpkg.com/en/) or
[unpkg](https://unpkg.com).

Next, create a text file called `triangle.html` and fill it with the following HTML. This creates
a mobile-friendly page with a full-screen canvas.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Filament Tutorial</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,user-scalable=no,initial-scale=1">
    <style>
        body { margin: 0; } canvas { touch-action: none; width: 100%; height: 100%; }
    </style>
</head>
<body>
    <canvas></canvas>
    <script src="filament.js"></script>
    <script src="//unpkg.com/gl-matrix@2.8.1/dist/gl-matrix-min.js"></script>
    <script src="tutorial_triangle.js"></script>
</body>
</html>
```

The above HTML loads three JavaScript files:
- `filament.js` fetches and compiles the WebAssembly module
- `gl-matrix-min.js` is a small library that provides vector math functionality
- `tutorial_triangle.js` will contain your application code

Go ahead and create `tutorial_triangle.js` with the following content:

```js
class App {
  constructor() {
    /// Initialization
  }
  render() {
    /// Render
  }
  resize() {
    /// Resize
  }
}

Filament.init(['bakedColor.filamat'], () => { Window.app = new App() } );
```

The call to `Filament.init` does two things: it submits a list of asset URL's that can start
downloading immediately, and it provides a callback that gets executed as soon as all assets have
finished downloading and the Filament Engine can be instantiated.

<!-- If you have assets that can be downloaded later in the app's execution, you should not include
them in Filament.init since they will lengthen the loading process. -->

Download [bakedColor.filamat]() and place it in the same folder. We'll learn more about materials
and how to build them in the next tutorial.

## Spawn a local server

Because of CORS restrictions, your web app cannot fetch `bakedColor.filamat` directly from the
file system. One way to create a server is to use Python:

```bash
python3 -m http.server     # Python 3
python -m SimpleHTTPServer # Python 2.7
```

To see if this works, navigate to http://localhost:8000 and see if you can load the web page
without any errors in your browser's developer console.

## Flesh out the JavaScript

