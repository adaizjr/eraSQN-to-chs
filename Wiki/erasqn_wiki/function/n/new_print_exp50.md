# @NEW_PRINT_EXP50

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色经历的异常验值

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L1594-L1735)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_.md)</sup>

**调用**：

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DEF_COLOR`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/def_color.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@EXP_GAIN`<sup>[说明文件](/Wiki/erasqn_wiki/function/e/exp_gain.md)</sup>

+ `@PALAM_NUM`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/palam_num.md)</sup>

+ `@STRLENS_FIX`<sup>[说明文件](/Wiki/erasqn_wiki/function/s/strlens.md)</sup>

+ `@TEXT_RJ`<sup>[说明文件](/Wiki/erasqn_wiki/function/t/text_rj.md)</sup>

### 函数实现

#### 参数

+ ARG

#### 返回值

+ 当关闭了异常经验值显示时，返回`0`

+ 角色没有异常经验，返回`0`

#### 功能实现

**L1594-L1596**：

声明变量`LCOUNT`和`MEMO_STR`

**L1598-L1599**：

当角色的异常经验值`EXP:ARG:异常经验`为`0`时：

  + 返回`0`

**L1600-L1601**：

将`LOCALS`的值置为`□ 异常经验:{EXP:ARG:异常经验, 2} □`

调用`@DRAWLINES, LOCALS, "异常经验"`，输出经异常验信息区块的标题分割线

**L1603-L1604**：

当玩家关闭了异常经验信息区块`@CONFIG("項目：異常経験")`的显示时：

  + 返回`0`

**L1606-L1607**：

将变量`MEMO_STR`置为`0`

调用引擎命令`VARSET`，将`LOCALS`置空值

**L1609-L1634**：

如果`@GETBITS(CFLAG:ARG:11, 0, 19)`返回不为`0`时：<br/>（这段的翻译不是十分确定，因为有很多FLAG我都没有触发过）

+ 将`LOCALS`置为空值

+ 当`CFLAG:ARG:11`的第`0`个二进制位的值为`1`时：

  + 将`超大`追加赋值给`LOCALS`

+ 当`CFLAG:ARG:11`的第`1`个二进制位的值为`1`时：

  + 将`震动棒`追加赋值给`LOCALS`

+ 当`CFLAG:ARG:11`的第`8`个二进制位的值为`1`时：

  + 将`触手`追加赋值给`LOCALS`

+ 当`CFLAG:ARG:11`的第`2`个二进制位的值为`1`时：

  + 将`３Ｐ`追加赋值给`LOCALS`

+ 当`CFLAG:ARG:11`的第`3`个二进制位的值为`1`时：

  + 将`%LOCALS%%TEXTS("助手の名称")%的假阴茎`追加赋值给`LOCALS`

+ 如果`CFLAG:ARG:11`的第`3`、`4`或`5`个二进制位的值其中任意一个为`1`时：

  + 将`に跨って`追加赋值给`LOCALS`

+ 否则当`CFLAG:ARG:11`的第`5`个二进制位为`1`时：

  + 将`騎乗位で`追加赋值给`LOCALS`

将`处女丧失`追加赋值给`LOCALS`

当`CFLAG:ARG:11`的第`7`个二进制位为`1`时：

+ 将`(摄影)`追加赋值给`LOCALS`

将`[%LOCALS%]`赋值给`LOCALS`（加方括号）

**L1635-L1636**：

当`CFLAG:ARG:11`的第`20`个二进制位为`1`时：

+ 将`[尽管是童贞但有Ａ性交经验]`赋值给`LOCALS:1`

**L1637-L1648**：

如果`CFLAG:ARG:11`的第`32`个二进制位为`1`时：

  + 当`CFLAG:ARG:11`的第`30`或`31`个二进制位为`1`时：

    + 将`处女`追加赋值给`LOCALS:2`

  + 当`CFLAG:ARG:11`的第`30`和`31`个二进制位都为`1`时：

    + 将`、`追加赋值给`LOCALS:2`

  + 当`CFLAG:ARG:11`的第`31`个二进制位都为`1`时：

    + 将`童贞`追加赋值给`LOCALS:2`

  + 将`之前`追加赋值给`LOCALS:2`

将`[在丧失%LOCALS:2%丧失Ａ处女]`复制给`LOCALS:2`

**L1650-L1667**：

当`CFLAG:ARG:12`的第`0`个二进制位都为`1`时：

  + 将`[公开自慰]`赋值给`LOCALS:3`

当`CFLAG:ARG:12`的第`1`个二进制位都为`1`时：

  + 将`[野外全裸]`赋值给`LOCALS:4`

当`CFLAG:ARG:12`的第`2`个二进制位都为`1`时：

  + 将`[公开剃毛]`赋值给`LOCALS:5`

当`CFLAG:ARG:12`的第`3`个二进制位都为`1`时：

  + 将`[公开放尿]`赋值给`LOCALS:6`

当`CFLAG:ARG:12`的第`4`个二进制位都为`1`时：

  + 将`[性器穿环]`赋值给`LOCALS:7`

当`CFLAG:ARG:12`的第`5`个二进制位都为`1`时：

  + 根据不同的情况将`[野外录影]`或`[野外排泄]`赋值给`LOCALS:8`

当`CFLAG:ARG:12`的第`8`个二进制位都为`1`时：

  + 将`[肛交侍奉]`赋值给`LOCALS:9`

当`CFLAG:ARG:12`的第`9`个二进制位都为`1`时：

  + 将`[打扫口交(Ａ)]`赋值给`LOCALS:10`

当`CFLAG:ARG:12`的第`10`个二进制位都为`1`时：

  + 将`[二穴插入]`赋值给`LOCALS:11`

**L1669-L1675**：


如果`CFLAG:ARG:12`的第`11`或`12`个二进制位为`1`时：

  + 当`CFLAG:ARG:12`的第`11`个二进制位为`1`时：

    + 将`Ｖ`追加赋值给`LOCALS:12`

  + 当`CFLAG:ARG:12`的第`12`个二进制位为`1`时：

    + 将`Ａ`追加赋值给`LOCALS:12`

  + 将`[%LOCALS:12%扩张]`赋值给`LOCALS:12`

**L1677-L1680**：

当`CFLAG:ARG:12`的第`13`个二进制位为`1`时：

  + 将`[拳交]`赋值给`LOCALS:13`

当`CFLAG:ARG:12`的第`14`个二进制位为`1`时：

  + 将`[龙奸]`赋值给`LOCALS:14`

**L1682-L1686**：

当`CFLAG:ARG:12`的第`16`个二进制位为`1`时：

  + 将`[五重绝顶]`赋值给`LOCALS:15`

当`CFLAG:ARG:12`的第`15`个二进制位为`1`时：

  + 将`[四重绝顶]`赋值给`LOCALS:15`

**L1688-L1693**：

当`CFLAG:ARG:12`的第`17`个二进制位为`1`时：

  + 将`[子宫绝顶]`赋值给`LOCALS:17`

当`CFLAG:ARG:12`的第`18`个二进制位为`1`时：

  + 将`[肛门性交]`赋值给`LOCALS:18`<br/>（翻译不确定，别处没有出现此词汇）

当`CFLAG:ARG:12`的第`19`个二进制位为`1`时：

  + 将`[ミニマムいらず]`赋值给`LOCALS:19`<br/>（翻译不确定，别处没有出现此词汇）

**L1696-L1721**：

当`CFLAG:ARG:12`的第`21`个二进制位为`1`时：

  + 将`[针刺]`赋值给`LOCALS:20`

当`CFLAG:ARG:12`的第`22`个二进制位为`1`时：

  + 将`[难耐的痛苦]`赋值给`LOCALS:21`

当`CFLAG:ARG:12`的第`23`个二进制位为`1`时：

  + 将`[意料之外的妊娠]`赋值给`LOCALS:22`

当`CFLAG:ARG:12`的第`24`个二进制位为`1`时：

  + 将`[触手]`赋值给`LOCALS:23`

当`CFLAG:ARG:12`的第`25`个二进制位为`1`时：

  + 将`[扶她化]`赋值给`LOCALS:24`

当`CFLAG:ARG:12`的第`26`个二进制位为`1`时：

  + 将`[喷乳]`赋值给`LOCALS:25`

当`CFLAG:ARG:12`的第`27`个二进制位为`1`时：

  + 将`[梦魔化]`赋值给`LOCALS:26`

当`CFLAG:ARG:12`的第`28`个二进制位为`1`时：

  + 将`[性转换]`赋值给`LOCALS:27`

当`CFLAG:ARG:12`的第`29`个二进制位为`1`时：

  + 将`[化蝶之梦]`赋值给`LOCALS:28`

当`CFLAG:ARG:12`的第`30`个二进制位为`1`时：

  + 将`[子宫插入]`赋值给`LOCALS:29`

当`CFLAG:ARG:12`的第`31`个二进制位为`1`时：

  + 将`[ニプルファック（乳头性交？）]`赋值给`LOCALS:30`<br/>（翻译不确定）

当`CFLAG:ARG:12`的第`32`个二进制位为`1`时：

  + 将`[尿道扩张]`赋值给`LOCALS:31`

当`CFLAG:ARG:12`的第`33`个二进制位为`1`时：

  + 将`[尿道处女丧失]`赋值给`LOCALS:32`

**L1723-L1733**：

以`LCOUNT`作为迭代数，迭代`32`次：<br/>（这里原本时循环60次，但实际上只有32个字符串数组被使用，所以这里我改成32次了，不要浪费无谓的CPU时间）

  + 当`LOCALS:LCOUNT`的字符长度为`0`时：

    + 立即进入下次循环

  + `MEMO_STR`的值在现有的基础上加上`LOCALS:LCOUNT`的字符长度

  + 如果`MEMO_STR`大于`@NUM("折り返し文字数")`的返回值时：

    + 输出一个换行符

    + 将`MEMO_STR`的值置为`LOCALS:LCOUNT`的字符长度

  + 输出`LOCALS:LCOUNT`所储存的字符串

**L1735**：

返回`0`
