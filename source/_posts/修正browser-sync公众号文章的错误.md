---
title: 修正browser-sync公众号文章的错误
date: 2017-01-21 22:30:29
tags:
---
首先说说声对不起，在上一篇的公众号文章：《放弃F5，拥抱browser-sync》中存在几个错误点。链接地址:

<https://mp.weixin.qq.com/s?__biz=MzAxMDgyOTgwOQ==&mid=2247483709&idx=1&sn=9939c3029c12ef1f716111cd0c9e9ffc&chksm=9b4b2ba3ac3ca2b5dea5496d6f9d87d7a0218ed85e4f807d4da2374957dd1b64cea234d5074c&mpshare=1&scene=1&srcid=0228DCwqHbO5bJNRzdNcoQaJ&key=1ffbac7579ea006ba638f1c527ceb6fccc5cd60675bb72cb4ac4e1669f8844ac48f5c811613c0700f5b5a5d0758631cddccd09a62852836bbe7ea0a2f3b6519205a05d50a53e595fa3c414a39a8f507f&ascene=0&uin=MTkwMTU1MzgyMw%3D%3D&devicetype=iMac+Macmini7%2C1+OSX+OSX+10.12.3+build(16D32)&version=12020010&nettype=WIFI&fontScale=100&pass_ticket=iTAw5XKKAiEh5rRG8zKg5HPSatL3GYf2%2FVDBxyBOTnbVmCeOf%2FgW%2FmhS5DctS64z>

几个错误点修改如下：
1. 文章中的：
*......更重要的是 Browsersync可以同时在PC、平板、手机等设备下进项调试...*
将“进项调试”修改为“进行调试”
2.　最后的代码有一个目录错误，因为我的粗心，给大家带来的不变，请见谅！在以后的文章中我会更加小心
发表文章，力求保证没有错误！
```
var gulp        = require('gulp');
var browserSync = require('browser-sync').create();
var browserify = require('gulp-browserify');
var sass        = require('gulp-sass');
var uglify = require('gulp-uglify');
// Compile sass into CSS & auto-inject into browsers
gulp.task('sass', function() {
    return gulp.src("app/scss/*.scss")
        .pipe(sass())
        .pipe(gulp.dest("dist/css"))
        .pipe(browserSync.stream());
});
// process JS files and return the stream.
gulp.task('js', function () {
    return gulp.src('app/js/*.js')
        .pipe(browserify())
        .pipe(uglify())
        .pipe(gulp.dest('dist/js'));
});
// Static Server + watching scss/js/html files
gulp.task('serve', ['sass','js'], function() {
    browserSync.init({
        server: "./app"
    });
    gulp.watch("app/scss/*.scss", ['sass']);
        gulp.watch("app/js/*.js", ['js']);
    gulp.watch("app/*.html").on('change', browserSync.reload);
});
gulp.task('default', ['serve']);
```
修改为：
```
var gulp        = require('gulp');
var browserSync = require('browser-sync').create();
var browserify = require('gulp-browserify');
var sass        = require('gulp-sass');
var uglify = require('gulp-uglify');
// Compile sass into CSS & auto-inject into browsers
gulp.task('sass', function() {
    return gulp.src("app/scss/*.scss")
        .pipe(sass())
        .pipe(gulp.dest(".app/dist/css"))
        .pipe(browserSync.stream());
});
// process JS files and return the stream.
gulp.task('js', function () {
    return gulp.src('app/js/*.js')
        .pipe(browserify())
        .pipe(uglify())
        .pipe(gulp.dest('.app/dist/js'));
});
// Static Server + watching scss/js/html files
gulp.task('serve', ['sass','js'], function() {
    browserSync.init({
        server: "./app"
    });
    gulp.watch("app/scss/*.scss", ['sass']);
        gulp.watch("app/js/*.js", ['js']);
    gulp.watch("app/*.html").on('change', browserSync.reload);
});
gulp.task('default', ['serve']);
```

参照对比原文地址：

<https://mp.weixin.qq.com/s?__biz=MzAxMDgyOTgwOQ==&mid=2247483709&idx=1&sn=9939c3029c12ef1f716111cd0c9e9ffc&chksm=9b4b2ba3ac3ca2b5dea5496d6f9d87d7a0218ed85e4f807d4da2374957dd1b64cea234d5074c&mpshare=1&scene=1&srcid=0228DCwqHbO5bJNRzdNcoQaJ&key=1ffbac7579ea006ba638f1c527ceb6fccc5cd60675bb72cb4ac4e1669f8844ac48f5c811613c0700f5b5a5d0758631cddccd09a62852836bbe7ea0a2f3b6519205a05d50a53e595fa3c414a39a8f507f&ascene=0&uin=MTkwMTU1MzgyMw%3D%3D&devicetype=iMac+Macmini7%2C1+OSX+OSX+10.12.3+build(16D32)&version=12020010&nettype=WIFI&fontScale=100&pass_ticket=iTAw5XKKAiEh5rRG8zKg5HPSatL3GYf2%2FVDBxyBOTnbVmCeOf%2FgW%2FmhS5DctS64z>

目前内容已经修改！欢迎反馈，欢迎交流：

![strongant公众号二维码](http://mmbiz.qpic.cn/mmbiz_png/bLPd4tHRLu6MfYBKkZ6Rkk5E2H92YaZN1JO92ub5SEVFEPxCHY8PCRHTLUHXiaghl4p7hRnxT8yySSdl7ZV7epA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)