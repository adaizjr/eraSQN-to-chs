# @NEW_PRINT_TALENT

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色的素质

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L1990-L2213)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_state.md)</sup>

**调用**：

+ `@BL`<sup>[说明文件](/Wiki/erasqn_wiki/function/b/bl.md)</sup>

+ `@CEVENT`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/cevent.md)</sup>

+ `@COND`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/cond.md)</sup>

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@CSVTALENT_EX`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/csvtalent_ex.md)</sup>

+ `@DEF_COLOR`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/def_color.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@NUM`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/num.md)</sup>

+ `@PALAM_NUM`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/palam_num.md)</sup>

+ `@PENIS`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/penis.md)</sup>

+ `@STRCOUNTS`<sup>[说明文件](/Wiki/erasqn_wiki/function/s/strcounts.md)</sup>

+ `@TALENT_NAME`<sup>[说明文件](/Wiki/erasqn_wiki/function/t/talent_name.md)</sup>

+ `@TEXTS`<sup>[说明文件](/Wiki/erasqn_wiki/function/t/texts.md)</sup>

### 函数实现

#### 参数

+ ARG

#### 返回值

+ 函数正常结束时，返回`0`

#### 功能实现

**L1991-L2006**：

声明变量`LCOUNT`、`LCOUNT2`、`MEMO_STR`、`TALENT_TYPE`、`TALENT_TYPES`、`IGNORE_COLOR`、字符串数组`PRINT_TALENTS`、`TALENT_FIX`以及`TALENT_RMV`

**L2008-L2059**：

如果参数`ARG`不为`MASTER`，且目前在制作角色中`@COND("キャラメイク中")`，且`@STRCOUNTS(CSTR:MASTER:10, "固定：", "除外：")`返回不为`0`时：<br/>（最后一个条件作用不明，过后研究）<br/>（这段代码的作用是在创建角色时，将玩家指定的素质不同的颜色输出到信息区块标题的后方）

  + 输出`□ 素质 □`

  + 以变量`MEMO_STR`记录`STRLENS("□ 素质 □ ")`的字符长度

  + 调用引擎明日`VARSET`重置变量`LOCALS`

  + 调用`@TEXTS("固定可能な素質")`并将其返回的字符串以`/`分割，储存到`LOCALS`中

  + 如果`STRCOUNT(CSTR:MASTER:10, "固定：")`的字符长度不为`0`：

    + 调用引擎命令`SETCOLOR`，将输出颜色置为`绿色`

    + 输出`固定：`的提示

    + `MEMO_STR`自增`6`（加上上面输出的提示的长度）

    + 以`LCOUNT`作为迭代数，FOR循环`100`次：

      + 当`LOCALS:LCOUNT`为空值时：

        + 立即跳出当前循环

      + 将`固定：%LOCALS:LCOUNT%`赋值给`TALENT_FIX`

      + 当`@CEVENT(TALENT_FIX, MASTER)`返回`0`时：

        + 立即进入下次循环

      + 打印`[%LOCALS:LCOUNT%]`

      + `MEMO_STR`自增`STRLENS(LOCALS:LCOUNT) + 3`

  + 调用引擎命令`RESETCOLOR`，重置输出颜色

  + 如果`@STRCOUNT(CSTR:MASTER:10, "除外：")`的字符长度大于`0`

    + 调用引擎命令`SETCOLOR`，将输出颜色置为`青`

    + 输出`除外：`的提示

    + `MEMO_STR`自增`6`（加上上面输出的提示的长度）

    + 以`LCOUNT`作为迭代数，FOR循环`100`次：

      + 当`LOCALS:LCOUNT`为空值时：

        + 立即跳出当前循环

      + 将`除外：%LOCALS:LCOUNT%`赋值给`TALENT_FIX`

      + 当`@CEVENT(TALENT_FIX, MASTER)`返回`0`时：

        + 立即进入下次循环

      + 打印`[%LOCALS:LCOUNT%]`

      + `MEMO_STR`自增`STRLENS(LOCALS:LCOUNT) + 3`

  + 调用引擎命令`RESETCOLOR`，重置输出颜色

  + 以`LCOUNT`作为迭代数，FOR循环`NUM("折り返し文字数") - MEMO_STR`次：

    + 输出`-`

  + 输出一个换行符

否则：

调用`@DRAWLINES, "□ 素质 □", "素质"`，输出宝珠信息区块的标题分割线

**L2061-L2062**：

当`@CONFIG("項目：素质")`的返回值不为`0`时：

  + 返回`0`

**L2064**：

调用引擎明日`VARSET`重置变量`PRINT_TALENTS`

**L2066-L2154**：

以`LCOUNT`作为迭代数，FOR循环`300`次：

  + 当角色的`TALENT:ARG:LCOUNT`为`0`时：

    + 立即进入下次循环

  + 当第LCOUNT号的素质字符长度`STRLENS(TALENTNAME:LCOUNT)`为`0`时：

    + 立即进入下次循环

  + 将`IGNORE_COLOR`置为`0`

  + 以`LCOUNT`作为选择支：

    + 为不同编号的TALENT分配对应的`TALENT_TYPE`

    + 部分TALENT与性别有关，需要执行对应的判断

    + 这里仅列出特殊情况的说明，其余情况清参考源码

    + `CASE 2`：当玩家没有阴茎`@PENIS(ARG) == 0`或游戏全局设定中没有设置`CONFIG("ペニス詳細設定")`时：

      + 立即进入下次循环

    + `CASE 98`：当玩家不为`TALENT:ARG:男性`时：

      + 立即进入下次循环

    + `CASE 138, 139, 141`：当玩家不为`TALENT:ARG:男性`时：

      + 立即进入下次循环

    + `CASE 8`：当玩家为`TALENT:ARG:男性`，或调用`@TALENT_NAME(LCOUNT, TALENT:ARG:LCOUNT, ARG)`无返回时：

      + 立即进入下次循环

    + `CASE 9`：当角色有阴茎时`@PENIS(ARG)`：

      + 立即进入下次循环

    + `CASE 151`：当角色`TALENT:ARG:魔法使`的值大于或等于`2`时：

      + 将`PRINT_TALENTS:4`的值置为`全部`

    + `CASE 197`：将`PRINT_TALENTS:TALENT_TYPE`的值置为`[%TALENT_NAME(LCOUNT, TALENT:ARG:LCOUNT, ARG)%]/%PRINT_TALENTS:TALENT_TYPE%`

  + 当`IGNORE_COLOR`的值为`0`，且`@CSVTALENT_EX(ARG, LCOUNT)`不等于`TALENT:ARG:LCOUNT`时：

    + 将`PRINT_TALENTS:TALENT_TYPE`的值置为`%PRINT_TALENTS:TALENT_TYPE%色変え/`

  + 将`PRINT_TALENTS:TALENT_TYPE`的值置为`%PRINT_TALENTS:TALENT_TYPE%[%TALENT_NAME(LCOUNT, TALENT:ARG:LCOUNT, ARG)%]/`

**L2156-L2211**：

以`LCOUNT2`作为迭代数，FOR循环10次：

  + 当`PRINT_TALENTS:LCOUNT2`的值为空值时：

    + 立即进入下次循环

  + 以`LCOUNT2`的值作为选择支：

    + 根据`LCOUNT2`的值，将`TALENT_TYPES`设为不同的类别标签，如`性别：`、`性格：`和`体质：`等

    + `CASE 4`是特殊情况：

      + 如果`TALENT:ARG:魔法使`的值大于或等于`2`：

        + 打印`魔法：全部`

        + 立即进入下次循环

      + 将`TALENT_TYPES`置为`魔法：`

  + 输出`TALENT_TYPES`的值，并用`MEMO_STR`记录它的字符长度

  + 调用引擎命令`SPLIT`，将`PRINT_TALENTS:LCOUNT2`以`/`分割，将分割结果存到`LOCALS`中

  + 以`LCOUNT`作为迭代数，FOR循环`300`次：

    + 以`LOCALS:LCOUNT`的值作为选择支：

      + 当其值为空值时：

        + 跳出当前循环

      + 当其值为`色変え`时：

        + 调用引擎命令`SETCOLOR`，将输出颜色设为`黄色`

        + 立即进入下次循环

      + `MEMO_STR`的值在现有的基础上加上`LOCALS:LCOUNT`的字符长度

      + 如果`MEMO_STR`的值大于`@NUM("折り返し文字数")`的返回值：

        + 输出一个换行符

        + 输出与`TALENT_TYPES`字符长度相等个数的空格

        + 将`MEMO_STR`的值置为`LOCALS:LCOUNT`的字符长度加`6`（`TALENT_TYPES`的字符长度？）

      + 输出`LOCALS:LCOUNT`

      + 调用引擎命令`RESETCOLOR`将输出颜色重置为默认值

**L2213**：

返回`0`
