# You do not (may not) need task runner

How to manage your workflow in shell without task runner (gulp, grunt, fly, just, etc.)

## Table of Contents

-   [Resources](#resources)

-   [Recipes](#recipes)

    -   [Delete files and folders](#delete-files-and-folders)
    -   [ESLint](#eslint)
    -   [ESLint in watch mode](#eslint-in-watch-mode)
    -   [Parallel Tasks](#parallel-tasks)
    -   [Compile TypeScript](#compile-typescript)
    -   [Copy files](#copy-files)

## Resources

-   [Everything awesome related to npm scripts and using npm as a build tool](https://github.com/RyanZim/awesome-npm-scripts)
-   [Why I Left Gulp and Grunt for npm Scripts](https://medium.com/free-code-camp/why-i-left-gulp-and-grunt-for-npm-scripts-3d6853dd22b8) - Article by Cory House
-   [Build Automation with Vanilla JavaScript](https://medium.com/@tarkus/build-automation-with-vanilla-javascript-74639ec98bad)
-   [How to Use npm as a Build Tool](https://www.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/) - Blog post by Keith Cirkel
-   [Why we should stop using Grunt & Gulp](https://www.keithcirkel.co.uk/why-we-should-stop-using-grunt/)
-   [Helpers and tips for npm run scripts](https://michael-kuehnel.de/tooling/2018/03/22/helpers-and-tips-for-npm-run-scripts.html) - Blog post by Michael Kühnel covering advanced topics
-   [Advanced front-end automation with npm scripts](https://www.youtube.com/watch?v=0RYETb9YVrk) - Talk at Nordic.js 2015 by Kate Hudson
-   [How to create a build system with npm scripts](http://www.penta-code.com/how-to-create-a-build-system-with-npm-scripts/) - Video tutorial series on setting up a front-end build system
-   [Ecosystem-free task runner that goes well with npm scripts](https://github.com/scriptype/salinger)

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

**npm rimraf**

```sh
rimraf dist
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
    const w = gulp.watch('src/**/*.ts', gulp.series('eslint'));
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

**Taskfile/Shell**

```sh
# Taskfile
eslint_watch() {
    while true; do
        inotifywait -r src && "npm run eslint"
    done
}
"$@"
```

```sh
sh Taskfile eslint_watch
```

### Parallel Tasks

**Gulp**

```js
gulp.task('dev:watch', gulp.parallel('test:watch', 'eslint:watch');
```

**npm run-p**

```sh
run-p test:watch eslint:watch
```

**npm concurrently**

```sh
concurrently "npm run test:watch" "npm run eslint:watch"
```

**Taskfile/Shell**

```sh
# Taskfile
dev_watch() {
    npm run test:watch 2>&1 &
    npm run eslint:watch 2>&1 &
}
"$@"
```

```sh
sh Taskfile dev_watch
```

### Compile TypeScript

**Gulp**

```js
gulp.task('scripts', () => {
    return gulp.src('src/**/*.ts')
        .pipe(g.typescript())
        .pipe(gulp.dest('dist'));
});
```

**npm typescript**

```sh
tsc --project tsconfig.json --outDir dist
```

### Copy files

**Gulp**

```js
gulp.task('copy', () => {
    return gulp.src('src/index.html')
        .pipe(gulp.dest('dist/public'));
});
```

**Shell**

```sh
mkdir -p dist/public
cp src/index.html dist/public
```
