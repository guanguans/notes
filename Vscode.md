# Vscode.md

## Users Settings

``` json
{
    "workbench.colorTheme": "Monokai",
    "terminal.integrated.shell.windows": "D:\\Git\\bin\\bash.exe", // 终端在 Windows 上使用的 Shell 的路径。
    "files.trimTrailingWhitespace": true,
    "files.insertFinalNewline": true,
    "files.trimFinalNewlines": true,
    "workbench.iconTheme": "material-icon-theme",
    "trailing-spaces.trimOnSave": true,
    "files.autoSave": "afterDelay",
    "files.autoSaveDelay": 3000,
    "workbench.statusBar.feedback.visible": false,
    "phpfmt.enable_auto_align": true
}
```

## XDebug 配置

``` json
{
    // 使用 IntelliSense 了解相关属性。
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "log": true,
            "localSourceRoot": "${workspaceRoot}",
            "serverSourceRoot": "/var/www/laravel",
            // "pathMappings": {
            //     "/var/www/laravel": "${workspaceRoot}"
            // },
            "port": 9000
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9000
        }
    ]
}
```
