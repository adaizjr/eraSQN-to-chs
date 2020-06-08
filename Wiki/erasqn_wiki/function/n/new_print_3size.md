# @NEW_PRINT_3SIZE

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 根据传入的参数，以不同的方式打印角色的三围

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L1285-L1358)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_state.md)</sup>

+ `@PRINT_NUM_NAME`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/print_num_name.md)</sup>

**调用**：

+ `@COND`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/cond.md)</sup>

+ `@CONDS`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/conds.md)</sup>

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@TEXT_RJ`<sup>[说明文件](/Wiki/erasqn_wiki/function/t/text_rj.md)</sup>

### 函数实现

#### 参数

+ ARG

+ ARGS

#### 返回值

+ 当关闭了三围信息显示时，返回`0`

#### 功能实现

**L1286-L1287**：

当玩家关闭了三围信息显示`@CONFIG("３サイズ：表示") == 0`时：

  + 返回`0`

**L1289-L1325**：

（因此选择支内容较多，所以下面会将说明拆分）

以传入的参数`ARGS`作为选择支：

  + 当其值为`一覧表示`时：<br/>（在角色列表显示三围，而非显示单人详情时）

**L1290-L1293**：

如果角色的`BASE:ARG:身高`为`0`或（角色为`TALENT:ARG:男性`且不为伪娘`@COND("男の娘", ARG) == 0`）时：

  + 返回`0`

**L1294-L1298**：

如果玩家具有素质`TALENT:ARG:拉弥亚`时：

 + 输出带追加要素的身高`BASE:ARG:身高 + BASE:ARG:身高的追加要素`

否则：

  + 直接输出身高`BASE:ARG:身高`

**L1300-L1301**：

调用`@CONDS("バストカップ", ARG)`返回角色的罩杯并存放到`LOCALS`中

输出角色的`@COND("胸围", ARG)`胸围、`LOCALS`罩杯、`BASE:ARG:腰围`腰围、`BASE:ARG:臀围`臀围

**L1304-L1316**：

如果角色为`TALENT:ARG:男性`：

  + 输出臀围等级描述`(--)`

否则如果角色素质`TALENT:ARG:大臀`大于或等于`3`时：

  + 输出臀围等级描述`(超)`

否则如果角色素质`TALENT:ARG:大臀`等于`2`时：

  + 输出臀围等级描述`(爆)`

否则如果角色素质`TALENT:ARG:大臀`大于`0`时：

  + 输出臀围等级描述`(巨)`

否则如果角色素质`TALENT:ARG:小臀`大于`0`时：

  + 输出臀围等级描述`(小)`

否则：

  + 输出臀围等级描述`(普通)`

**L1318-L1324**：

如果设定了`@CONFIG("陰毛と腋毛")`：

  + 如果角色的`BASE:ARG:阴毛`为`0`时：

    + 打印`----------`

  + 否则：

    + 打印`@CONDS("阴毛", ARG)`阴毛的描述

**L1325**：

打印`@CONDS("体型", ARG)`体型的描述

**L1327-L1358**：

（呼应*L1289-L1325*）

（因此选择支内容较多，所以下面会将说明拆分）

以传入的参数`ARGS`作为选择支：

  + 当其值为`個別表示`时：<br/>（在显示单人详情时显示三围）

**L1328-L1329**：

如果角色的`BASE:ARG:身高`为`0`或（角色为`TALENT:ARG:男性`且不为伪娘`@COND("男の娘", ARG) == 0`）时：

  + 返回`0`

**L1330-L1331**：

调用`@CONDS("体型", ARG)`查询角色的体型描述，并将描述存到变量`LOCALS`之中

调用`@DRAWLINES, LOCALS, "体型"`，输出体型信息区块的标题分割线

**L1333-L1334**：

当`@CONFIG("項目：体型")`（查询`FLAG:3`的第5个二进制位）的返回不为`0`时，返回`0`

**L1336-L1340**：

如果玩家具有素质`TALENT:ARG:拉弥亚`时：

 + 输出带追加要素的身高`BASE:ARG:身高 + BASE:ARG:身高的追加要素`

否则：

  + 直接输出身高`BASE:ARG:身高`

**L1341**：

输出角色的`@COND("胸围", ARG)`胸围、`LOCALS`罩杯、`BASE:ARG:腰围`腰围、`BASE:ARG:臀围`臀围

**L1344-L1356**：

如果角色为`TALENT:ARG:男性`：

  + 什么都不做

否则如果角色素质`TALENT:ARG:大臀`大于或等于`3`时：

  + 输出臀围等级描述`(超)`

否则如果角色素质`TALENT:ARG:大臀`等于`2`时：

  + 输出臀围等级描述`(爆)`

否则如果角色素质`TALENT:ARG:大臀`大于`0`时：

  + 输出臀围等级描述`(巨)`

否则如果角色素质`TALENT:ARG:小臀`大于`0`时：

  + 输出臀围等级描述`(小)`

否则：

  + 输出臀围等级描述`(普通)`
