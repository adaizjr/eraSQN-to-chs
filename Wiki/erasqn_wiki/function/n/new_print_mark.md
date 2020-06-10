# @NEW_PRINT_MARK

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色的刻印

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L1933-L1985)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_state.md)</sup>

**调用**：

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@PRINT_BAR`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/print_bar.md)</sup>

### 函数实现

#### 参数

+ ARG

#### 返回值

+ 当查询MASTER，且无人拥有`主人屈服刻印`，或主人为`TALENT:ARG:男性`时，返回`0`

+ 当关闭了刻印显示时，返回`0`

+ 函数正常结束时，返回`0`

#### 功能实现

**L1934-L1936**：

声明变量`LCOUNT`和`NEXT_LINE`

**L1746**：

以参数`ARG`作为选择支：

  + 当其值为`MASTER`时：<br/>（暂时不清楚为什么要这样处理，需要调试）

    + 调用引擎命令`FINDCHARA`查找是否存在拥有刻印`MARK:主人屈服刻印`的角色，如果有：

      + 当主人拥有刻印`MARK:淫纹`，或为`TALENT:ARG:男性`时：

        + 返回`0`

    + 调用`@DRAWLINES, "□ 刻印 □", "刻印"`，输出宝珠信息区块的标题分割线

    + 当`@CONFIG("項目：刻印")`的返回值不为`0`时：

      + 返回`0`

    + 将`NEXT_LINE`的值置为`0`

    + 以`LCOUNT`作为迭代数，FOR循环`CHARANUM`次（从`2`开始，跳过MASTER）：

      + 当角色号为`LCOUNT`的角色没有`MARK:LCOUNT:主人屈服刻印`时：

        + 立即进入下次循环

      + 打印出`MARK:LCOUNT:主人屈服刻印`等级、角色号`LCOUNT`以及以角色名字`CALLNAME:LCOUNT`

      + `NEXT_LINE`自增`1`

      + 当`NEXT_LINE`对`2`取模的值为`0`时：

        + 输出一个换行符

    + 输出结束后，当`NEXT_LINE`对`2`取模的值不为`0`时：<br/>（输出最后一行不满2个项目）

      + 输出一个换行符

  + 否则：

    + 调用`@DRAWLINES, "□ 刻印 □", "刻印"`，输出宝珠信息区块的标题分割线

    + 当`@CONFIG("項目：刻印")`的返回值不为`0`时：

      + 返回`0`

    + 以`LCOUNT`作为迭代数，FOR循环`4`次：

      + 输出刻印`MARKNAME:LCOUNT`的前`2`个字符、刻印的等级`MARK:ARG:LCOUNT`

      + 调用`@PRINT_BAR, "黄色ゲージ", MARK:ARG:LCOUNT, 3, 3`以进度条的形式，输出刻印的经验值

      + 输出一个用于分割不通刻印项目的全角空格

**L1980-L1983**：

如果角色拥有`MARK:ARG:淫纹`，且不为`TALENT:ARG:男性`时：

  + 输出`MARK:ARG:淫纹`的等级

  + 调用`@PRINT_BAR, "桃色ゲージ", MARK:ARG:淫纹, 3, 3`以进度条的形式，输出刻印的经验值

**L1985**：

返回`0`
