# mac中vscode的四个文件配置

## c_cpp_properties.json

```json
{
    "configurations": [
        {
            "name": "Mac",
            "includePath": [
                "${workspaceFolder}/**",
            ],
            "defines": [],
            "macFrameworkPath": [
                "/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/System/Library/Frameworks"
            ],
            "compilerPath": "/usr/bin/clang++",
            "cStandard": "c17",
            "cppStandard": "c++17",
            "intelliSenseMode": "macos-clang-arm64"
        }
    ],
    "version": 4
}
```

## launcn.json

```json
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "lldb",
            "request": "launch",
            "name": "Debug",
           "program":  "${workspaceFolder}//test",
            "args": [],
           "cwd": "${workspaceFolder}",
           "preLaunchTask": "C/C++: clang++ 生成活动文件"
        }
    ]
}
```

## settings.json

```json
{
    "code-runner.runInTerminal": true,
    "code-runner.saveAllFilesBeforeRun": true,
    "code-runner.saveFileBeforeRun": true,
    "code-runner.preserveFocus": false,
    "cmake.configureOnOpen": true,
    "explorer.confirmDelete": false,
    "editor.fontSize": 18,
    "editor.fontFamily": "Fira Code",
    "explorer.confirmDragAndDrop": false,
    "files.autoSave": "onFocusChange",
    "editor.fontLigatures": true,
    "editor.fontWeight": "normal",
    "workbench.iconTheme": "material-icon-theme",
    "terminal.integrated.enableMultiLinePasteWarning": false,
    "code-runner.executorMap": {
        "cpp": "cd $dir && clang++ $fileName -o $test.out && $dir$test.out"
    }
}
```

## tasks.json

```json
{
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: clang++ 生成活动文件",
            "command": "/usr/bin/clang++",
            "args": [
                "-fcolor-diagnostics",
                "-fansi-escape-codes",
                "-g",
                "${file}",
                "-o",
                "${workspaceFolder}//test",
                "-std=c++17"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "调试器生成的任务。"
        }
    ],
    "version": "2.0.0"
}
```

