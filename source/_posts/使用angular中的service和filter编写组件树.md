title: 使用angular中的service和filter编写组件树
author: strongant
tags:
  - angularjs
categories: []
date: 2017-08-05 16:49:00
---
> 学习《AngularJS深度剖析与实践》总结
* 在我们平时的开发中，需要对某些数据进行以树的形式进行展现，比如：权限角色、菜单、嵌套评论等。这个时候我们需要使用angular进行对数据抽象，构造我们自己的组件树：
* 例子：我们就拿主题树作为一个例子，然后一步一步去优雅的实现它:

1. 首先我们准备好angular的库文件，建立好相应的目录及文件，按照angular遵循的风格：约定优于配置。首先我们创建一个用于展示的目录，theme-tree
```
mkdir theme-tree && cd $_
```
2.创建需要展示的html页面文件:
```
touch index.html
```
3.创建存放项目js文件的目录:
```
mkdir js
```
4.创建存放angular项目的controller目录、service目录和filter目录:
```
mkdir controller && mkdir service && mkdir filter
```
5.创建angular项目的入口文件，app.js
```
cd js && touch app.js
```
6.目前先不考虑UI效果部分，主要以实现功能为主，我们使用bower来安装和管理相应的js第三方库文件，如果没有安装bower工具，可以借助npm进行安装-npm install -g bower ,在我们创建的theme-tree目录下，键入如下命令安装angular库的依赖：
```
bower install angular --save
```
以上命令实行完毕后我们的目录结构如下：
![目录文件显示](http://upload-images.jianshu.io/upload_images/1310396-c3be8338ba3a864d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

7.接下来我们开始编辑js/app.js入口文件：
```
angular.module('myApp', []);
```
8.接下来我们开始编写控制器文件js/controller/index.client.controller.js:
```
angular.module('myApp').controller("ThreedTreeCtrl",function ThreedTreeCtrl(tree) {
        var vm = this;
        vm.items = [{
                id: 1,
                title: "Java",
                poster: "Messi",
                dateCreated: "2012-02-19T00:00:00",
                items: [{
                        id: 11,
                        title: 'Spring',
                        poster: 'John',
                        dateCreated: "2012-02-19T00:00:00",
                        items: [
                                {
                                        id: 111,
                                        title: 'AOP',
                                        poster: 'Mike',
                                        dateCreated: "2016-02-19T00:00:00",
                                         items: [
                                {
                                        id: 1111,
                                        title: 'IOC',
                                        poster: 'Jack']
                                }
                        ]
                }, {

                                id: 2,
                                title: "SpringBoot",
                                poster: "Lucy",
                                dateCreated: "2011-02-19T00:00:00"
                        }
                ]
        }, {
                        id: 2,
                        title: "JavaScript",
                        poster: "Jack",
                        dateCreated: "2012-02-19T00:00:00",
                }
        ];
});

```
以上内容很简单，构建了一个ThreedTreeCtrl控制器，里面嵌套了一些随意的数据，主要是为了模拟父子关系；

9.接下来我们编辑js/service/index.client.service.js文件，用于对数据进行附加相应的行为。思考一下，当我们有了这样一组数据后，我们要为它添加什么方法和属性，首先应该添加父节点是否折叠，此属性主要是为了在界面显示的时候展开或折叠子节点数据。当展开的时候我们使用“-”表示，折叠的时候我们使用"+"表示，当折叠时单击节点应该展开子节点，当展开的时候，单击子节点应该折叠父节点；将新增的属性和方法为了减小和原始数据冲突，并且这些数据通过$http或者$resource提交给服务器，它们所调用的angular.toJso()函数会忽略所有以$开头的属性，这样我们扩展的属性就不会被提交到服务端了。还有一个方便的是，当我们看到数据上有"$"开头的属性就是扩展的属性。接下来我们实现它：
```
angular.module('myApp').service('tree',function Tree(){
    var self = this;
    //为每一项节点添加属性和方法
    var enhanceItem = function(item,childrenName){
        item.$hasChildren = function(){
            var subItems = this[childrenName];
            return angular.isArray(subItems) && subItems.length;
        };
        item.$foldToggle = function(){
            this.$folded = !this.$folded;
        };
        item.$isFolded = function(){
            return this.$folded;
        };
    };

    //对传进来的数据进行强化
    this.enhance = function(items,childrenName){
        if(angular.isUndefined(childrenName)){
            childrenName = "items";
        }
        angular.forEach(items,function(item){
            enhanceItem(item,childrenName);
            //如果有子节点则递归处理
            self.enhance(item[childrenName],childrenName);
        });
        console.log(items);
        return items;
    };
});

```

10.这样我们完成了对数据进行强化，此时我们如果直接在controller调用service的enhance 方法，将服务端返回的json数据进行加强，为他们添加的相应的属性和方法，然后在页面进行展示调用就可以了，但是这样感觉比较脏，不干净，我们不在contrller直接调用service里面的enhance 方法，我们可以创建一个过滤器来对数据进行添加过滤的功能，接下来我们开始编辑filter/index.client.filter.js:

```
angular.module('myApp').filter('tree',function(tree){
    return function(items,childrenName){
        tree.enhance(items,childrenName);
        return items;
    };
});

```
11.接下来编写html文件，开始对主题树进行展现并且引入相关文件：
```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
</head>

<body>

    <div ng-app="myApp" ng-controller="ThreedTreeCtrl as vm">
        <ul ng-if="vm.items">
            <li ng-repeat="item1 in vm.items | tree">
                <div ng-click="item1.$foldToggle()">
                    <span ng-if="item1.$hasChildren()">
                    <span ng-if="!item1.$isFolded()">-</span>
                    <span ng-if="item1.$isFolded()">+</span>
                    </span>
                    {{ item1.title }}
                </div>

                <ul ng-if="item1.$hasChildren() && !item1.$isFolded()">
                    <li ng-repeat="item2 in item1.items">
                        <div ng-click="item2.$foldToggle()">
                            <span ng-if="item2.$hasChildren()">
                    <span ng-if="!item2.$isFolded()">-</span>
                            <span ng-if="item2.$isFolded()">+</span>
                            </span>
                            {{ item2.title }}
                        </div>

                        <ul ng-if="item2.$hasChildren() && !item2.$isFolded()">
                            <li ng-repeat="item3 in item2.items">
                                {{ item3.title }}
                            </li>
                        </ul>
                    </li>
                </ul>
            </li>
        </ul>

    </div>
    <script src="bower_components/angular/angular.js"></script>
    <script src="js/app.js"></script>
     <script src="js/controller/index.client.controller.js"></script>
    <script src="js/service/index.client.service.js"></script>
    <script src="js/filters/index.client.filter.js"></script>
    
     
</body>

</html>

```
此时我们便完成了对主题树功能的实现，在index.html文件中，我们只展示了两层嵌套关系以作为示例，根据自己的业务场景进行扩展。
以上实现还不够优雅，等待以后需要将主题递归树封装为指令，最后附上github地址:
<https://github.com/strongant/angularjs>
源码位于此仓库下的angular-tree目录，欢迎提出issue。