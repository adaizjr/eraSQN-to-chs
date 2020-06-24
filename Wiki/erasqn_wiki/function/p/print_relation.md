# @PRINT_RELATION

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色相性

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L2323-L2423)

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

+ ARGS

#### 返回值

+

+ 当关闭了相性显示时，返回`0`

+ 函数正常结束返回`0`

#### 功能实现

> `RELATION:NUM1:NUM2`应该是指1号和2号角色的相性
> 参考链接`https://wiki.eragames.rip/index.php/Emuera/eramavar`
> （注意：这不是官方的Wiki，应该是英语区爱好者的一个网站，里面可以找到很多英译的eragame）

**L2324-L2326**：

声明变量`LCOUNT`和`NEXT_LINE`

**L2330**：

（作用不明，过后研究）

（根据原本程序注释，是在设置这个角色跟其所属的种族之间的相性）

在角色CSV文件`相性`字段与`120`中找出最大值，并赋值给角色的相性`RELATION:ARG:(NO:ARG)`

**L2332**：

调用引擎命令`VARSET`，将`LOCAL`置为空值

**L2335-L2359**：

以`LCOUNT`作为迭代数，FOR循环100次：

  + 以`ARGS`的值作为选择支：

    + 其值为`种族`时：

      + 当`LCOUNT`的值与`NO:ARG && COND("ユニーク", ARG)`的值相等时：

        + 立即执行下次循环

      + 以当前第`ARG`号角色和第`LCOUNT`号角色的`RELATION`作为选择支：

        + 当其值为`0`或`81～119`时：

          + 立即执行下次循环

    + 否则：

      + 当`LCOUNT`的值为`ARG`时：

        + 立即执行下次循环

      + 当`LCOUNT`的值大于或等于当前角色总数`CHARANUM`时：

        + 立即跳出循环

      + 以`RELATION:ARG:(NO:LCOUNT)`的值为选择支：

        + 当其值为`0`或`81～119`时：

          + 立即执行下次循环

  + 将`LOCAL`的值置为`1`

  + 立即跳出循环

**L2423**：

函数正常结束，返回`0`
