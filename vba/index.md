# VBA


为毛线日本人这么喜欢 Excel，去他娘的 VBA。

<!--more-->

## 单元格样式

设置Excel中的一个或多个单元格甚至是一个区域的或者是被选中单元格的左对齐、友对齐、居中对齐、字体、字号、字型等属性。

①左对齐、右对齐、居中对齐

```vb
'选择区域或单元格右对齐　　
Selection.HorizontalAlignment = Excel.xlRight

'选择区域或单元格左对齐
Selection.HorizontalAlignment = Excel.xlLeft

'选择区域或单元格居中对齐　　
Selection.HorizontalAlignment = Excel.xlCenter

'固定区域的对齐方式的代码：
Range("A1:A9").HorizontalAlignment = Excel.xlLeft
```

②字体、字号、字型

```vb
'当前单元格字体为粗体
Selection.Font.Bold = True

'当前单元格字体为斜体
Selection.Font.Italic = True

'当前单元格字体为宋体20号字
With Selection.Font
	.Name = "宋体"
	.Size = 20
End With
```



　

