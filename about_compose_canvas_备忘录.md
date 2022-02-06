# 包
1. `androidx.compose.foundation.Canvas` (`@Composable`)
  ``` kotlin
  @Composable
  fun Canvas(modifier: Modifier?, onDraw: (@ExtensionFunctionType DrawScope.() -> Unit)?): Unit
  ```
2. `androidx.compose.ui.graphics.Canvas` (底层 canvas 控制)
  ``` kotlin
  \\ 使用方法 https://developer.android.com/reference/kotlin/androidx/compose/ui/graphics/drawscope/package-summary#(androidx.compose.ui.graphics.drawscope.DrawScope).drawIntoCanvas(kotlin.Function1)
  Canvas(modifier = Modifier.fillMaxSize()) {
    val path = Path().apply{}
    val paint = Paint()
    paint.blendMode = BlendMode.SrcOut
    drawIntoCanvas {
        it.drawRect(
            rect = Rect(offset = Offset(0f, 0f), size = Size(screenWidth, screenHeight)),
            paint = paint
        )
    }
  }
  ```

# 使用`foundation.Canvas`的注意事项
- 对于透明显示为黑色的: 添加 `.graphicsLayer { alpha = 0.99f }`

# 混色 `BlendMode`
[链接](https://developer.android.com/reference/android/graphics/BlendMode)
