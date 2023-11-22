---
title: Vscode log 颜色高亮配置
date: 2023-11-21 10:00:00
categories: [碎碎记]
---

用 vscode 查看 txt 或者 log 文件，把不同log 等级的颜色进行不同的配色，以便于更好的查看log 文件。

### 安装插件

Log File Highlighter

### 插件配置

```
{
  "security.workspace.trust.untrustedFiles": "open",
  "editor.accessibilitySupport": "off",
  "window.zoomLevel": 1,
  "files.associations": {
    "*.log-viewer": "log",
    "*.txt": "log",
  },
  "logViewer.options": {
  },
  "logViewer.logLevel": "trace",
  "logViewer.showStatusBarItemOnChange": true,
  "logFileHighlighter.customPatterns": [

    {
      "pattern": ".* D .*",
      "foreground": "#0070BB"
    },
    {
      "pattern": ".* I .*",
      "foreground": "#48BB31"
    },
    {
      "pattern": ".* E .*",
      "foreground": "#FF6B68"
    },
    {
      "pattern": ".* W .*",
      "foreground": "#BBB529"
    },
    {
      "pattern": " GC ",//GC
      "background": "#ee00c2"
    },
    {
      "pattern": "am_proc_died",//进程死亡
      "background": "#ee0000"
    },
    {
      "pattern": "am_proc_start",//进程启动
      "background": "#00c83f",
      "foreground": "#000000"
    },
    {
      "pattern": "wm_on_.+_called",//生命周期
      "background": "#044f1c"
    }
  ]
}

```

