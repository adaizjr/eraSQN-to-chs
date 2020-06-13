# @PRINT_EQUIPPING_ACCESSORY

> [\[回Wiki首页\]](/Wiki) [\[回函数列表\]](/Wiki/erasqn_wiki/function/README.md)

### 作用描述

+ 显示角色正在装备的饰品

### 所在文件

+ [New_Print_State.erb](/ERB/SHOP/New_Print_State.erb#L2473-L2484)

### 调用关系

**被调用**：

+ `@NEW_PRINT_STATE`<sup>[说明文件](/Wiki/erasqn_wiki/function/n/new_print_state.md)</sup>

**调用**：

+ `@CONFIG`<sup>[说明文件](/Wiki/erasqn_wiki/function/c/config.md)</sup>

+ `@DRAWLINES`<sup>[说明文件](/Wiki/erasqn_wiki/function/d/drawlines.md)</sup>

+ `@PRINT_ACCESSORY`<sup>[说明文件](/Wiki/erasqn_wiki/function/p/print_accessory.md)</sup>

### 函数实现

#### 参数

+ ARG

#### 返回值

+ 当参数不为`MASTER`，或MASTER没有装备饰品时，返回`0`

+ 当关闭了饰品显示时，返回`0`

+ 函数正常结束时，返回`0`

#### 功能实现

**L2474-L2475**：

当参数`ARG`的值不为`MASTER`，或MASTER没有装备饰品（`FLAG:399`值为`0`）时：

  + 返回`0`

**L1450-L1451**：

当参数`ARG`的值为`MASTER`时：

  + 返回`0`

**L2477**：

调用`@DRAWLINES, "□ 装饰品 □", "装饰品"`，输出宝珠信息区块的标题分割线

**L2479-L2480**：

当`@CONFIG("項目：アクセサリ")`的返回值不为`0`时：

  + 返回`0`

**L2482**：

调用`@PRINT_ACCESSORY, FLAG:399`显示角色所装备的饰品

**L2484**：

返回`0`
