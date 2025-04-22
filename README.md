```
// Block and sidebar block Attributes ! block.json ! 

...
"attributes": {
    "name": {
        "type": "string",
        "default": ""
      },
      "age": {
        "type": "number",
        "default": 0
      }
},
...

```

# WPBlockExtendDevelopment
WordPress Custom Block Gutenberg Builder 

```

npx @wordpress/create-block my-block

```

```

cd my-block

my-block/
    │
    ├── src/                # Your block source code (JS/JSX, CSS, etc.)
    ├── build/              # Compiled output
    ├── plugin.php          # Main plugin file
    ├── package.json        # NPM config
    ├── block.json          # Block metadata


```

```

// To compile your JavaScript and watch for changes:

npm start

```

```
// For production build:

npm run build

```


Open ``` src/edit.js ``` and  ``` src/save.js ``` to define how your block works.

Example: Simple Hello World Block
``` src/edit.js ```

```JS

import { __ } from '@wordpress/i18n';
import { useBlockProps } from '@wordpress/block-editor';

export default function Edit() {
    return (
        <div { ...useBlockProps() }>
            <p>Hello from the editor!</p>
        </div>
    );
}

````

```

src/save.js

```

```JS

import { useBlockProps } from '@wordpress/block-editor';

export default function save() {
    return (
        <div { ...useBlockProps.save() }>
            <p>Hello from the frontend!</p>
        </div>
    );
}

```


Make sure plugin.php is loading your block correctly.

```PHP

<?php
/**
 * Plugin Name:       My Custom Block
 */

function my_custom_block_init() {
    register_block_type( __DIR__ . '/build' );
}
add_action( 'init', 'my_custom_block_init' );

```


```

Done: WordPress plugin Myblocks bootstrapped in the /Users/apple/plugs/wp-content/plugins/myblocks directory.

You can run several commands inside:

  $ npm start
    Starts the build for development.

  $ npm run build
    Builds the code for production.

  $ npm run format
    Formats files.

  $ npm run lint:css
    Lints CSS files.

  $ npm run lint:js
    Lints JavaScript files.

  $ npm run plugin-zip
    Creates a zip file for a WordPress plugin.

  $ npm run packages-update
    Updates WordPress packages to the latest version.

To enter the directory type:

  $ cd myblocks

You can start development with:

  $ npm start

```



Passing the value from block inpur into PHP render file 

```

npm install @wordpress/server-side-render --save

```

Helpful link: 

WP Theme Block Development : https://github.com/nielsoffice-Pro/WPTHEME-REACTBLOCK
