# Intro to Gulp

[Gulp](http://gulpjs.com/) is a task runner, used for automating your workflow. *It's like a Makefile on steroids*!

What can you automate? Anything receptive, like -

1. Minification
1. Compilation
1. Testing
1. Linting

Install globally:

```sh
$ npm install --g gulp
```

## Setup

### Install

1. Create a new project using the Galvanize HTML generator
1. Install Gulp as a dev dependency - `npm install gulp --save-dev`

### gulpfile.js

Add *gulpfile.js* file to the project root, and then add the boilerplate code:

```javascript
var gulp = require('gulp');

gulp.task('default', function() {
  // place code for your default task here
});
```

This sets up the default task, which can be run with `gulp default` or `gulp`. Try it!

Now we need to add additional tasks, using the [Gulp plugin system](http://gulpjs.com/plugins/).

## Plugins

Plugins are meant to perform a single job:

1. `gulp.task` - defines tasks
1. `gulp.src` - defines the files we want to use to perfrom some task
1. `gulp.dest` - defines the output folder that files are written to after performing a task
1. `gulp.watch` - is used for monitoring files and folders (usually for changes)

> Refer to the [API docs](https://github.com/gulpjs/gulp/blob/master/docs/API.md) for more info on these methods.

For example, you could set up a minification task (`gulp.task`) on all JavaScript files found within the "src/js" folder (`gulp.src`). After the task runs, the files then could be saved to a build folder, like "build/js" (`gulp.dest`). Finally, you could watch (`gulp.watch`) for any chances to the *.js* files found within "src/js", so that when a change occurs to one of the files the minification task (`gulp.task`) is ran.

## Tasks

So, which tasks should you run?

### Linting

**gulp-jshint** - `npm install --save-dev gulp-jshint jshint-stylish`

```javascript
var gulp = require('gulp');
var jshint = require('gulp-jshint');

// configure jshint task
gulp.task('jshint', function() {
  return gulp.src('src/javascripts/**/*.js') // update path!
    .pipe(jshint())
    .pipe(jshint.reporter('jshint-stylish'));
});

// configure which files to watch and what tasks to use on file changes
gulp.task('watch', function() {
  gulp.watch('source/javascript/**/*.js', ['jshint']); // update path!
});

// default task!
gulp.task('default', ['watch']);
```

### Running a Server

**gulp-server-livereload** - `npm install --save-dev gulp-server-livereload`

```javascript
var gulp = require('gulp');
var jshint = require('gulp-jshint');
var server = require('gulp-server-livereload');

// configure webserver task
gulp.task('webserver', function() {
  gulp.src('app')
    .pipe(server({
      livereload: true,
      directoryListing: true,
      open: true
    }));
});

// configure jshint task
gulp.task('jshint', function() {
  return gulp.src('src/javascripts/**/*.js') // update path!
    .pipe(jshint())
    .pipe(jshint.reporter('jshint-stylish'));
});

// configure which files to watch and what tasks to use on file changes
gulp.task('watch', function() {
  gulp.watch('source/javascript/**/*.js', ['jshint']); // update path!
});

// default task!
gulp.task('default', ['watch', 'webserver']);
```

### Other Plugins

https://github.com/mjhea0/angular-gulp-browserify-seed/blob/master/gulpfile.js

