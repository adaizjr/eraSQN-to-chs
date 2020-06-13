# @PRINT_MIDASHINAMI

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色仪表指示

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L1020-L1121)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_state.md)</sup>

**调用**：

+ `@COND`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/cond.md)</sup>

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@PRINT_ACCESSORY`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/print_accessory.md)</sup>

+ `@TEXTS`<sup>[说明文件](/Wiki/erasqn_wiki/function/t/texts.md)</sup>

### 函数实现

#### 参数

+ ARG

#### 返回值

+ 当`CFLAG:ARG:368`的值为`0`时，返回`0`

+ 当关闭了仪表显示时，返回`0`

+ 函数正常结束时，返回`0`

#### 功能实现

**L1021**：

声明变量`LCOUNT`

**L1022**：

当`CFLAG:ARG:368`的值为`0`时：

  + 返回`0`

**L1024-L1028**：

如果`ARG`的值为`MASTER`时：

  + 调用`@DRAWLINES, "□ 仪表 □", "仪表"`，输出仪表信息区块的标题分割线

否则：

  + 调用`@DRAWLINES, "□ 仪表指示 □", "仪表指示"`，输出仪表信息区块的标题分割线

**L1030-L1031**：

当`@CONFIG("項目：身嗜み")`的返回值不为`0`时：

  + 返回`0`

**L1033-L1040**：

以`@COND("身嗜み：陰毛", ARG)`的返回值作为选择支：

  + 当其值为`3`时：

    + 输出`・陰毛を常にツルツルに保つ`

  + 当其值为`5`时：

    + 输出`・陰毛を常に整える`

  + 当其值为`7`

    + 输出`・陰毛を常に整える`

**L1042-L1047**：

以`@COND("身嗜み：腋毛", ARG)`的返回值作为选择支：

  + 根据其值不同：

    + 输出不同的腋毛描述

**L1049-L1058**：

以`@COND("身嗜み：Ｖ拡張", ARG)`的返回值作为选择支：

  + 根据其值不同：

    + 输出不同的V扩张指令描述

**L1060-L1069**：

以`@COND("身嗜み：Ａ拡張", ARG)`的返回值作为选择支：

  + 根据其值不同：

    + 输出不同的A扩张指令描述

**L1071-L1078**：

以`@COND("身嗜み：Ａ準備", ARG)`的返回值作为选择支：

  + 根据其值不同：

    + 输出不同的A准备指令描述

**L1080-L1083**：

以`@COND("身嗜み：Ｐ準備", ARG)`的返回值作为选择支：

  + 根据其值不同：

    + 输出不同的P准备指令描述

**L1085-L1088**：

以`@COND("身嗜み：Ｖ準備", ARG)`的返回值作为选择支：

  + 根据其值不同：

    + 输出不同的V准备指令描述

**L1090-L1093**：

以`@COND("身嗜み：服装", ARG)`的返回值作为选择支：

  + 根据其值不同：

    + 输出不同的着装指令描述

**L1095-L1098**：

以`@COND("身嗜み：尿道拡張", ARG)`的返回值作为选择支：

  + 根据其值不同：

    + 输出不同的尿道扩张指令描述

**L1100-L1121**：

以`@COND("身嗜み：性行為の制限", ARG)`的返回值作为选择支：

  + 根据其值不同：

    + 输出不同的性行为限制指令描述
