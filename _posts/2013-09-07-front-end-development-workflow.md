---
layout: post
title: "front end development workflow"
description: "fe development workflow"
category: 
tags: [fe]
---

# 前端开发流程

安装略去. 需要 node, npm, bower, grunt. 安装时都 `-g` 全局安装.


## 开发环境初始化  [npm](https://npmjs.org/)

创建npm的配置文件, **package.json**  或者通过 npm init 来创建. 

在配置文件中, 通过 **dependencies**/**devDependencies** 指定项目依赖后, 运行 `npm install` 便可自动将项目依赖打包安装进项目根目录.

另外, 还可以通过 `npm install pkgname --save` 来完成 **package.json** 中项目依赖的添加.

注:  package.json 的相关帮助 `npm help  package.json`

示例:


    {
        "name": "y1",
        "devDependencies": {
            "grunt": "latest",
            "grunt-contrib-concat": "latest"
        }
    }


## 依赖管理 [bower](http://bower.io/)

和 上一步初始化非常类似, 也是创建针对bower的配置文件, `bower.json` 可以通过 `bower init` 来创建. 

配置文件中, 通过 **dependencies** 指定前端依赖后, 运行 `bower install`.

`bower install pkgname --save` 同样可行.

另外, 一般 bower 安装的文件默认在 **bower_components**,  这个如果需要改变的话, 可以在项目根目录下新建 **.bowerrc** 文件, 指定 **directory** 目录. [配置相关](https://docs.google.com/document/d/1APq7oA9tNao1UYWyOm8dKqlRP2blVkROYLZ2fLIjtWc/edit#heading=h.4pzytc1f9j8k)

示例:

    {
        "name": "y1",
        "dependencies": {
          "underscore": "latest",
          "jasmine-ajax": "git@github.com:pivotal/jasmine-ajax.git"
        }
    }


## 自动化 [Grunt](http://gruntjs.com/)

手动创建 **Gruntfile.js**, 该文件中定义各种[任务](http://gruntjs.com/plugins), 比如压缩js, css, 合并文件等.

前提需要在package.json中配置所需要的插件, 然后安装.

简单示例. 


    module.exports = function(grunt) {

        var jsfiles = [ 'components/jquery/jquery.js',
                        'components/underscore/underscore.js',
                        'javascripts/module.js' ],
            cssfiles = 'stylesheets/*.css';

        grunt.initConfig({
            concat: {
                js: {
                    options: { separator: ';' },
                    src: jsfiles,
                    dest: 'app/javascripts/lib.js'
                },
                css: {
                    options: { separator: '' },
                    src: cssfiles,
                    dest: 'app/stylesheets/page.css'
                }
            },
            watch: {
                autoConcatJs: {
                    files: [jsfiles],
                    tasks: ['concat:js']
                },
                autoConcatCss:{
                    files: [cssfiles],
                    tasks: ['concat:css']                
                }
            }        
        });
        grunt.loadNpmTasks('grunt-contrib-concat');
        grunt.loadNpmTasks('grunt-contrib-watch');
    };


其中,**Gruntfile.js** 完全由js编写. 

以上配置文件, 用到了俩个grunt 插件: 

* [grunt-contrib-concat](https://npmjs.org/package/grunt-contrib-concat) 
* [grunt-contrib-watch](https://npmjs.org/package/grunt-contrib-watch)

**js** 和 **css** 分别为任务名, 命令行 `grunt concat:js` 便可执行所定义的任务. options的separator配置指明了文件拼接所用的字符,这个在js和css文件中时不同的. 在 **autoConcatCss** 中, **task**表明需要触发的任务, **files** 指代关注的文件列表.


ENF



