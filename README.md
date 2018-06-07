# view-binary-element
Native Web Component for previewing a few common types of binary files

This is essentially a refactored version of https://github.com/grtjn/view-file-ng to eliminate AngularJS. Not yet as feature rich though.

Disclaimer: Work in Progress, and not tested in production. Feedback welcome though.

Check https://caniuse.com/ to verify how well Web Components is covered by current browsers. This component uses Custom Elements v1, (optionally) HTML Imports, HTML Templates, Shadow DOM v1 (gracefull decay would be possible).

## Installation

### CDN and polyfill

Simplest way:

    <link rel="import" href="https://cdn.rawgit.com/grtjn/view-binary-element/master/view-binary.html">

Likely together with this polyfill:

    <script src="https://cdn.rawgit.com/webcomponents/webcomponentsjs/v1.2.0/webcomponents-hi.js" type="text/javascript" defer></script>


### NPM and html-loader

This component is also published on npm:

    npm install --save view-binary-element

Potentially combined with something like:

    <%= require('html-loader!../node_modules/view-binary-element/view-binary.html') %>

### Bower, wiredep, and gulp

This component is also published on bower:

    bower install --save view-binary-element

You can combine that with gulp and wiredep with something like:

    .pipe(gulpWiredep({
      fileTypes: {
        html: {
          block: /(([ \t]*)<!--\s*bower:*(\S*)\s*-->)(\n|\r|.)*?(<!--\s*endbower\s*-->)/gi,
          detect: {
            js: /<script.*src=['"]([^'"]+)/gi,
            css: /<link.*href=['"]([^'"]+)/gi,
            html: /<link.*href=['"]([^'"]+)/gi
          },
          replace: {
            js: '<script src="{{filePath}}"></script>',
            css: '<link rel="stylesheet" href="{{filePath}}">',
            html: '<link rel="import" href="{{filePath}}">'
          }
        }
      }
    }))

Add this to your index.html:

    <!-- bower:html -->
    <link rel="import" href="/bower_components/view-binary-element/view-binary.html">
    <!-- endbower -->

    <!-- @exclude -->
    <script src="https://cdn.rawgit.com/webcomponents/webcomponentsjs/v1.2.0/webcomponents-hi.js" type="text/javascript" defer></script>
    <!-- @endexclude -->

This relies on the html-import polyfill loaded from CDN. If you prefer not to rely on that, or if your tooling builds minified versions of everything, you can include the html similarly to html-loader mentioned above in NPM, and strip off the polyfill using gulp-preprocessor roughly like this:

    .pipe(gulpReplace(/<link rel="import" href="([^"]+)">/g, '<!-- @include ../$1 -->'))
    .pipe(gulpPreprocess())

## Usage

Example:

    <view-binary class="audio" src="data/sample-music.mp3" type="audio/mpeg" title="sample-music.mp3">
      <a slot="fallback" href="data/sample-music.mp3" target="_blank" download>Download sample-music.mp3</a>
    </view-binary>

Does not emit events.

### Plaing HTML and JavaScript

- Assumes CDN and polyfill installation
- In your html:

        <style>
        view-binary {
          display: block;
          height: 300px;
        }
        view-binary.audio {
          height: 32px;
        }
        </style>
    
        <view-binary class="audio" src="data/sample-music.mp3" type="audio/mpeg" title="sample-music.mp3">
          <a slot="fallback" href="data/sample-music.mp3" target="_blank" download>Download sample-music.mp3</a>
        </view-binary>

### Vue.js

- Import or include the web component in your index.html (see for instance NPM and html-loader installation)
- Add `view-binary` to ignoreElements to stop it from squeaking:

        Vue.config.ignoredElements = ["view-binary"];

- Use it in any component:

        <view-binary :src="viewUri" :type="contentType" :title="fileName">
          <a slot="fallback" class="btn btn-default" :href="downloadUri" target="_blank" download>Download {{ fileName }}</a>
        </view-binary>

### AngularJS

- Assumes Bower, wiredep, and gulp installation
- In your html template:

        <view-binary src="{{viewUri}}" type="{{contentType}}" title="{{fileName}}">
          <a slot="fallback" class="btn btn-default" href="{{downloadUri}}" target="_blank" download>Download {{ fileName }}</a>
        </view-binary>

## Test locally

- Uncomment the local import line in docs/index.html
- Run something like `python -m SimpleHTTPServer 8888` from project root
- Open http://localhost:8888/docs/

