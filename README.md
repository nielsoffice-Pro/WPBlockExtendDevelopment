References: https://developer.wordpress.org/block-editor/reference-guides/block-api/block-attributes/
<br>Meta: https://developer.wordpress.org/block-editor/reference-guides/block-api/block-metadata/
<br> Support: https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/
<br> Related: https://developer.wordpress.org/block-editor/reference-guides/packages/packages-block-editor/

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

```
// Support

"supports": {
  "align": true,
  "alignWide": true,
  "anchor": true,
  "customClassName": true,
  "html": false,
  "reusable": true,
  "multiple": true,
  "lock": false,
  "renaming": true,
  "position": { "sticky": true },
  "color": { "text": true, "background": true, "link": true },
  "spacing": { "padding": true, "margin": true },
  "typography": { "fontSize": true, "lineHeight": true },
  "border": true,
  "dimensions": true
}

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

-----------------------------------------------------------------------------------------

<br>If You Want to Create Another Block…
<br>No, you don’t need to create another plugin just to create another block. In fact, it’s best practice to include multiple blocks in one plugin, especially if they’re related.
<br>
<br>Instead of creating another plugin, you can simply add another folder + ``` block.json ``` file in the same plugin, like this:
<br>

```

my-block-plugin/
├── build/
├── src/
│   ├── block-one/
│   │   ├── block.json
│   │   ├── edit.js
│   │   ├── save.js
│   ├── block-two/
│   │   ├── block.json
│   │   ├── edit.js
│   │   ├── save.js
├── plugin.php

```

How to Register Multiple Blocks in One Plugin
If you’re using the @wordpress/scripts setup (create-block), you can tweak ``` index.js ``` like this:

```

import './block-one';
import './block-two';

```


In Your plugin.php
<br>No changes needed if you're using block.json + register_block_type_from_metadata(). It will pick up each block automatically when included.

```PHP

function my_block_plugin_register_blocks() {
    register_block_type( __DIR__ . '/build/block-one' );
    register_block_type( __DIR__ . '/build/block-two' );
}
add_action( 'init', 'my_block_plugin_register_blocks' );


```

```PHP
// If you have lots of blocks, loop through them:

$blocks = [ 'block-one', 'block-two', 'block-three' ];

foreach ( $blocks as $block ) {
    register_block_type( __DIR__ . "/build/$block" );
}

```

-----------------------------------------------------------------------------------------

Helpful link: 

WP Theme Block Development : https://github.com/nielsoffice-Pro/WPTHEME-REACTBLOCK
<br> https://developer.wordpress.org/block-editor/reference-guides/core-blocks/
<br> Block Editor: https://developer.wordpress.org/block-editor/
