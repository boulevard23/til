# Get Scala Syntax Tree

```
scala> import scala.reflect.runtime.currentMirror
scala> import scala.tools.reflect.ToolBox
scala> val tb = currentMirror.mkToolBox()
scala> tb.parse("val a = 10")
res0: tb.u.Tree = val a = 10
```