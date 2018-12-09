---
layout: default
---

### 1. 字符串
### 字符串分割为集合
```xml
<#assgin objList = "1,3,4"?split(",")>
```
### JSON转对象
```xml
<#assgin abc="{\"name\":\"小明\"}"?eval>
```

### 2. 数字
### 保留小数位
```
${size?string('#.##')}
```
### 3. 集合
### 获取集合长度
```
<#assgin size = objList?size>
```
### 遍历集合时获取索引
```xml
<#list objList as item>
  ${item?if_exists}
  ${item_index} # 当前索引
</#list>
```
### 固定长度集合
```xml
<#list 1..10 as item>
  ...
</#list>
```
### 4. 日期
### 时间戳转日期
```
${date?number_to_datetime}
```
### 日期格式化
```
${date?datetime} # 日期时间
${date?date} # 日期
${date?time} # 时间
${date?string("yyyy")} # 自定义
```

### 5. 其他

### 判空
```xml
# 输出判空
${name?if_exists}

# if中判空
<#if objList??>
  ...
</#if>
```
