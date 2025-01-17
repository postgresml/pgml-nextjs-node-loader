# pgml-nextjs-node-loader

This is a fork of: https://github.com/eisberg-labs/nextjs-node-loader

This is a custom loader for Webpack that allows you to include native Node.js `.node` modules in your Next.js project.
It simplifies the process of loading native modules by providing a standardized interface that works seamlessly with
Next.js.

## Getting Started

To begin, you'll need to install a `nextjs-node-loader`:

```console
npm install nextjs-node-loader --save-dev
```

**next.config.js**

```js
module.exports = {
  webpack: (config, { dev, isServer, webpack, nextRuntime }) => {
    config.module.rules.push({
      test: /\.node$/,
      use: [
        {
          loader: "nextjs-node-loader",
          options: {
            flags: os.constants.dlopen.RTLD_NOW,
            outputPath: config.output.path,
          },
        },
      ],
    });
    return config;
  },
};
```

And use in e.g. your api route;

```javascript
import module from "node-module";

export default function handler(req, res) {
  // ...
}
```

## Options

|    Name    |    Type    |       Default        | Description                                           |
| :--------: | :--------: | :------------------: | :---------------------------------------------------- |
|   flags    | `{Number}` |     `undefined`      | Enables/Disables `url`/`image-set` functions handling |
| outputPath | `{String}` | webpack's outputPath | The root path of shared node libraries                |

## License

[MIT](./LICENSE)
