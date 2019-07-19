# You do not (may not) need Gulp

How to manage your workflow in shell without task runner (gulp, grunt, fly, just, etc.)

## Table of Contents

-   [Articles](#articles)

-   [Recipes](#recipes)

    -   [Delete files and folders](#delete-files-and-folders)
    -   [ESLint](#eslint)
    -   [ESLint in watch mode](#eslint-in-watch-mode)
    -   [Parallel](#parallel)
    -   [Compile TypeScript](#compile-typescript)
    -   [Copy files](#copy-files)

## Articles

-   [Why I Left Gulp and Grunt for npm Scripts](https://medium.com/free-code-camp/why-i-left-gulp-and-grunt-for-npm-scripts-3d6853dd22b8)
-   [How to Use npm as a Build Tool](https://webcache.googleusercontent.com/search?q=cache:http://blog.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/)
-   [Build Automation with Vanilla JavaScript](https://medium.com/@tarkus/build-automation-with-vanilla-javascript-74639ec98bad)
-   [Why we should stop using Grunt & Gulp](https://webcache.googleusercontent.com/search?q=cache:https://www.keithcirkel.co.uk/why-we-should-stop-using-grunt/)

## Recipes

### Delete files and folders

**Gulp**

```js
const del = require('del');

gulp.task('clean', () => {
  return del(['dist/report.csv', 'dist/mobile/**/*']);
});
```

**npm del-cli**

```sh
del "dist/report.csv" "dist/mobile/**/*"
```

**Shell**

```sh
rm -rf "dist/report.csv" "dist/mobile"
```

### ESLint

**Gulp**

```js
gulp.task('eslint', () => {
    return gulp.src('src/**/*.ts')
        .pipe(g.eslint())
        .pipe(g.eslint.format());
});
```

**npm eslint**

```sh
eslint src --ext ts
```

### ESLint in watch mode

**Gulp**

```js
gulp.task('eslint:watch', (done) => {
    const w = gulp.watch('src/**/*.ts', { ignoreInitial: false }, gulp.series('eslint'));
    process.on('SIGINT', () => {
        w.close();
        done();
    });
});
```

**npm watchexec-bin**

```sh
watchexec -w src "npm run eslint"
```

### Parallel

### Compile TypeScript

### Copy files

<!--
## Watch

Gulp
```js
const watcher = gulp.watch(['input/*.js']);

watcher.on('change', function(path, stats) {
  console.log(`File ${path} was changed`);
});

watcher.on('add', function(path, stats) {
  console.log(`File ${path} was added`);
});

watcher.on('unlink', function(path, stats) {
  console.log(`File ${path} was removed`);
});

watcher.close();
```
-->
