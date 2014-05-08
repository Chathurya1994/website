J'ai bien galéré lorsque j'ai dû passer de **grunt** à **gulp**. Non pas que gulp soit compliqué mais retrouver exactement le même _workflow_ qu'avant sachant que gulp est jeune et que les _plugins_ sont bien moins nombreux que sur grunt, forcément ce n'était pas si évident.

M'enfin, on trouve toujours une solution. Et là, justement mon problème était de répliquer mon _process_ de **svg-to-font**.

Voici comment faire.

## gulp-iconfont

Tout d'abord, installez évidemment **gulp** et faites ce que vous avez à faire avec. Vous êtes prêt(e) ? Okay, go.

### Intallez les _packages_

Oui, deux packages, [gulp-iconfont](https://github.com/nfroidure/gulp-iconfont) et [gulp-iconfont-css](https://github.com/backflip/gulp-iconfont-css).

```
$ npm install gulp-iconfont gulp-iconfont-css --save-dev
```

### Importez le

```
// import
var gulp = require('gulp')

var iconfont = require('gulp-iconfont')
  , iconfontCss = require('gulp-iconfont-css')
```

### Créez votre tâche gulp

```
// glyphicons
gulp.task('glyphicons', function() {
 return gulp.src('src/glyphicons/**/*') // où sont vos svg
    .pipe(iconfontCss({
      fontName: 'icons', // nom de la fonte, doit être identique au nom du plugin iconfont
      targetPath: '../../styles/shared/icons.css', // emplacement de la css finale
      fontPath: '../fonts/' // emplacement des fontes finales
    }))
    .pipe(iconfont({
      fontName: 'icons' // identique au nom de iconfontCss
     }))
    .pipe( gulp.dest('src/assets/fonts') )
})
```


### Fichier final

Ce qui donne :

```
// import
var gulp = require('gulp')

var iconfont = require('gulp-iconfont')
  , iconfontCss = require('gulp-iconfont-css')

gulp.task('glyphicons', function() {
 return gulp.src('src/glyphicons/**/*')
    .pipe(iconfontCss({
      fontName: 'icons', // nom de la fonte, doit être identique au nom du plugin iconfont
      targetPath: '../../styles/shared/icons.css', // emplacement de la css finale
      fontPath: '../fonts/' // emplacement des fontes finales
    }))
    .pipe(iconfont({
      fontName: 'icons' // identique au nom de iconfontCss
     }))
    .pipe( gulp.dest('src/assets/fonts') )
})
```

Et voilà, on est bon.
