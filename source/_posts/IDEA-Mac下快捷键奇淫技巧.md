title: IDEA Mac下快捷键奇淫技巧
tags: 'IDEA,Mac快捷键'
reward: true
date: 2017-07-22 21:59:47
---
* 为你的ide设置背景图片；
只需要双击enter键，然后输入*set back*， 找到*Set Background Image* 选择你想要添加的背景图片即可。如果不需要设置图片，再次打开单击*clear*按钮即可清除。
*  若果你想展示自己点击的按钮快捷键，可以安装*Presentation Assistant*即可，安装完之后需要重启。
*  如果你想快速跳到某一个类的某一行，那么你可以使用*Command+O*,然后键入你想要跳转的类名称，然后输入冒号加行号；
* 如果你想看到你进入这个类中总共有哪些方法，你可以使用*Command+7*，此时便可以显示这个类中的所有方法；
* 如果你想找到某个类中的某个字段，你可以使用*Command+Option+O*,然后通过"/id"的方式，就可以找到所有包含id属性的类；
* 如果你想查看某个类中的变量或者方法在哪儿使用，直接使用*Command+B*即可；
* 如果你想查看某个变量的引用定义详情，则可以选中这个变量，然后使用*Command+Y*；
* 如果你想扩展左边项目结构窗口的大小，则可以使用*Command+Shift+>(右方向键)*；
* 如果你想对编辑器某些窗口进行显示和隐藏，则可以双击Shift键，然后输入"#editor ",则可以对当前编辑器进行一些快速设置；
* 如果你想在idea中快速测试rest服务，则可以双击*Shift*然后输入*test rest*，找到最后一项打开*rest test client*便可以对服务进行测试调用；
* 如果你想双击*Shift*后，键入*ws*便可以打开*test restful client tool*，可以在keymap设置中输入*test rest*，找到*Tools--Test Restful Webservice*，然后选中右键选择*Abbreviation*设置*ws*，点击确定，然后双击*Shift*，输入*ws*，这时候第一项就是这个工具，此时便可以快速进入*test restful client tool*工具窗口；
* 如果你想对某个类进行全屏编辑，则可以使用*Command+Shift+F12*；
* 如果想快速打开项目结构视图，则可以使用*Command+1*；
* 如果你想对代码给别人展示或者review代码的时候，想放大某个类，则可以在*view*视图下选择：*Enter Presenttion Mode*即可，当然你也可以设置快捷键进行绑定，这个功能特别有用,比如我设置的是*Command+Shift+S*，这样当需要对某个文件进行展示时，直接按快捷键即可，在*Presenttion Mode*窗口中，我们可以使用*Command+E*显示最近浏览的文件，可以快速切换展示；
* 编辑器垂直分割和水平分割可以在菜单来*Window*下的*edit tab*中找到并绑定对应的快捷键；
* 当选择一行或者某个列时，使用*option*+上下方向键，不要使用鼠标勾选的方式；
* 如果你使用了两次以上剪贴操作，你想查看前几次的剪贴内容，则可以使用*Commad+Shift+V*,此时便可以找到前几次的剪贴记录；
* 如果你选择了某一行，想向上下选取，则使用*option*+上下方向键后，可以再使用*shift+option*+上下方向键；
* 当你需要对代码样式进行一些改变时，则可以选中代码片段 然后使用*option+Enter*；
* 如果你想在某个包下面建立一个类，你可以使用*Command+上方向键*激活导航bar，然后选择相应的目录，然后使用*Command+N*,新建你需要新建的类型即可，不要使用鼠标选择File新建，这样会影响效率；
* 如果不想在view中显示navbar，则可以设置navbar隐藏，方法：双击*shift*，输入*nav*，找到*view navigation bar* 选择off，然后使用*Command*+向上方向键便可以激活navbar；
* 如果你想使用BufferReader读取一个文件，此时你键入`BufferReader bf = new`的时候可以使用*shift+option+space*智能导入其派生类，由于 *shift+option+space*快键键可能会和输入法切换会有冲突，我设置成了*shift+option+command+space*；
* 如果你想在idea中引入包或者包裹异常，则可以使用*option+Enter*；
* 如果你想要对某个变量进行NPE验证，那么只需要使用这个变量名打"."然后输入*not*，这时候选择相应的代码模板即可；
* 如果你想在代码的末尾添加分号，不要移动光标添加，直接使用*shift+command+回车*即可；
* 如果你想手写一个简单的JSON，可能需要使用转义字符进行转义双引号，此时你可以在字符串中使用*option*+回车选择*Inject language reference*选择JSON，然后再次使用*option+回车键*，选择*Edit Json Fragement*即可，此时你便可以在JSON 窗口中按照正常的方式编写JSON字符串了，IDE会自动帮你添加转义字符；同样的方式我们可以选择*Regex*，对正则进行编写，并且可以帮我们进行对正则校验，使用方法和JSON 输入的方式类似；
* 如果需要多行选中，则可以使用*option+shift+鼠标点击* 即可，或者可以使用*control+G*,然后继续选择你需要多行同时编辑的行，如果选择的行数多了，可以使用*control+shift+g*进行减少选中；
* 如果需要对选中的变量或者代码片段进行重构，则可以使用*control+T*；
* 对bool参数值进行转换，则可以对定义的bool变量选中然后使用*control+T*，输入*invert*，找到*invert boolean*，便可以对变量的值进行反转；
* 如果想对项目进行版本控制管理，使用*Command+K*或者使用*Ctrl+V*；
* 使用*control+tab*可以进行对不同的文件进行选择显示打开；
* 如果你想查看你目前使用快捷键的情况，则可以在idea的*help*菜单找到*Poductivity Guide*查看；
**注意：以上快捷键主要是Mac系统下的操作，如果你使用的是非Mac系统，那么你只需要安装Presentation Assistant便可以显示Linux和Windows上的快捷键**
如果想深入学习，可以参考该视频链接：
<https://www.youtube.com/watch?v=M2eL5YuqecQ&list=PLQ176FUIyIUYUuSwE--flZWw2hfI21SjF&index=2>