# WINDOWS系统下对VSCODE的配置总结

# mingw放在c盘根目录下,安装medium的fira code

## c_cpp_properties.json

```json
{
    "configurations": [
        {
          "name": "Win32",
          "includePath": ["${workspaceFolder}/**"],
          "defines": ["_DEBUG", "UNICODE", "_UNICODE"],
          "windowsSdkVersion": "10.0.17763.0",
          "compilerPath": "C:\\mingw64\\bin\\g++.exe",  
          "cStandard": "c11",
          "cppStandard": "c++17",
          "intelliSenseMode": "${default}"
        }
      ],
      "version": 4
}


```

## launch.json

```json
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "g++.exe build and debug active file",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}\\test.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "C:\\mingw64\\bin\\gdb.exe",		/*修改成自己bin目录下的gdb.exe，这里的路径和电脑里复制的文件目录有一点不一样，这里是两个反斜杠\\*/
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "task g++"
        }
    ]
}
```

## settings.json

```json
{
    /*editor*/
    "editor.cursorBlinking": "smooth",//使编辑器光标的闪烁平滑，有呼吸感
    "editor.formatOnPaste": true,//在粘贴时格式化代码
    "editor.formatOnType": true,//敲完一行代码自动格式化
    "editor.smoothScrolling": true,//使编辑器滚动变平滑
    "editor.tabCompletion": "on",//启用Tab补全
    "editor.fontFamily": "'fira code', '思源黑体'",//字体设置，个人喜欢Jetbrains Mono作英文字体，思源黑体作中文字体
    "editor.fontSize": 20, //设置字体大小
    "editor.fontWeight": "normal", //这个设置字体粗细，可选normal,bold,"100"~"900"等，选择合适的就行
    "editor.fontLigatures": true,//启用字体连字
    "editor.detectIndentation": false,//不基于文件内容选择缩进用制表符还是空格
    /*
    因为有时候VSCode的判断是错误的
    */
    "editor.insertSpaces": true,//敲下Tab键时插入4个空格而不是制表符
    "editor.copyWithSyntaxHighlighting": false,//复制代码时复制纯文本而不是连语法高亮都复制了
    "editor.suggest.snippetsPreventQuickSuggestions": false,//这个开不开效果好像都一样，据说是因为一个bug，建议关掉
    "editor.stickyTabStops": true,//在缩进上移动光标时四个空格一组来移动，就仿佛它们是制表符(\t)一样
    "editor.wordBasedSuggestions": false,//关闭基于文件中单词来联想的功能（语言自带的联想就够了，开了这个会导致用vscode写MarkDown时的中文引号异常联想）
    "editor.linkedEditing": true,//html标签自动重命名（喜大普奔！终于不需要Auto Rename Tag插件了！）
    "editor.wordWrap": "on",//在文件内容溢出vscode显示区域时自动折行
    "editor.cursorSmoothCaretAnimation": "on",//让光标移动、插入变得平滑
    "editor.renderControlCharacters": true,//编辑器中显示不可见的控制字符
    "editor.renderWhitespace": "boundary",//除了两个单词之间用于分隔单词的一个空格，以一个小灰点的样子使空格可见
    /*terminal*/
    "terminal.integrated.defaultProfile.windows": "Command Prompt",//将终端设为cmd，个人比较喜欢cmd作为终端
    "terminal.integrated.cursorBlinking": true,//终端光标闪烁
    "terminal.integrated.rightClickBehavior": "default",//在终端中右键时显示菜单而不是粘贴（个人喜好）
    /*files*/
    "files.autoGuessEncoding": true,//让VScode自动猜源代码文件的编码格式
    "files.autoSave": "onFocusChange",//在编辑器失去焦点时自动保存，这使自动保存近乎达到“无感知”的体验
    "files.exclude": {//隐藏一些碍眼的文件夹
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/CVS": true,
        "**/.DS_Store": true,
        "**/tmp": true,
        "**/node_modules": true,
        "**/bower_components": true
    },
    "files.watcherExclude": {//不索引一些不必要索引的大文件夹以减少内存和CPU消耗
        "**/.git/objects/**": true,
        "**/.git/subtree-cache/**": true,
        "**/node_modules/**": true,
        "**/tmp/**": true,
        "**/bower_components/**": true,
        "**/dist/**": true
    },
    /*workbench*/
    "workbench.list.smoothScrolling": true,//使文件列表滚动变平滑
    "workbench.editor.enablePreview": false,//打开文件时不是“预览”模式，即在编辑一个文件时打开编辑另一个文件不会覆盖当前编辑的文件而是新建一个标签页
    "workbench.editor.wrapTabs": true, //隐藏新建无标题文件时的“选择语言？”提示（个人喜好，可以删掉此行然后Ctrl+N打开无标题新文件看看不hidden的效果）
    /*explorer*/
    "explorer.confirmDelete": false,//删除文件时不弹出确认弹窗（因为很烦）
    "explorer.confirmDragAndDrop": false,//往左边文件资源管理器拖动东西来移动/复制时不显示确认窗口（因为很烦）
    /*search*/
    "search.followSymlinks": false,//据说可以减少vscode的CPU和内存占用
    /*window*/
    "window.menuBarVisibility": "visible",//在全屏模式下仍然显示窗口顶部菜单（没有菜单很难受）
    "window.dialogStyle": "custom",//使用更具有VSCode的UI风格的弹窗提示（更美观）
    /*debug*/
    "debug.internalConsoleOptions": "openOnSessionStart",//每次调试都打开调试控制台，方便调试
    "debug.showBreakpointsInOverviewRuler": true,//在滚动条标尺上显示断点的位置，便于查找断点的位置
    "debug.toolBarLocation": "docked",//固定调试时工具条的位置，防止遮挡代码内容（个人喜好）
    "debug.saveBeforeStart": "nonUntitledEditorsInActiveGroup",//在启动调试会话前保存除了无标题文档以外的文档（毕竟你创建了无标题文档就说明你根本没有想保存它的意思（至少我是这样的。））
    "debug.onTaskErrors": "showErrors",//预启动任务出错后显示错误，并不启动调试
    /*html*/
    "html.format.indentHandlebars": true,
    "workbench.editor.empty.hint": "hidden" ,//在写包含形如{{xxx}}的标签的html文档时，也对标签进行缩进（更美观）
    
	"code-runner.executorMap": {
    "cpp": "cd $dir && g++ $fileName -g -o $test.exe -std=c++11 && $dir$test.exe"
	},
	"code-runner.runInTerminal": true,
}
```

## tasks.json

```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558 
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
        "type": "shell",
        "label": "task g++",
        "command": "C:\\mingw64\\bin\\g++.exe",	/*修改成自己bin目录下的g++.exe，这里的路径和电脑里复制的文件目录有一点不一样，这里是两个反斜杠\\*/
        "args": [
            "-g",
            "${file}",
            "-o",
            "${workspaceFolder}\\test.exe",
            "-I",
            "E:\\Cpp code",      /*修改成自己放c/c++项目的文件夹，这里的路径和电脑里复制的文件目录有一点不一样，这里是两个反斜杠\\*/
            "-std=c++17"
        ],
        "options": {
            "cwd": "C:\\mingw64\\bin"	/*修改成自己bin目录，这里的路径和电脑里复制的文件目录有一点不一样，这里是两个反斜杠\\*/
        },
        "problemMatcher":[
            "$gcc"
        ],
        "group": "build",
        
        }
    ]
}

```

