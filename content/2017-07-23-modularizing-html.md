+++

date = "2017-07-23T19:31:38+03:00"
description = "Using Gulp to automate tasks and using Nunjucks as a template engine. This articles explains the basics of doing so"

title = "Modularising & Automating your workflow using Gulp and Nunjucks"

[taxonomies]
tags = ["howto", "productivity", "programming"]
categories = ["y"]
+++

This weekend, I thought it would be cool to discuss my current web dev workflow here. I realised that writing websites is a pain to some. Some of the stuff I discuss here have been around for quite a while yet alot of people don't use 'em. In this article, I talk about some *gulp recipés* and `nunjucks`- a really cool javascript templating engine. I hope this turns out to be useful to someone out there.

First things first, what is `Gulp` and what is a templating engine? The Gulp [website](http://gulpjs.com/URL ) best summarizes what `Gulp` is-- a toolkit for automating painful or time-consuming tasks in your dev work, so you can stop messing around and build something. Template engines are toolkits that enable you to modularise your HTML code(you can break your HTML into chunks and reuse it in other HTML files) in addition to providing you with some really cool ways to interact with data, like looping and passing data.

To do all the aforementioned things, you need `nodejs`- a javascript runtime built on Chrome's V8 Javascript engine. Go [here](https://nodejs.org/en/URL ) to download NodeJs.

In order to make things more intuitive, let's build some really simple website that has 3 pages: index.html; about.html; and contact.html.
We start off by creating some directory structure that'll look this:
```
.
├── app
│   ├── css
│   ├── pages
│   ├── scss
│   └── templates
│       └── partials
└── dist
```
The *pages* folder will be used to store ninjucks files that will be compiled to HTML. The *templates* folder is used to store nunjucks "partials" that will be used in files located in the *pages* folder. Partials are smaller html files that can be added to another file. To create the above dir structure run:
```
mkdir -p dist/ app/{scss,css,pages,templates/partials}
```
From the root of your project, initialise your project folder using `npm` by running:
```
npm init
```
Answer the questions that npm gives you. After doing this, it's time to install useful node packages that we will use in our dev work which are:
`gulp` (the gulp toolkit); `browser-sync` (time-saving synchronised browser testing as a node module); `gulp-sass` (converts sass to css); `gulp-cssmin` (minifies css); `gulp-newer`; and `gulp-nunjucks-render` (render nunjuck files).
For now, let's work with these modules. In this tutorial, I chose to install the modules locally in the project folder by running:
```
npm install gulp{,-sass,-cssmin,-newer,-nunjucks-render} browser-sync --save-dev
```

We start off by creating a basic layout file that will be used in all our html files:
app/templates/layout.njk:

```
<!--app/templates/layout.njk -->
<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8"/>
        {% block title %} {% endblock %}
        <link rel="stylesheet" href="css/styles.css">
    </head>
    <body>
        {% include "partials/navigation.njk" %}
        {% block content %} {% endblock %}
    </body>
</html>
```
This is the basis for all other html files in our project. We use our layouts.njk as our boilerplote code. You should have hopefully noticed that there are some fancy "handles" i.e `{% stuff %} {% endblock %}` going on. In nunjucks, the handles will be replaced later by a block of html markup that is more useful. You shall see this later.

Now, let's create our pages using the layout's boiler plate code. Head over to our `pages` folder and create 3 files: index.njk, about.njk, and contact.njk. Put the following code in the respective files:

app/pages/index.njk:
```
<!-- index.njk -->
{% extends "layout.njk" %}

{% block title %}
    Home
{% endblock %}
{% block content %}
    <p class="m-text">I am the home page</p>
{%  endblock %}
```

app/pages/about.njk:
```
<!-- app/pages/about.njk/about.njk -->
{% extends "layout.njk" %}

{% block title %}
About
{% endblock %}
{% block content %}
<p class="m-text">About. Just another tutorial</p>
{%  endblock %}
```

app/pages/contact.njk:
```
<!-- app/pages/contact.njk -->
{% extends "layout.njk" %}

{% block title %}
    About
{% endblock %}
{% block content %}
    <p class="m-text">Get in touch with me</p>
{%  endblock %}
```

Let's also create some very basic navigation that'll look something like this:
app/templates/partials/navigation.njk:
```
<!-- app/templates/partials/navigation.njk -->
<navigation>
    <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="contact.html">Say Hi!</a></li>
    </ul>
</navigation>
```
Let's add some fancy basic style using scss. Go to our scss file and add the following:
app/scss/styles.scss:
```
<!-- app/scss/styles.scss -->
.m-text {
    border: solid 2px green;
}
```
Now let's write our gulp recipé that looks something like this:
./gulpfile.js
```
var gulp           = require('gulp');
var browserSync    = require('browser-sync').create();
var cssmin         = require('gulp-cssmin');
var sass           = require('gulp-sass');
var nunjucksRender = require('gulp-nunjucks-render');
var newer          = require('gulp-newer');
var reload         = browserSync.reload;
var src = {
  scss : 'app/scss/**/*.scss',
  css  : 'app/css/',
  njk  : 'app/**/*.njk',
  dist  : 'dist/'
};

gulp.task('serve', ['scss', 'nunjucks'], function() {
  browserSync.init({
    server: "./app"
  });
  gulp.watch(src.njk, ['nunjucks']),
  gulp.watch(src.scss, ['scss']);
  gulp.watch(src.html).on('change', reload);
});

// Converting njk files to html
gulp.task('nunjucks', function() {
  return gulp.src('app/pages/**/*.+(html|njk|nunjucks)')
  // We do not need the data.json for this demo but you can use it if you wanna
    //.pipe(data(function(){
    //  return require('./app/data.json');
    //}))
    .pipe(nunjucksRender({
      path: ['app/templates/']
    }))
    .pipe(gulp.dest('app'))
    .pipe(reload({stream: true }));
});

// HTML Processing
gulp.task('html', ['images'], function(){
  return gulp.src(src.html)
    .pipe(newer(src.html))
    .pipe(gulp.dest(src.dist));
});

// Converting scss files to css files
gulp.task('scss', function(){
  return gulp.src(src.scss)
    .pipe(sass().on('error', sass.logError))
    .pipe(gulp.dest(src.css))
    .pipe(reload({stream: true}));
});

gulp.task('default', ['serve']);

gulp.task('minify-css', ['sass', 'scss'], function(){
  return gulp.src(src.css + '**/*.css')
    .pipe(cssmin())
    .pipe(gulp.dest(src.dist + 'css'));
});

gulp.task('production', ['nunjucks', 'html', 'minify-css']);

```
From your terminal, run `gulp serve`. The website will be served from your localhost. Editing the scss files will cause the browser to reload. Try it:)

Running `gulp serve` from your terminal executes the `scss` and `nunjucks` tasks. The `scss` task converts any `scss` files into `css` files while the `nunjucks` task converts the `nunjucks` files into valid html. I've also added a `gulp production` task that minifies css in addition to copying relevant files to the the `dist` folder.

By now, you hopefully have a rough idea of how to modularise your work with a templating engine and automating tasks(minifying css, reloading the browser when files change, conveting njk files to html etc etc). You can do so much more with gulp and nunjucks beyond what I've discussed here. Using gulp(or something similar) saves you alot of time by automating your work. Using a templating engine makes your mark up more sane by breaking large chunks of html into manageable chunks.
