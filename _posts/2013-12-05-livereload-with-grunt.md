---
title: Livereload with grunt
tags:
  - Node
description: >
    Instructions to configure Grunt to interact with a Livereload server.
---

## What you get

After changing your html, css and js files, you don't need to refresh your browser to see changes.

<div class="paper info">Your page will <strong>magically</strong> change, as you save your files!</div>

## Requirements

Create a *package.json*

```bash
$ cd /path/to/your/working/folder/
$ npm init
```

Install *grunt-cli* globally (only once).

```bash
$ npm uninstall -g grunt-cli
$ npm install -g grunt-cli
```

Install *grunt* and other packages

```bash
$ npm install --save-dev grunt
$ npm install --save-dev grunt-contrib-connect
$ npm install --save-dev grunt-contrib-watch
$ npm install --save-dev grunt-open
```

## Configuration

I suppose there is at least an *index.html* and some JavaScript file under *js/* folder.
I like to use [coffee-script][3] to edit configuration, i.e. I use a *Gruntfile.coffee*

Here it is a working configuration

```coffee
livereloadPort = 35729

module.exports = (grunt) ->
  grunt.initConfig
    watch:
      index:
        files: ['index.html']
        tasks: []
        options:
          livereload: livereloadPort
      js:
        files: ['js/*.js']
        tasks: []
        options:
          livereload: livereloadPort
    connect:
      server:
        options:
          port: 3000
          livereload: livereloadPort
    open:
      index:
        path: 'http://localhost:3000'
        app: 'chrome'

  grunt.loadNpmTasks 'grunt-contrib-connect'
  grunt.loadNpmTasks 'grunt-contrib-watch'
  grunt.loadNpmTasks 'grunt-open'

  grunt.registerTask 'default', ['connect', 'open', 'watch']
```

Now, if you launch

```bash
grunt
```

<div class="paper success">Your browser will open, and the window will change <strong>as soon as</strong> you modify your files.</div>


[1]: http://gruntjs.com/
[2]: http://livereload.com/
[3]: http://coffeescript.org/

