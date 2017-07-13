FDS-43-gulp
========

- 참고: <http://seungha-kim.github.io/gulp-lecture>

## GULP
- 빌드도구
- JS코드를 이용해 빌드 과정 정의
- Node.js Stream 활용 - 디스크 쓰기를 최소화

## gulp-sass
- 참고: <http://blueng.tistory.com/5>
- Gulp를 사용해서 Sass 컴파일
- app폴더 안에 있는 scss 파일을 자동으로 css로 변환하여 dist폴더에 넣어준다.
```bash
$ npm install gulp-sass --save-dev
```

```js
var sass = require('gulp-sass');
 
gulp.task('sass', function () {
  return gulp.src('./sass/**/*.scss')
    .pipe(sass().on('error', sass.logError))
    .pipe(gulp.dest('./css'));
});
 
gulp.task('sass:watch', function () {
  gulp.watch('./sass/**/*.scss', ['sass']);
});
```


## gulp-sourcemaps
- 파일 역추적, 코드상의 위치를 알려주는 것(개발자 도구에서)
- 참고: <http://webclub.tistory.com/470>
```bash
$ npm install gulp-sourcemaps --save--dev
```
```js
var sourcemaps = require('gulp-sourcemaps'), // sourcemaps 호출

gulp.task('javascript', function() {
  gulp.src('src/**/*.js')
    .pipe(sourcemaps.init())
      .pipe(plugin1())
      .pipe(plugin2())
    .pipe(sourcemaps.write())
    .pipe(gulp.dest('dist'));
});

```