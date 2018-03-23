# view-binary-element
Native Web Component for previewing a few common types of binary files

Disclaimer: Work in Progress, and not tested in production. Feedback welcome though.

Check https://caniuse.com/ to verify how well Web Components is covered by current browsers. This component uses Custom Elements v1, (optionally) HTML Imports, HTML Templates, Shadow DOM v1 (gracefull decay would be possible).

## Installation

Simplest way:

    <link rel="import" href="https://cdn.rawgit.com/grtjn/view-binary-element/master/view-binary.html">

Likely together with this polyfill:

    <script src="https://cdn.rawgit.com/webcomponents/webcomponentsjs/master/webcomponents-hi.js" type="text/javascript" defer></script>

Alternatively, 'require'/include it with a tool like Webpack:

    <%= require('html-loader!https://cdn.rawgit.com/grtjn/view-binary-element/master/view-binary.html') %>

## Usage

Static example:

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

Embedding in Vue.js:

- Import or include the web component in your index.html
- Add `view-binary` to ignoreElements to stop it from squeaking:

        Vue.config.ignoredElements = ["view-binary"];

- Use it in any component:

        <view-binary :src="viewUri" :type="contentType" :title="fileName">
          <a slot="fallback" class="btn btn-default" :href="downloadUri" target="_blank" download>Download {{ fileName }}</a>
        </view-binary>

## Test locally

- Uncomment the local import line in docs/index.html
- Run something like `python -m SimpleHTTPServer 8888` from project root
- Open http://localhost:8888/docs/

