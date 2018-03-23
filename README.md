# view-binary-element
Native Web Component for previewing a few common types of binary files

Disclaimer: Work in Progress, and not tested in production. Feedback welcome though.

Check https://caniuse.com/ to verify how well Web Components is covered by current browsers. This component uses Custom Elements v1, (optionally) HTML Imports, HTML Templates, Shadow DOM v1 (gracefull decay would be possible).

## Usage

Simplest way:

    <link rel="import" href="https://cdn.rawgit.com/grtjn/view-binary-element/master/view-binary.html">

Likely together with this polyfill:

    <script src="https://cdn.rawgit.com/webcomponents/webcomponentsjs/master/webcomponents-hi.js" type="text/javascript" defer></script>

Alternatively, 'require'/include it with a tool like Webpack:

    <%= require('html-loader!https://cdn.rawgit.com/grtjn/view-binary-element/master/view-binary.html') %>

## Test locally

- Uncomment the local import line in docs/index.html
- Run something like `python -m SimpleHTTPServer 8888` from project root
- Open http://localhost:8888/docs/

