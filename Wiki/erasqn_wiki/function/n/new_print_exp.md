# @NEW_PRINT_EXP

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色拥有的经验值

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L1503-L1591)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/func_template.md)</sup>

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

+ 当关闭了经验值显示时，返回`0`

+ 函数正常结束时，返回`0`

#### 功能实现

**L1441-L1443**：

声明变量`LCOUNT`、`LCOUNT2`和`NEXT_LINE`

**L1509**：

调用`@DRAWLINES, "□ 经验 □", "经验"`，输出经验信息区块的标题分割线

**L1511-L1512**：

当`@CONFIG("項目：宝珠")`的返回值不为`0`时：

  + 返回`0`

**L1515-L1537**：

先将`LOCALS`置为空值

然后根据输出顺序，将各个经验名称存到`LOCALS`

当角色为`TALENT:ARG:男性`时：

  + 输出`ＢＬ经验`

否则：

  + 输出`百合经验`

**L1539**：

调用引擎命令`SPLIT`，将`LOCALS`以`/`分割，并储存到`LOCALS`数组中

**L1542-L1548**：

以`LCOUNT`作为迭代数，循环`68`次：<br/>（这里原本时循环100次，但实际上只有68个经验，所以这里我改成68次了，不要浪费无谓的CPU时间）

  + 以`LCOUNT2`作为迭代数，循环`7`次：

    + 调用引擎明日`SUBSTRING`检查`LOCALS:LCOUNT`的第一个全角字符是否为`　`（全角空格），当其不为全角空格时，跳出本循环

    + 将`LOCALS:LCOUNT`的值设为`SUBSTRING(LOCALS:LCOUNT, 2, -1)`，以去除字符串前面第一个全角字符<br/>因为上面的判断会在第一个字符不为全角空格时跳出本循环，所以就保证了不会误删有意义的字符<br/>给`SUBSTRING`传入小于`0`的参数，代表的是倒数第X位<br/>所以当此语句每被执行一次，`LOCALS:LCOUNT`储存的第1个全角空格都会被去掉

**L1550**：

将`NEXT_LINE`置为`0`

**L1551-L1586**：

以`LCOUNT`作为迭代数，循环`100`次：

  + 调用引擎命令`GETNUM`获取对应标号`GETNUM(EXP, LOCALS:LCOUNT)`的EXP数值，并将数值赋值给`LOCAL`

  + 如果`LOCAL`的值为`0`时：

    + 直接跳出循环

  + 否则如果`EXP:ARG:LOCAL`大于或等于`1`时：

    + 如果`STRLENS(EXPNAME:LOCAL)`返回技能名称长度大于或等于`14`：<br/>（此处的`STRLENS`对应的是日语的`SHIFT-JIS`编码，有些中文字符会有长度计算不准的问题，我已替换为`STRLENSU`，以Unicode标准返回字符长度，函数名为`@STRLENS_FIX`）

      + 调用引擎命令`SUBSTRING`截取技能名中的第1～倒数第4位，并调用`@TEXT_RJ`将其以`13`个字符宽度右对齐输出

    + 否则：

      + 直接调用`@TEXT_RJ`以`13`个字符位宽度，右对齐输出`EXPNAME:LOCAL`

    + 当`@COND("調教中")`和`@EXP_GAIN(LOCAL, ARG)`的返回值都大于`0`时：

      + 调用引擎命令`SETCOLOR`将输出颜色设为`黄色`

    + 以经验数值`EXP:ARG:LOCAL`作为选择支：

      + 当其值大于或等于`100,000,000`时：

        + 将其值除以`1,000,000`再加上后缀`M`（百万）再输出，以字符长度为`4`的宽度输出

      + 当其值大于或等于`100,000`时：

        + 将其值除以`1,000`再加上后缀`K`（千）再输出，以字符长度为`4`的宽度输出

      + 否则：

        + 直接输出数值，以字符长度为`5`的宽度输出（上面两个都多出一个后缀）

  + 否则如果`@CONFIG("経験表示詰め")`的返回值不为`0`时：<br/>（设置了不显示未获得的经验值）

    + 立即进入下次循环

  + 否则：

    + 输出`？？？？？？:　　0`

  + 让`NEXT_LINE`自增`1`

  + 当`NEXT_LINE`对`4`取模的值为`0`时：<br/>（每输出4项就换行）

    + 输出一个换行符

**L1588-L1589**：

当`NEXT_LINE`对`4`取模的值不为`0`时：<br/>（确保信息区块输出完成后还会再输出一个换行符）

  + 输出一个换行符

**L1591**：

返回`0`
