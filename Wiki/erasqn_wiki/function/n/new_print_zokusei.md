# @NEW_PRINT_ZOKUSEI

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 根据传入的参数，以不同的格式输出角色的性癖、弱点、以及属性信息

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L1285-L1358)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_.md)</sup>

**调用**：

+ `@COND`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/cond.md)</sup>

+ `@CONDS`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/conds.md)</sup>

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DEF_COLOR`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/def_color.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@NAMES`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/names.md)</sup>

+ `@NUM`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/num.md)</sup>

+ `@NUM_BIT`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/num_bit.md)</sup>

+ `@TEXT_RJ`<sup>[说明文件](/Wiki/erasqn_wiki/function/t/text_rj.md)</sup>

### 函数实现

#### 参数

+ ARG

+ ARG:1

#### 返回值

+ 当关闭了属性信息显示时，返回`0`

#### 功能实现

**L1362**：

声明变量`LCOUNT`

**L1364**：

调用引擎命令`VARSET`重置变量`LOCAL`

**L1365-L1409**：

以参数`ARG`的值作为选择支：

  + 当其值为`MASTER`时：

    + 如果角色`TALENT:MASTER:性癖`不为`0`：

      + 调用`@DRAWLINES, "□ 性癖 □", "性癖"`，输出性癖信息区块的标题分割线

        + 如果`@CONFIG("項目：性癖")`的返回值为`0`<br/>（打开了性癖显示？）

          + 以`LCOUNT`为迭代数，迭代`@NUM("属性")`次：

            + 当`GETBIT(TALENT:MASTER:性癖, LCOUNT)`的值为`0`时

              + 立即进入下次循环

            + 将`@NAMES("属性", LCOUNT)`和返回值赋值给`LOCALS`

            + `LOCAL`的值在原基础上加上`STRLENS(LOCALS)`

            + 如果`LOCAL`的值大于`@NUM("折り返し文字数")`时：

              + 输出一个换行符

              + 将`LOCAL`的值置为`STRLENS(LOCALS)`

            + 输出`LOCALS`储存的字符串

          + 输出一个换行符

    + 如果角色`TALENT:MASTER:弱点`不为`0`：

      + 调用`@DRAWLINES, "□ 弱点 □", "弱点"`，输出弱点信息区块的标题分割线

      + 如果`@CONFIG("項目：弱点")`返回为`0`：

        + 如果`@NUM_BIT(TALENT:MASTER:弱点)`的返回值和`NUM("弱点")`的返回值相同：

          + 输出`全部弱点`

        + 否则

          + 以`LCOUNT`为迭代数，FOR循环`@NUM("弱点")`次：

            + 当`GETBIT(TALENT:MASTER:弱点, LCOUNT)`的值为`0`时：

              + 立即进入下次循环

            + 将`@NAMES("弱点", LCOUNT)`和返回值赋值给`LOCALS`

            + `LOCAL`的值在原基础上加上`STRLENS(LOCALS)`

            + 如果`LOCAL`的值大于`@NUM("折り返し文字数")`时：

              + 输出一个换行符

              + 将`LOCAL`的值置为`STRLENS(LOCALS)`

            + 输出`LOCALS`储存的字符串

          + 输出一个换行符

**L1413-L1414**：

当角色的`BASE:ARG:属性`值为`0`时：

  + 返回`0`

**L1446-L1418**：

调用`DRAWLINES, "□ 属性 □", "属性"`，输出属性信息区块的标题分割线

当`@CONFIG("項目：属性")`返回不为`0`时：

  + 返回`0`

**L1421**：

调用引擎命令`VARSET`重置变量`LOCAL`

**L1422-L1436**：

+ 以`LCOUNT`为迭代数，FOR循环`@NUM("属性")`次：

  + 当`GETBIT(TALENT:MASTER:属性, LCOUNT)`的值为`0`时：

    + 立即进入下次循环

  + 当`GETBIT(TALENT:MASTER:性癖, LCOUNT)`的值不为`0`时：

    + 调用引擎命令`SETCOLOR`，将文字输出颜色改成黄色`@DEF_COLOR("イエロー")`

  + 将`@NAMES("属性", LCOUNT)`的返回值赋值给`LOCALS`

  + `LOCAL`的值在原基础上加上`STRLENS(LOCALS)`

  + 如果`LOCAL`的值大于`@NUM("折り返し文字数")`时：

    + 输出一个换行符

    + 将`LOCAL`的值置为`STRLENS(LOCALS)`

  + 输出`LOCALS`储存的字符串
