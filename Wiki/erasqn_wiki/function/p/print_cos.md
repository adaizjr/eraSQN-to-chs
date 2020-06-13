# @PRINT_COS

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色服装详细

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L1132-L1282)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_state.md)</sup>

**调用**：

+ `@BRA`<sup>[说明文件](/Wiki/erasqn_wiki/function/b/bra.md)</sup>

+ `@BODYS`<sup>[说明文件](/Wiki/erasqn_wiki/function/b/bodys.md)</sup>

+ `@CEVENTS`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/cevents.md)</sup>

+ `@CHECK_BODYS`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/check_bodys.md)</sup>

+ `@CHECK_CLO`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/check_clo.md)</sup>

+ `@CHECK_OUTER`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/check_outer.md)</sup>

+ `@CHECK_PANTIES`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/check_panties.md)</sup>

+ `@CHECK_SHIRT`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/check_shirt.md)</sup>

+ `@COND`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/cond.md)</sup>

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DEF_COLOR`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/def_color.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@GLOVE`<sup>[说明文件](/Wiki/erasqn_wiki/function/g/glove.md)</sup>

+ `@OUTER`<sup>[说明文件](/Wiki/erasqn_wiki/function/o/outer.md)</sup>

+ `@PANTIES`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/panties.md)</sup>

+ `@PENIS`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/penis.md)</sup>

+ `@PRINT_ACCESSORY`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/print_accessory.md)</sup>

+ `@SHIRT`<sup>[说明文件](/Wiki/erasqn_wiki/function/s/shirt.md)</sup>

+ `@SOCKS`<sup>[说明文件](/Wiki/erasqn_wiki/function/s/socks.md)</sup>

+ `@TEXTS`<sup>[说明文件](/Wiki/erasqn_wiki/function/t/texts.md)</sup>

### 函数实现

#### 参数

+ ARG

#### 返回值

+ 当`ARG`的值为`MASTER`时，返回`0`

+ 当关闭了服装详细显示时，返回`0`

#### 功能实现

**L1133**：

声明变量`LCOUNT`

**L1134-L1135**：

当`ARG`的值为`MASTER`时：

  + 返回`0`

**L1137**：

调用`@DRAWLINES, "□ 服装详细 □", "服装详细"`，输出服装详细区块的标题分割线

**L1139-L1140**：

当`@CONFIG("項目：服装詳細")`的返回值不为`0`时：

  + 返回`0`

**L1142-L1143**：

当角色穿着了上衣`EQUIP:ARG:上衣`时：

  + 当`@CHECK_SHIRT("スカート着用", ARG)`返回`1`且`EQUIP:ARG:裙子`为`0`时，打印衣装的名称`%SHIRT(ARG)%（没穿裙子）`，否则只打印衣装的名称`%SHIRT(ARG)%`

**L1144-L1156**：

如果角色穿着了连体衣`EQUIP:ARG:连体衣`：

  + 打印衣装的名称`@BODYS(ARG)`

  + 如果衣装带拉链`@CHECK_BODYS("ファスナー", ARG)`：

    + 打印`(拉链)`

  + 如果衣装露出VA`@CHECK_BODYS("ＶＡ露出", ARG)`：

    + 打印`(二穴露出)`

  + 如果衣装露出A`@CHECK_BODYS("Ａ露出", ARG)`：

    + 打印`(Ａ穴露出)`

  + 如果衣装露出V`CHECK_BODYS("Ｖ露出", ARG)`：

    + 打印`(Ｖ穴露出)`

**L1157-L1158**：

当角色穿着了胸罩`EQUIP:ARG:胸罩`时：

  + 打印`Ｅ：[%BRA(ARG)%]`

**L1159-L1173**：

如果角色穿着了外套`EQUIP:ARG:外套`：

  + 打印衣装的名称`@OUTER(ARG)`

  + 如果衣装带拉链`@CHECK_OUTER("ファスナー", ARG)`：

    + 打印`(拉链)`

  + 如果衣装开衩`@CHECK_OUTER("スリット", ARG)`：

    + 打印`(开衩)`

  + 如果衣装露出VA`@CHECK_OUTER("ＶＡ露出", ARG)`：

    + 打印`(二穴露出)`

  + 如果衣装露出A`@CHECK_OUTER("Ａ露出", ARG)`：

    + 打印`(Ａ穴露出)`

  + 如果衣装露出V`CHECK_OUTER("Ｖ露出", ARG)`：

    + 打印`(Ｖ穴露出)`

**L1159-L1173**：

如果角色穿着了胖次`EQUIP:ARG:胖次`：

  + 打印衣装的名称`@PANTIES(ARG)`

  + 如果衣装带拉链`@CHECK_PANTIES("ファスナー", ARG)`：

    + 打印`(拉链)`

  + 如果衣装露出VA`@CHECK_PANTIES("ＶＡ露出", ARG)`：

    + 打印`(二穴露出)`

  + 如果衣装露出A`@CHECK_PANTIES("Ａ露出", ARG)`：

    + 打印`(Ａ穴露出)`

  + 如果衣装露出V`CHECK_PANTIES("Ｖ露出", ARG)`：

    + 打印`(Ｖ穴露出)`

**L1187-L1193**：

当角色穿着了袜子`EQUIP:ARG:袜子`时：

  + 打印`Ｅ：[%SOCKS(ARG)%]`

当角色穿着了鞋子`EQUIP:ARG:鞋子`时：

  + 打印`Ｅ：[%SHOES(ARG)%]`

当角色穿着了手套`EQUIP:ARG:手套`时：

  + 打印`Ｅ：[%GLOVE(ARG)%]`

**L1193-L1199**：

如果角色穿着了`EQUIP:ARG:配饰`时：

  + 调用引擎命令`SPLIT`，将`CSTR:ARG:49`以`/`分割，结果存到`LOCALS`

  + 以`LCOUNT`作为迭代数，FOR循环`4`次：

    + 当`LOCALS:LCOUNT`的值不为空值时：

      + 打印`Ｅ：[%LOCALS:LCOUNT%]`

**L1200-L1208**：

如果角色`TALENT:ARG:阴蒂穿环`值不为`0`时：

  + 当角色有阴茎`@PENIS(TARGET)`，就输出`阴茎穿环`，否则输出`阴蒂穿环`

  + 如果查询穿环件形状`@CEVENTS("クリピアス", ARG)`的返回不为空时：

    + 调用引擎命令`SETCOLOR`，将输出颜色设为`黄色`

    + 输出`@CEVENTS("クリピアス", ARG)`穿环件的形状

    + 调用引擎命令`RESETCOLOR`将输出颜色重置为默认值

**L1209-L1217**：

如果角色`TALENT:ARG:阴唇穿环`值不为`0`时：

  + 输出`阴唇穿环`

  + 如果查询穿环件形状`@CEVENTS("ラビアピアス", ARG)`的返回不为空时：

    + 调用引擎命令`SETCOLOR`，将输出颜色设为`黄色`

    + 输出`@CEVENTS("ラビアピアス", ARG)`穿环件的形状

    + 调用引擎命令`RESETCOLOR`将输出颜色重置为默认值

**L1218-L1226**：

如果角色`TALENT:ARG:乳头穿环`值不为`0`时：

  + 输出`乳头穿环`

  + 如果查询穿环件形状`@CEVENTS("ニプルピアス", ARG)`的返回不为空时：

    + 调用引擎命令`SETCOLOR`，将输出颜色设为`黄色`

    + 输出`@CEVENTS("ニプルピアス", ARG)`穿环件的形状

    + 调用引擎命令`RESETCOLOR`将输出颜色重置为默认值

**L1227-L1235**：

如果角色`TALENT:ARG:肚脐穿环`值不为`0`时：

  + 输出`肚脐穿环`

  + 如果查询穿环件形状`@CEVENTS("へそピアス", ARG)`的返回不为空时：

    + 调用引擎命令`SETCOLOR`，将输出颜色设为`黄色`

    + 输出`@CEVENTS("へそピアス", ARG)`穿环件的形状

    + 调用引擎命令`RESETCOLOR`将输出颜色重置为默认值

**L1262-L1279**：

将`LOCALS`置为空值

如果角色全裸`@CHECK_CLO("ハダカ", ARG)`时：

  + 将`全裸`复制给`LOCALS`

否则：

  + 如果`@CHECK_CLO("ボトムレス", ARG)`返回值不为`0`时：

    + 将`下半身全裸`复制给`LOCALS`

  + 否则如果`@CHECK_CLO("トップレス", ARG)`返回值不为`0`时：

    + 如果角色为`TALENT:ARG:男性`时：

      + 将`上半身露出`复制给`LOCALS`

    + 否则：

      + 将`胸部露出`复制给`LOCALS`

否则如果`@CHECK_CLO("Ｖ露出", ARG)`、`@CHECK_CLO("Ａ露出", ARG)`和`@CHECK_CLO("乳首露出", ARG)`返回均不为`0`时：

  + 将`重要部位露出`复制给`LOCALS`

否则如果`@CHECK_CLO("ノーパン", ARG)`不为`0`时：

  + 将`不穿内裤`复制给`LOCALS`

**L1281-L1282**：

当`LOCALS`的字符长度不为`0`时：

  + 输出`备注：%LOCALS%`
