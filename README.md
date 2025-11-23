[![][License img]][License]

<div>
    <a href="http://lpsc.in2p3.fr/" target="_blank">
        <img src="https://raw.githubusercontent.com/nyxlib/nyx-node/main/docs/img/logo_lpsc.svg" height="72"></a>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <a href="http://www.in2p3.fr/" target="_blank">
        <img src="https://raw.githubusercontent.com/nyxlib/nyx-node/main/docs/img/logo_in2p3.svg" height="72"></a>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <a href="http://www.univ-grenoble-alpes.fr/" target="_blank">
        <img src="https://raw.githubusercontent.com/nyxlib/nyx-node/main/docs/img/logo_uga.svg" height="72"></a>
</div>

# nyx-webpack-plugin

This is the repository of the [webpack](https://webpack.js.org/) plugin for developing [Nyx Lab](https://github.com/nyxlib/nyx-lab/) addons.

# Installing nyx-webpack-plugin

```bash
npm install --dev https://github.com/nyxlib/nyx-webpack-plugin.git
```

# Using nyx-webpack-plugin

In the poject root directory, create `webpack.config.js`:
```js
/*--------------------------------------------------------------------------------------------------------------------*/

const ADDON_NAME = 'addon-name';

/*--------------------------------------------------------------------------------------------------------------------*/

import {VueLoaderPlugin} from 'vue-loader';

/*--------------------------------------------------------------------------------------------------------------------*/

import NyxPlugin from 'nyx-webpack-plugin';

import TerserPlugin from 'terser-webpack-plugin';

/*--------------------------------------------------------------------------------------------------------------------*/

// noinspection JSUnusedGlobalSymbols
export default {
    mode: process.env.NODE_ENV === 'production' ? 'production' : 'development',
    entry: {
        'plugin': './src/plugin.js',
    },
    module: {
        rules: [
            {
                test: /\.vue$/,
                loader: 'vue-loader'
            },
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env']
                    }
                }
            },
            {
                test: /\.css$/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            },
            {
                'type': 'asset/resource',
                'test': /\.(ttf|png|jpg|wasm)$/,
                'generator': {
                    'filename': 'assets/[hash][ext]'
                }
            }
        ]
    },
    plugins: [
        new VueLoaderPlugin(),
        new NyxPlugin(ADDON_NAME),
    ],
    optimization: {
        minimize: true,
        minimizer: [
            new TerserPlugin({
                test: /\.js$/,
                parallel: true,
                extractComments: false,
            })
        ]
    },
    performance: {
        hints: false
    }
};

/*--------------------------------------------------------------------------------------------------------------------*/
```

# Home page and documentation

Home page:
* https://nyxlib.org/

Documentation:
* https://nyxlib.org/documentation/

# Developer

* [Jérôme ODIER](https://annuaire.in2p3.fr/4121-4467/jerome-odier) ([CNRS/LPSC](http://lpsc.in2p3.fr/))

# A bit of classical culture

In Greek mythology, Nyx is the goddess and personification of the night. She is one of the primordial deities, born from Chaos at the dawn of creation.

Mysterious and powerful, Nyx dwells in the deepest shadows of the cosmos, from where she gives birth to many other divine figures, including Hypnos (Sleep) and Thanatos (Death).

<div style="text-align: center;">
    <img src="https://raw.githubusercontent.com/nyxlib/nyx-node/refs/heads/main/docs/img/nyx.png" style="width: 600px;" />
</div>

[License]:https://www.gnu.org/licenses/lgpl-3.0.txt
[License img]:https://img.shields.io/badge/License-LGPL_3.0_or_later-blue.svg
