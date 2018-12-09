>JSR 223中规范了在Java虚拟机上运行的脚本语言与Java程序之间的交互方式。JSR 233是JavaSE6的一部分，在Java表中API中的包是javax.script。 

**下面根据实践来说一下调用动态语言脚本具体做什么：**
假如有这种情况：需要判断一个变量`a`的大小，但是`判断规则`是不确定的，可能是 `a < 1`，也可能是 `a > 1`、`a == 1` 等等。

* 下面是不调用动态脚本实现:
```java
public boolean compare(double a, String expression) {
  int n = Integer.parseInt(expression.replaceAll("\\D", ""));
  if(expression.contains(">=")) {
    return a >= n;
  } else if(expression.contains("<=")) {
    return a < n;
  } else if(expression.contains("==")) {
    return a == n;
  } else if(expression.contains(">")) {
    return a > n;
  } else {
    ...
  }
}
```
实现起来比较麻烦，就是一堆判断。但是对于 `a < 1 && a > 0` 这种复杂的表达式实现起来更加吃力。

* 下面是调用js脚本实现:
```java
public boolean compare(double a, String expression) throws Exception{
  expression = expression.replace("a", a)
  ScriptEngineManager sem = new ScriptEngineManager();
  ScriptEngine scriptEngine = sem.getEngineByName("js");
  return scriptEngine.eval(expression);
}
```
通过这种方式实现起来非常简单，而且可以应对复杂的表达式。

### 下面是执行`js`脚本与`lua`脚本的对比:
* 执行`js`脚本

 测试代码
```java
        int size = 10000;
        ScriptEngineManager sem = new ScriptEngineManager();
        ScriptEngine scriptEngine = sem.getEngineByName("js");
        long start = System.currentTimeMillis();
        for (int i = 0; i < size; i++) {
            String jsStr = String.format("%d > %d", i, i+1);
            try{
                scriptEngine.eval(jsStr);
            }catch (Exception e) {
                e.printStackTrace();
            }
        }
        long end = System.currentTimeMillis();
        System.out.printf("js：%d ms\n" ,end - start);
```
* 执行`lua`脚本
> 需要第三方库`Luaj`的支持

Luaj是基于lua 5.2.x版本的lua解释器，其中考虑了以下目标：
- 以Java为中心的lua vm实现，旨在利用标准Java功能。
- 轻量级，高性能的lua执行。
- 可以在JME，JSE或JEE环境中运行的多平台。
- 用于集成到实际项目中的完整库和工具集。
- 由于对vm和库功能进行了充分的单元测试，因此可靠。


 测试代码
```java
        int size = 100000;

        Globals globals = JsePlatform.standardGlobals();
        long start = System.currentTimeMillis();
        for (int i = 0; i < size; i++) {
            String luaStr = String.format("return %d > %d", i, i+1);
            LuaValue chunk = globals.load(luaStr);
            chunk.call().toboolean();
        }
        long end = System.currentTimeMillis();
        System.out.printf("lua：%d ms\n", end - start);
```

### 平均执行时长
`lua`：900 ms
`javascript`：60000 ms
lua脚本的执行效率大大高于js脚本的执行效率。
