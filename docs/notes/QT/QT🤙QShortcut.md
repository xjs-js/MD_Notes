---
tags: [Notebooks/QT]
title: "QT\U0001F919QShortcut"
created: '2019-10-03T10:39:36.187Z'
modified: '2020-03-08T03:12:06.531Z'
---

# QT:call_me_hand:QShortcut

## Basic Usage
<details>
<summary>1</summary>
<markdown>

```cpp
QAction copyAct = new QAction(tr("&Copy"), this);
copyAct->setShortcut(QKeySequence("Ctrl+Shift+F1"));
connect(copyAct, &QAction::triggered, this, &MainWindow::copy);
```

</markdown>
</details>

<details>
<summary>2</summary>
<markdown>

```cpp
QShortcut shortcut = new QShortcut(QKeySequence("Ctrl+Shift+F1"), this);
connect(shortcut, &QShortcut::activated, this, &Mainwindow::copy);
```

</markdown>
</details>
