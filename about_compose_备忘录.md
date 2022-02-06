# 关于 compose 的三个阶段方面的一些性能优化细节
`Modifier`下的三个方法: Modifier.compose 组合阶段 Modifier.layout 布局阶段 Modifier.draw[...] 绘制阶段 注意这些方法的运行都是传入lambda作为参数 这些方法会为使用的可组合项跳过某些阶段，对于那些依赖变量而不是lambda的方法会直接从组合阶段重新开始 组合阶段 -> 布局阶段 -> 绘制阶段 这样对于某些频繁变化但没有必要经历完整阶段的可以从这些方面优化性能。
自定义布局 用的是Layout可以做到布局基元的控制（即可以做到多帧的合并后绘制，上面Modifier.layout也可以做到对调用的组合项合并一些帧, 但是不可以跨越组合项）
新添加的两个方法 placeWithLayer 与 placeRelativeWithLayer 会在 Placeable 元素下 引入一个图形层放入 layerBlock，当移动元素时可以跳过绘制阶段 [链接](https://developer.android.com/reference/kotlin/androidx/compose/ui/layout/Placeable.PlacementScope#(androidx.compose.ui.layout.Placeable).placeRelativeWithLayer(androidx.compose.ui.unit.IntOffset,kotlin.Float,kotlin.Function1))


# To-do
- [ ] Compose 如何实现手势拦截 https://developer.android.com/training/gestures/viewgroup
