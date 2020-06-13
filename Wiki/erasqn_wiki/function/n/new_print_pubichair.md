# @NEW_PRINT_PUBICHAIR

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色阴毛腋毛的状态

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L2425-L2471)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_state.md)</sup>

**调用**：

+ `@CEVENTS`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/cevents.md)</sup>

+ `@COND`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/cond.md)</sup>

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@PALAM_NUM`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/palam_num.md)</sup>

+ `@TEXTS`<sup>[说明文件](/Wiki/erasqn_wiki/function/t/texts.md)</sup>

### 函数实现

#### 参数

+ ARG

#### 返回值

+ 当阴毛状态不适用时，返回`0`

+ 当关闭了毛发显示时，返回`0`

+ 函数正常结束时，返回`0`

#### 功能实现

**L2426-L2427**：

当没有设定阴毛和腋毛的状态`@CONFIG("陰毛と腋毛")`，或角色为男性`TALENT:ARG:男性`且不为伪娘`@COND("男の娘", ARG)`时：

  + 返回`0`

**L2428-L2432**：

如果设置了腋毛`CONFIG("腋毛")`：

  + 将`□ 阴毛和%TEXTS("腋")%毛的状态 □`赋值给`LOCALS`

否则：

  +将`□ 阴毛的状态 □`赋值给`LOCALS`

**L2433**：

调用`@DRAWLINES, LOCALS, "阴毛的状态"`，输出经毛发信息区块的标题分割线

**L2433-L2436**：

当玩家关闭了毛发信息区块`@CONFIG("項目：陰毛")`的显示时：

  + 返回`0`

**L2438-L2451**：

如果没有设定阴毛状态`@COND("阴毛", ARG)`：

  + 输出` ----------`

否则：

  + 如果`@CONFIG("腋毛")`返回`1`则输出`阴毛：`否则什么都不输出，接着输出`@CONDS("阴毛", ARG)`

  + 如果`@CONDS("阴毛", ARG)`的返回值为`お手入れ済`，且`@CEVENTS("陰毛の名称", ARG)`的返回值为空值：

    + 如果`@CEVENTS("陰毛の形", ARG)`的返回值为`HEARTMARK`：

      + 输出`(`

      + 调用`HEARTMARK`，输出一个心型符号

      + 输出`@CEVENTS("陰毛の名称", ARG)`的返回值和`)`

    + 否则：

      + 如果`@CEVENTS("陰毛の形", ARG)`返回值的字符长度大于`1`时，输出`@CEVENTS("陰毛の形", ARG)`的返回值，否则输出`@CEVENTS("陰毛の名称", ARG)`的返回值

**L2452-L2459**：

以`@COND("身嗜み：陰毛", ARG)`的返回值作为选择支：

  + 当其值为`3`时：

    + 如果`ARG`的值为MASTER时：打印`ツルツルに剃る主義`，否则打印`ツルツルに剃るようにお願い中`

  + 当其值为`5`时：

    + 如果`ARG`的值为MASTER时：打印`形を綺麗に保つ主義`，否则打印`形を綺麗に保つようにお願い中`

  + 当其值为`7`时：

    + 如果`ARG`的值为MASTER时：打印`剃らない主義`，否则打印`剃らないようにお願い中`

**L2461-L2462**：

当`@CONFIG("腋毛")`的返回值为`0`时：<br/>（没有打开腋毛设定时）

  + 返回`0`

**L2464**：

打印腋毛的描述`%TEXTS("腋")%毛：%CONDS("腋毛", ARG)%`

**L2464-L2471**：

以`@COND("身嗜み：腋毛", ARG)`的返回值作为选择支：

  + 当其值为`3`时：

    + 如果`ARG`的值为MASTER时：打印`ツルツルに剃る主義`，否则打印`ツルツルに剃るようにお願い中`

  + 当其值为`7`时：

    + 如果`ARG`的值为MASTER时：打印`剃らない主義`，否则打印`剃らないようにお願い中`

**L2471**：

返回`0`
