# 关于compose的三个阶段方面的一些性能优化细节
Modifier下的三个方法: Modifier.compose 组合阶段 Modifier.layout 布局阶段 Modifier.draw[...] 绘制阶段 注意这些方法的运行都是传入lambda作为参数
