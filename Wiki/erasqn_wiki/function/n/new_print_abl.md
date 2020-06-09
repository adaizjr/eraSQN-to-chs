# @NEW_PRINT_ABL

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色拥有的能力

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L1742-L1929)

### 调用关系

**被调用**：

+ `@ABLUP_MASTER`<sup>[说明文件](/Wiki/erasqn_wiki/function/a/ablup_master.md)</sup>

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_state.md)</sup>

**调用**：

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DEF_COLOR`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/def_color.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@TEXT_RJ`<sup>[说明文件](/Wiki/erasqn_wiki/function/t/text_rj.md)</sup>

### 函数实现

#### 参数

+ ARG

#### 返回值

+ 当关闭了能力显示时，返回`0`

+ 函数正常结束时，返回`0`

#### 功能实现

**L1743-L1744**：

声明变量`LCOUNT`和`NOABL`

**L1746**：

调用`@DRAWLINES, "□ 能力 □", "能力"`，输出经验信息区块的标题分割线

**L1748-L1749**：

当`@CONFIG("項目：能力")`的返回值不为`0`时：

  + 返回`0`

**L1761-L1923**：

以`LCOUNT`为迭代数，FOR循环`29`次：

  + 调用引擎命令`VARSET`，重置变量`LOCAL`和`LOCALS`

  + 将变量`NOABL`置为`0`

  + 以`LCOUNT`的值作为选择支：

    + 根据`LCOUNT`的值不同，将`LOCAL`设为不同的值<br/>（设置各个能力的显示顺序）

    + 当要显示`Ｃ`、`Ｖ`、`Ａ`、`Ｂ`和`Ｍ`几个部位的能力时，需要检查对应部位的`特殊能力`以及是`钝感`还是`敏感`并将能力描述储存到`LOCALS`之中

    + 当显示仅女性才能具备的能力时，还需要检查角色是否为`TALENT:ARG:男性`，如果是则需要将`NOABL`置为`1`

    + （男性的`尿道扩张`，`CASE 28`需要确认，男性应该是不能进行尿道扩张的，但原本的程序却未关闭显示。注释说了`現時点ではペニスの尿道は無し…やっぱあり`。这里我暂且先将它的显示关闭）


  + 以传入的参数`ARG`作为选择支：

    + 当其值为`MASTER`时：

      + 以`LCOUNT`为选择支：

        + 将`2`以及`12～29`项能的`NOABL`置为`1`<br/>（MASTER不显示这些能力）

  + 将`%ABLNAME:LOCAL%%LOCALS%`赋值给`LOCALS`<br/>（利用引擎提供的变量查找能力名，并在其后加上能力描述）

  + 以`NOABL`作为选择支：

    + 当其值为`0`时：

      + <del>这里原本还有一个选择支判断，但是被注释了其中一个分支，剩下的两个选择支的输出是一样的，且条件包含了所有情况，导致这个选择支失去了意义，我将其注释掉了</del>

      + 以`13`个字符宽度右对齐的方式打印出能力名称及描述，接着输出能力的数值

    + 否则：

      + 调用引擎命令`SETCOLOR`，将显示颜色设置为`灰色`

      + 以`13`个字符宽度右对齐的方式打印出能力名称及描述，接着输出` ----`代替数值

  + 调用引擎命令`RESETCOLOR`，重置输出颜色

  + 当`LCOUNT + 1`对`4`取模的值为`0`时：<br/>（每输出4项就换行）

    + 输出一个换行符

**L1926-L1927**：

当`LCOUNT + 1`对`4`取模的值不为`0`时：<br/>（确保信息区块输出完成后还会再输出一个换行符）

  + 输出一个换行符

**L1929**：

返回`0`
