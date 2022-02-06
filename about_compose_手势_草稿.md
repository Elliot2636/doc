# 调用
`Modifier` 上调用 `.pointer ...`开头的方法。

# 关于 `pointerHoverIcon`
[待回答 stack overflow 问题](https://stackoverflow.com/questions/70981631/what-is-the-difference-between-the-different-options-under-pointericondefaults-i)
``` kotlin
Column(
    Modifier
        .padding(top = 300.dp)
        .pointerHoverIcon(PointerIconDefaults.Text)) {
    SelectionContainer {
        Column {
            Text("Selectable text")
            Text(
                modifier = Modifier.pointerHoverIcon(PointerIconDefaults.Hand, true),
                text = "Selectable text with hand"
            )
        }
    }
    Text("Just text with global pointerIcon")
}
```

# 手势拦截
### 获取
``` kotlin
.pointerInput(Unit) {
    forEachGesture {
        awaitPointerEventScope {
            val down = this.awaitFirstDown(requireUnconsumed = true) // requireUnconsumed 设置为 true 则只会拦截未消耗的手势 若设置为false类似手势穿透
            if (down != null) {
                isPress = true
            }
            this.waitForUpOrCancellation()
            if (down.changedToDownIgnoreConsumed()) {
                isPress = false
            }
        }
    }
}
```
### 拦截
注意: compose的手势会穿透当前view层传递到对应点击位置的第一个消耗点击事件的元素，所以若是在一个有点击按钮的view层上在覆盖一层时，一定要在新增加的层次上添加`pointerInput`消耗掉手势操作
``` kotlin
Column(
    modifier = Modifier
        .fillMaxSize()
        .background(Color(0.2f, 0.2f, 0.2f, 0f))
        .pointerInput("create_todo_bg") {}
) {
	... ...
}
```

