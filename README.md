# You do not (may not) need Gulp

#### Delete files and folders
###### Gulp
```js
const del = require('del');

gulp.task('clean', () => {
  return del(['dist/report.csv', 'dist/mobile/**/*']);
});
```
###### npm del-cli
```sh
npx del "dist/report.csv" "dist/mobile/**/*"
```
###### Shell
```sh
rm -rf "dist/report.csv" "dist/mobile"
```

#### ESLint
###### Gulp
```js
gulp.task('eslint', () => {
    return gulp.src('src/**/*.ts')
        .pipe(g.eslint())
        .pipe(g.eslint.format());
});
```
###### npm eslint
```sh
npx eslint src --ext ts
```

#### ESLint in watch mode
###### Gulp
```js
gulp.task('eslint:watch', (done) => {
    const w = gulp.watch('src/**/*.ts', { ignoreInitial: false }, gulp.series('eslint'));
    process.on('SIGINT', () => {
        w.close();
        done();
    });
});
```
###### npm watchexec-bin
```sh
watchexec -w src "npm run eslint"
```

<!--
#### Watch

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