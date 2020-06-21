# @SHOW_FAMILY

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色的家族构成

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L2215-L2321)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_state.md)</sup>

**调用**：

+ `@COND`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/cond.md)</sup>

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@TEXT_LJ`<sup>[说明文件](/Wiki/erasqn_wiki/function/t/text_lj.md)</sup>

### 函数实现

#### 参数

+ ARG

#### 返回值

+ 当关闭了家族构成显示时，返回`0`

+ 函数正常结束时，返回`0`

#### 功能实现

**L2216-L2221**：

声明变量`LCOUNT`、`MOTHER`、`FATHER`、`FATHER_CHILD`、`MOTHERS`和`FATHERS`

**L2223-L2225**：

将角色的母亲角色号`@COND("母亲", ARG)`复制给`MOTHER`

将角色的父亲角色号`@COND("父亲", ARG)`复制给`FATHER`

将角色的胎儿的父亲角色号`@COND("胎儿的父亲", ARG)`复制给`FATHER_CHILD`

**L2227**：

调用引擎命令`VARSET`，将变量`LOCAL`置为空值


**L2228-L2229**：

当角色具有`TALENT:ARG:生产经历`，或有`MOTHER`，或有`FATHER`，或为一或多人父亲时`@COND("子持ち：父親", ARG)`时：

  + 调用`@DRAWLINES, "□ 家族构成 □", "家族构成"`，输出家族构成区块的标题分割线

**L2231-L2232**：

当`@CONFIG("項目：家族構成")`的返回值不为`0`时：

  + 返回`0`

**L2235-L2248**：

如果角色的母亲`MOTHER`或父亲`FATHER`大于`0`时：

  + 当角色的母亲`MOTHER`大于`0`时：

    + 如果`MOTHER`的值不为`MASTER`则让将`[{MOTHER}]%CALLNAME:MOTHER%`赋值给`MOTHERS`（母亲的角色编号和名字）；否则（当MOTHER为MASTER时），将`%CALLNAME:MOTHER%`赋值给`MOTHERS`（不显示MASTER的角色编号）


  + 当角色的父亲`FATHER`大于`0`时：

    + 如果`FATHER`的值不为`MASTER`则让将`[{FATHER}]%CALLNAME:FATHER%`赋值给`FATHERS`（父亲的角色编号和名字）；否则（当FATHER为MASTER时），将`%CALLNAME:FATHER%`赋值给`FATHERS`（不显示MASTER的角色编号）

  + 如果角色的父亲`FATHER`和母亲`MOTHER`都大于`0`时：

    + 输出`这个孩子是%FATHERS%和%MOTHERS%的第{BASE:ARG:第几号}个孩子`

  + 否则如果角色的父亲`FATHER`大于`0`时：

    + 输出`这个孩子是%FATHERS%的孩子`

  + 否则如果角色的母亲`MOTHER`大于`0`时：

    + 输出`这个孩子是%MOTHERS%的第{BASE:ARG:第几号}个孩子`

**L2250-L2295**：

如果角色拥有`TALENT:ARG:生产经历`：

  + 输出`生产经验：上次出产的是`

  + 以`FATHER_CHILD`的值作为选择支：

    + 当其值大于`0`时：

      + 当`FATHER_CHILD`的值不为`MASTER`时：

        + 输出`FATHER_CHILD`的编号

      + 输出是谁的孩子`%CALLNAME:FATHER_CHILD%的孩子，`

    + 当其值为`-1`时：

      + 输出`被卖掉的梦魔的孩子，`

    + 当其值为`-2`时：

      + 输出`米兰达的娼妇的孩子，`

    + 当其值为`-3`时：

      + 输出`龙的孩子，`

    + 当其值为`-4`时：

      + 输出`父亲不明的孩子，`

    + 当其值为`-5`时：

      + 输出`异形触手的孩子，`

  + 输出`到目前为止已经出产了{TALENT:ARG:生产经历}个孩子`

  + 以`LCOUNT`为迭代数，FOR循环`CHARANUM`次：

    + 当角色的母亲`@COND("母亲", LCOUNT)`不为`ARG`时：

      + 立即进入下次循环

    + 输出第`LCOUNT`号角色时当前角色的第几个孩子`BASE:LCOUNT:第几号`、角色编号以及孩子的名字`CALLNAME:LCOUNT`

    + 用`LOCAL`记录该角色的父亲`@COND("父亲", LCOUNT)`角色编号

    + 以`LOCAL`的值作为选择支：

      + 当其值大于`0`时：

        + 当`LOCAL`的值不为`MASTER`时：

          + 输出`LOCAL`的编号

        + 输出角色父亲的姓名`CALLNAME:LOCAL`

      + 当其值为`-1`时：

        + 输出`行踪不明`

      + 当其值为`-2`时：

        + 输出`米兰达的娼妇`

      + 当其值为`-3`时：

        + 输出`龙`

      + 当其值为`-4`时：

        + 输出`不明`

      + 当其值为`-5`时：

        + 输出`触手`

**L2297-L2318**：

如果角色是某些角色的父亲`@COND("子持ち：父親", ARG)`：

  + 如果角色拥有`TALENT:ARG:生产经历`：

    + 输出`还是下列角色的父亲`

  + 否则：

    + 输出`下列角色的父亲`

  + 将`LOCAL`置为`0`

  + 以`LCOUNT`为迭代数，FOR循环`CHARANUM`次：

    + 当角色的母亲`@COND("父亲", LCOUNT)`不为`ARG`时：

      + 立即进入下次循环

    + 输出该角色的角色编号`LCOUNT`以及角色姓名`CALLNAME:LCOUNT`

    + `LOCAL`自增`1`

    + 当`LOCAL`对`3`取模的值为`0`时：<br/>（输出三个角色名后进行换行）

      + 输出一个换行符

  + 当`LOCAL`对`3`取模的值不为`0`时：<br/>（确保最后有一个换行符）

      + 输出一个换行符

**L2318**：

返回`0`
