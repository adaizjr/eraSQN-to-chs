# @NEW_PRINT_JUEL

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色拥有的宝珠

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L1440-L1500)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_state.md)</sup>

**调用**：

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@PALAM_NUM`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/palam_num.md)</sup>

### 函数实现

#### 参数

+ ARG

#### 返回值

+ 当`MASTER`作为参数传入时，返回`0`

+ 函数正常结束时，返回`0`

#### 功能实现

**L1441-L1443**：

声明变量`LCOUNT`、`NEXT_LINE`

**L1450-L1451**：

当参数`ARG`的值为`MASTER`时：

  + 返回`0`

**L1453**：

调用`@DRAWLINES, "□ 宝珠 □", "宝珠"`，输出宝珠信息区块的标题分割线

**L1455**：

当`@CONFIG("項目：宝珠")`的返回值不为`0`时：

  + 返回`0`

**L1450**：

将`NEXT_LINE`置为`0`

**L1459-L1495**：

以`LCOUNT`作为迭代数，FOR循环`12`次：

  + 以`LCOUNT`作为选择支：

    + 根据`LCOUNT`的变化设置`LOCAL`的值<br/>（主要用于设定输出列表的宝珠项目顺序）

    + 在第`12`项，当角色`JUEL:ARG:反感`数为`0`时，则不会显示

  + 输出宝珠名称`PALAMNAME:LOCAL`以及宝珠数量`@PALAM_NUM(JUEL:ARG:LOCAL)`

  + 每输出一项`NEXT_LINE`就自增`1`

  + 当`NEXT_LINE`对`6`取模的值为`0`时：<br/>（每输出6项就换行）

    + 输出一个换行符

**L1497-L1498**：

输出结束后，当`NEXT_LINE`对`6`取模的值不为`0`时：<br/>（输出最后一行不满6个项目）

  + 输出一个换行符

**L1500**：

返回`0`
