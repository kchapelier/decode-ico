# Decode ICO

Decode `.ico` icons

## Installation

```sh
npm install --save decode-ico
```

## Usage

```js
const decodeIco = require('decode-ico')
const fs = require('fs')

const source = fs.readFileSync('favicon.ico')
const images = decodeIco(source)

console.log(images[0])
//=> { width: 16, height: 16, type: 'bmp', data: Buffer(...) }

console.log(images[1])
//=> { width: 32, height: 32, type: 'bmp', data: Buffer(...) }
```

## API

### `decodeIco(source: Buffer) => Image[]`

Decodes the `.ico` file in the given buffer, and returns an array of images.

Each image has the following properties:

- `width: Number` - The width of the image, in pixels
- `height: Number` - The height of the image, in pixels
- `type: String` - The type of image, will be one of `bmp` or `png`
- `data: Buffer` - The data of the image, format depends on `type`, see below

The format of the `data` parameter depends on the type of image. When the image is of type `bmp`, the `data` buffer will hold raw pixel data in the RGBA order, with integer values between 0 and 255 (included). When the type is `png`, the buffer will be png data.

💡 The `png` data can be written to a file with the `.png` extension directly, or be decoded by [node-lodepng](https://github.com/LinusU/node-lodepng) which will give you the same raw format as the `bmp` type.