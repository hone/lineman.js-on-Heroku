# Lineman.js on the Heroku Static Buildpack

## Setup
* Create a new lineman.js app
```sh
$ lineman new foo
$ cd foo
$ git init
$ git add .
$ git commit -m "initial commit"
```
* Add a npm postinstall task to `package.json`
```js
  "scripts": {
    "postinstall": "lineman build"
  }
```
```sh
$ git add package.json
$ git commit -m "build assets during build"
```
* Add a `static.json`
```js
{
  "root": "dist"
}
```
```sh
$ git add static.json
$ git commit -m "configuration for the static buildpack"
```
* Create a new heroku app
```sh
$ heroku create
```
* Setup the node.js buildpack to build the assets and the static buildpack to serve assets
```sh
$ heroku buildpacks:add https://github.com/heroku/heroku-buildpack-nodejs
$ heroku buildpacks:add https://github.com/hone/heroku-buildpack-static
```
* Tell the node.js buildpack to use dev dependencies
```sh
$ heroku config:set NPM_CONFIG_PRODUCTION=false
```
* Deploy the heroku app
```sh
$ git push heroku master
Counting objects: 44, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (33/33), done.
Writing objects: 100% (44/44), 27.67 KiB | 0 bytes/s, done.
Total 44 (delta 3), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> Multipack app detected
remote: -----> Fetching custom git buildpack... done
remote: -----> Node.js app detected
remote:
remote: -----> Creating runtime environment
remote:
remote:        NPM_CONFIG_LOGLEVEL=error
remote:        NPM_CONFIG_PRODUCTION=false
remote:        NODE_ENV=production
remote:        NODE_MODULES_CACHE=true
remote:
remote: -----> Installing binaries
remote:        engines.node (package.json):  unspecified
remote:        engines.npm (package.json):   unspecified (use default)
remote:
remote:        Resolving node version (latest stable) via semver.io...
remote:        Downloading and installing node 0.12.7...
remote:        Using default npm version: 2.11.3
remote:
remote: -----> Restoring cache
remote:        Skipping cache (new runtime signature)
remote:
remote: -----> Building dependencies
remote:        Pruning any extraneous modules
remote:        Installing node modules (package.json)
remote:
remote:        > js2coffee@0.3.3 preinstall /tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/js2coffee
remote:        > node ./cyclic.js
remote:
remote:
remote:        > utf-8-validate@1.1.0 install /tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/engine.io/node_modules/ws/node_modules/utf-8-validate
remote:        > node-gyp rebuild
remote:
remote:        make: Entering directory `/tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/engine.io/node_modules/ws/node_modules/utf-8-validate/build'
remote:          CXX(target) Release/obj.target/validation/src/validation.o
remote:          SOLINK_MODULE(target) Release/obj.target/validation.node
remote:          COPY Release/validation.node
remote:        make: Leaving directory `/tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/engine.io/node_modules/ws/node_modules/utf-8-validate/build'
remote:
remote:        > bufferutil@1.1.0 install /tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/engine.io/node_modules/ws/node_modules/bufferutil
remote:        > node-gyp rebuild
remote:
remote:        make: Entering directory `/tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/engine.io/node_modules/ws/node_modules/bufferutil/build'
remote:          CXX(target) Release/obj.target/bufferutil/src/bufferutil.o
remote:          SOLINK_MODULE(target) Release/obj.target/bufferutil.node
remote:          COPY Release/bufferutil.node
remote:        make: Leaving directory `/tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/engine.io/node_modules/ws/node_modules/bufferutil/build'
remote:
remote:        > utf-8-validate@1.1.0 install /tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/socket.io-client/node_modules/engine.io-client/node_modules/ws/node_modules/utf-8-validate
remote:        > node-gyp rebuild
remote:
remote:        make: Entering directory `/tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/socket.io-client/node_modules/engine.io-client/node_modules/ws/node_modules/utf-8-validate/build'
remote:          CXX(target) Release/obj.target/validation/src/validation.o
remote:          SOLINK_MODULE(target) Release/obj.target/validation.node
remote:          COPY Release/validation.node
remote:        make: Leaving directory `/tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/socket.io-client/node_modules/engine.io-client/node_modules/ws/node_modules/utf-8-validate/build'
remote:
remote:        > bufferutil@1.1.0 install /tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/socket.io-client/node_modules/engine.io-client/node_modules/ws/node_modules/bufferutil
remote:        > node-gyp rebuild
remote:
remote:        make: Entering directory `/tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/socket.io-client/node_modules/engine.io-client/node_modules/ws/node_modules/bufferutil/build'
remote:          CXX(target) Release/obj.target/bufferutil/src/bufferutil.o
remote:          SOLINK_MODULE(target) Release/obj.target/bufferutil.node
remote:          COPY Release/bufferutil.node
remote:        make: Leaving directory `/tmp/build_47481f0eba4a638e337ea80b7cf7970b/node_modules/lineman/node_modules/testem/node_modules/socket.io/node_modules/socket.io-client/node_modules/engine.io-client/node_modules/ws/node_modules/bufferutil/build'
remote:
remote:        > lineman-heroku@0.0.1 postinstall /tmp/build_47481f0eba4a638e337ea80b7cf7970b
remote:        > lineman build
remote:
remote:        Running "clean:dist" (clean) task
remote:
remote:        Running "common" task
remote:
remote:        Running "coffee:compile" (coffee) task
remote:        >> Destination (generated/js/app.coffee.js) not written because compiled files were empty.
remote:        >> Destination (generated/js/spec.coffee.js) not written because compiled files were empty.
remote:        >> Destination (generated/js/spec-helpers.coffee.js) not written because compiled files were empty.
remote:
remote:        Running "jshint:files" (jshint) task
remote:        >> 1 file lint free.
remote:
remote:        Running "handlebars:compile" (handlebars) task
remote:        >> Destination not written because compiled files were empty.
remote:        >> 0 files created.
remote:
remote:        Running "jst:compile" (jst) task
remote:        File "generated/template/underscore.js" created.
remote:
remote:        Running "concat_sourcemap:js" (concat_sourcemap) task
remote:        File "generated/js/app.js" created.
remote:
remote:        Running "concat_sourcemap:spec" (concat_sourcemap) task
remote:        File "generated/js/spec.js" created.
remote:
remote:        Running "concat_sourcemap:css" (concat_sourcemap) task
remote:        File "generated/css/app.css" created.
remote:
remote:        Running "copy:dev" (copy) task
remote:        Created 2 directories, copied 1 files
remote:
remote:        Running "images:dev" (images) task
remote:        Copying images to 'generated/img'
remote:
remote:        Running "webfonts:dev" (webfonts) task
remote:        Copying webfonts to 'generated/webfonts'
remote:
remote:        Running "pages:dev" (pages) task
remote:        generated/index.html generated from app/pages/index.us
remote:
remote:        Running "dist" task
remote:
remote:        Running "uglify:js" (uglify) task
remote:        File "dist/js/app.js" created.
remote:
remote:        Running "cssmin:compress" (cssmin) task
remote:        File dist/css/app.css created.
remote:
remote:        Running "copy:dist" (copy) task
remote:        Created 2 directories, copied 1 files
remote:
remote:        Running "images:dist" (images) task
remote:        Copying images to 'dist/img'
remote:
remote:        Running "webfonts:dist" (webfonts) task
remote:        Copying webfonts to 'dist/webfonts'
remote:
remote:        Running "pages:dist" (pages) task
remote:        dist/index.html generated from app/pages/index.us
remote:
remote:        Done, without errors.
remote:        lineman@0.36.4 node_modules/lineman
remote:        ├── connect-livereload@0.4.1
remote:        ├── config-extend@0.0.6
remote:        ├── grunt-contrib-copy@0.4.1
remote:        ├── commander@1.3.2 (keypress@0.1.0)
remote:        ├── grunt-contrib-sass@0.5.0 (dargs@0.1.0)
remote:        ├── semver@2.1.0
remote:        ├── grunt-contrib-coffee@0.7.0
remote:        ├── grunt-contrib-clean@0.5.0 (rimraf@2.2.8)
remote:        ├── resolve@0.6.3
remote:        ├── normalize-package-data@0.2.13 (github-url-from-git@1.1.1, github-url-from-username-repo@0.1.0)
remote:        ├── lodash@0.9.2
remote:        ├── grunt-contrib-cssmin@0.6.1 (clean-css@1.0.12, grunt-lib-contrib@0.6.1)
remote:        ├── watch_r-structr-lock@0.0.1 (structr@0.2.3, async@0.2.10, commander@1.1.1, underscore@1.4.4, tq@0.2.5, ejs@0.8.8)
remote:        ├── coffee-script@1.6.3
remote:        ├── underscore.string@2.3.3
remote:        ├── grunt-concat-sourcemap@0.4.3 (source-map@0.1.31)
remote:        ├── grunt-contrib-jst@0.5.1 (grunt-lib-contrib@0.5.3, lodash@1.0.2)
remote:        ├── grunt-watch-nospawn@0.0.8 (tiny-lr-fork@0.0.5, gaze@0.3.3)
remote:        ├── js2coffee@0.3.3 (file@0.2.2, underscore@1.6.0, nopt@3.0.4, coffee-script@1.7.1)
remote:        ├── http-proxy@0.10.3 (colors@0.6.2, pkginfo@0.2.3, optimist@0.3.7, utile@0.1.7)
remote:        ├── grunt-asset-fingerprint@0.2.1 (lodash@2.4.2)
remote:        ├── grunt-contrib-uglify@0.2.4 (grunt-lib-contrib@0.6.1, uglify-js@2.4.24)
remote:        ├── grunt@0.4.5 (dateformat@1.0.2-1.2.3, which@1.0.9, getobject@0.1.0, eventemitter2@0.4.14, rimraf@2.2.8, colors@0.6.2, hooker@0.2.3, async@0.1.22, grunt-legacy-util@0.2.0, exit@0.1.2, nopt@1.0.10, minimatch@0.2.14, glob@3.1.21, coffee-script@1.3.3, underscore.string@2.2.1, iconv-lite@0.2.11, findup-sync@0.1.3, grunt-legacy-log@0.1.2, js-yaml@2.0.5)
remote:        ├── grunt-contrib-handlebars@0.8.0 (grunt-lib-contrib@0.5.3, chalk@0.4.0, handlebars@1.3.0)
remote:        ├── fetcher@0.2.0 (async@0.9.2, underscore@1.8.3, which@1.1.2, mkdirp@0.5.1, cpr@0.2.0, coffee-script@1.10.0, rimraf@2.4.3, decompress@0.2.5, request@2.62.0, cson-safe@0.1.1)
remote:        ├── grunt-contrib-jshint@0.11.0 (hooker@0.2.3, jshint@2.6.3)
remote:        ├── express@3.4.0 (methods@0.0.1, range-parser@0.0.4, cookie-signature@1.0.1, fresh@0.2.0, buffer-crc32@0.2.1, cookie@0.1.0, mkdirp@0.3.5, commander@1.2.0, debug@2.2.0, send@0.1.4, connect@2.9.0)
remote:        └── testem@0.7.6 (xml-escape@1.0.0, styled_string@0.0.1, did_it_work@0.0.6, growl@1.8.1, consolidate@0.11.0, charm@1.0.0, colors@1.1.2, async@0.9.2, commander@2.8.1, mustache@1.2.0, cross-spawn@0.2.9, http-proxy@1.11.2, mkdirp@0.5.1, backbone@1.2.3, glob@4.5.3, rimraf@2.4.3, npmlog@1.2.1, fileset@0.1.8, express@4.13.3, fireworm@0.6.6, tap@0.6.0, js-yaml@3.4.2, socket.io@1.3.6)
remote:
remote: -----> Caching build
remote:        Clearing previous node cache
remote:        Saving 1 cacheDirectories (default):
remote:        - node_modules
remote:
remote: -----> Build succeeded!
remote:        └── lineman@0.36.4
remote:
remote: -----> Fetching custom git buildpack... done
remote: -----> Static HTML app detected
remote:   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
remote:                                  Dload  Upload   Total   Spent    Left  Speed
remote: 100  795k  100  795k    0     0  5481k      0 --:--:-- --:--:-- --:--:-- 5522k
remote: -----> Installed directory to /app/bin
remote:
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote:
remote: -----> Compressing... done, 23.7MB
remote: -----> Launching... done, v4
remote:        https://vast-river-2155.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy.... done.
To https://git.heroku.com/vast-river-2155.git
 * [new branch]      master -> master
```
