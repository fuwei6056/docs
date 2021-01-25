---
title: 火币USDT本位永续合约 API 文档

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://www.hbg.com/zh-cn/apikey/'>创建 API Key </a>
includes:

search: true
---

# 简介

## USDT本位永续合约API简介

欢迎使用火币USDT本位永续合约 API！ 你可以使用此 API 获得市场行情数据，进行交易，并且管理你的账户。

在文档的右侧是代码示例，目前我们仅提供针对 `shell` 的代码示例。

你可以通过选择上方下拉菜单的版本号来切换文档对应的 API 版本，也可以通过点击右上方的语言按钮来切换文档语言。


## 做市商项目

<aside class="notice">
做市商项目不支持点卡抵扣、VIP、交易量相关活动以及任何形式的返佣活动。
</aside>

欢迎有优秀 maker 策略交易量大的用户参与长期合约做市商项目。如果您的火币交割合约账户中有折合大于 3 BTC 资产，或火币币本位永续合约账户中有折合大于 3 BTC 资产，或火币期权合约账户中有折合大于 3 BTC 资产，或火币USDT本位永续合约账户中有大于 30000 USDT 资产，请提供以下信息到 dm_mm@huobi.com（做市商项目不支持点卡抵扣、VIP、交易量相关活动以及任何形式的返佣活动）:

1. 提供火币 UID （需不存在返佣关系的 UID）；
2. 提供其他交易平台 maker 交易量截图证明（比如30天内成交量，或者 VIP 等级等）；


# 更新日志

## 1.0.7 2021年1月27日 【新增：批量获取聚合行情接口、获取标记价格的 K 线数据、查询用户结算记录（全仓和逐仓）、订阅标记价格 K 线数据（sub）、请求标记价格 K 线数据（req）。7-28 修改接口，新增字段。修改：计划委托订单的订单ID由原本的自然数自增ID 改为长度为 18 位的唯一标识ID。推荐使用下单后返回的 order_id_str（字符串类型的订单 ID），避免发生长度过大而被系统截断的情况。】

### 1、新增批量获取聚合行情接口
 - 接口名称：【通用】批量获取聚合行情
 - 接口类型：公共接口
 - 接口URL：/linear-swap-ex/market/detail/batch_merged

### 2、新增获取标记价格的 K 线数据接口
 - 接口名称：【通用】获取标记价格的 K 线数据
 - 接口类型：公共接口
 - 接口URL：/index/market/history/linear_swap_mark _price_kline

### 3、新增订阅标记价格 K 线数据 WS 接口
 - 接口名称：【通用】订阅标记价格 K 线数据
 - 接口类型：公共接口
 - 订阅地址：market.$contract_code.mark_price.$period

### 4、新增请求标记价格 K 线数据 WS 接口
 - 接口名称：【通用】请求标记价格 K 线数据
 - 接口类型：公共接口
 - 订阅地址：market.$contract_code.mark_price.$period

### 5、新增查询用户结算记录(逐仓)接口
 - 接口名称：【逐仓】查询用户结算记录
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_user_settlement_records

### 6、新增查询用户结算记录(全仓)接口
 - 接口名称：【全仓】查询用户结算记录
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_user_settlement_records

### 7、修改全部撤单(逐仓)接口（请求参数新增 2 个选填字段:direction，表示买卖方向，不填默认撤销全部。参数可选值为“buy”:买，“sell”:卖。offset，表示开平方向，不填默认撤销全部。参数可 选值为“open”:开仓，“close”:平仓。）
 - 接口名称：【逐仓】全部撤单
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cancelall

### 8、修改全部撤单(全仓)接口（请求参数新增 2 个选填字段:direction，表示买卖方向，不填默认撤销全部。参数可选值为“buy”:买，“sell”:卖。offset，表示开平方向，不填默认撤销全部。参数可 选值为“open”:开仓，“close”:平仓。）
 - 接口名称：【全仓】全部撤单
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_cancelall

### 9、修改获取合约订单信息(逐仓)接口（返参data中新增real_profit字段，表示真实收益，类型decimal）
 - 接口名称：【逐仓】获取合约订单信息
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_order_info

### 10、修改获取合约订单信息(全仓)接口（返参data中新增real_profit字段，表示真实收益，类型decimal）
 - 接口名称：【全仓】获取合约订单信息
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_order_info

### 11、修改获取订单明细信息(逐仓)接口（返回参数中的 data 和 trades 下各新增以下字段:real_profit(真实收益)。同时 trades 下新增每笔成交收益字段：profit（平仓盈亏））
 - 接口名称：【逐仓】获取订单明细信息
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_order_detail

### 12、修改获取订单明细信息(全仓)接口（返回参数中的 data 和 trades 下各新增以下字段:real_profit(真实收益)。同时 trades 下新增每笔成交收益字段：profit（平仓盈亏））
 - 接口名称：【全仓】获取订单明细信息
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_order_detail

### 13、修改获取合约当前未成交委托(逐仓)接口（请求参数新增 2 个选填字段:sort_by，表示排序字段，不填默认按创建时间倒序。参数可选值为“created_at”(按照创建时间倒序)，“update_time”(按照更新时间倒 序)。trade_type，表示交易类型，不填默认查询全部。参数可选值为 0:全部,1:买入 开多,2: 卖出开空,3: 买入平空,4: 卖出平多。 返回参数中的 orders 下新增以下字段:update_time(订单更新时间，单位毫秒)、real_profit(真实收益)。）
 - 接口名称：【逐仓】获取合约当前未成交委托
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_openorders

### 14、修改获取合约当前未成交委托(全仓)接口（请求参数新增 2 个选填字段:sort_by，表示排序字段，不填默认按创建时间倒序。参数可选值为“created_at”(按照创建时间倒序)，“update_time”(按照更新时间倒 序)。trade_type，表示交易类型，不填默认查询全部。参数可选值为 0:全部,1:买入 开多,2: 卖出开空,3: 买入平空,4: 卖出平多。 返回参数中的 orders 下新增以下字段:update_time(订单更新时间，单位毫秒)、real_profit(真实收益)。）
 - 接口名称：【全仓】获取合约当前未成交委托
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_openorders

### 15、修改获取合约历史委托(逐仓)接口（返参orders中新增real_profit字段，表示真实收益，类型decimal）
 - 接口名称：【逐仓】获取合约历史委托
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_hisorders

### 16、修改获取合约历史委托(全仓)接口（返参orders中新增real_profit字段，表示真实收益，类型decimal）
 - 接口名称：【全仓】获取合约历史委托
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_hisorders

### 17、修改获取历史成交记录(逐仓)接口（返参trades中新增real_profit字段，表示真实收益，类型decimal）
 - 接口名称：【逐仓】获取历史成交记录
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_matchresults

### 18、修改获取历史成交记录(全仓)接口（返参trades中新增real_profit字段，表示真实收益，类型decimal）
 - 接口名称：【全仓】获取历史成交记录
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_matchresults

### 19、修改订阅订单成交数据(逐仓)接口（返参外层新增real_profit字段，表示真实收益，类型decimal.返参trade中新增：real_profit字段，表示真实收益、profit字段，表示平仓盈亏。）
 - 接口名称：【逐仓】订阅订单成交数据
 - 接口类型：私有接口
 - 订阅地址：orders.$contract_code

### 20、修改订阅订单成交数据(全仓)接口（返参外层新增real_profit字段，表示真实收益，类型decimal.返参trade中新增：real_profit字段，表示真实收益、profit字段，表示平仓盈亏。）
 - 接口名称：【全仓】订阅订单成交数据
 - 接口类型：私有接口
 - 订阅地址：orders_cross.$contract_code

### 21、修改计划委托全部撤单(逐仓)接口（请求参数新增 2 个选填字段:direction，表示买卖方向，不填默认撤销全部。参数可选值为“buy”:买，“sell”:卖。offset，表示开平方向，不填默认撤销全部。参数可 选值为“open”:开仓，“close”:平仓。）
 - 接口名称：【逐仓】计划委托全部撤单
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_trigger_cancelall

### 22、修改计划委托全部撤单(全仓)接口（请求参数新增 2 个选填字段:direction，表示买卖方向，不填默认撤销全部。参数可选值为“buy”:买，“sell”:卖。offset，表示开平方向，不填默认撤销全部。参数可 选值为“open”:开仓，“close”:平仓。）
 - 接口名称：【全仓】计划委托全部撤单
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_trigger_cancelall

### 23、修改止盈止损订单全部撤单(逐仓)接口（请求参数新增选填字段:direction，表示买卖方向，不填默认撤销全部）
 - 接口名称：【逐仓】止盈止损订单全部撤单
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_tpsl_cancelall

### 24、修改止盈止损订单全部撤单(全仓)接口（请求参数新增选填字段:direction，表示买卖方向，不填默认撤销全部）
 - 接口名称：【全仓】止盈止损订单全部撤单
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_tpsl_cancelall

### 25、修改查询计划委托当前委托(逐仓)接口（请求参数新增选填字段:trade_type，表示交易类型，不填默认查询全部。参数可选值为 0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多。）
 - 接口名称：【逐仓】查询计划委托当前委托
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_trigger_openorders

### 26、修改查询计划委托当前委托(全仓)接口（请求参数新增选填字段:trade_type，表示交易类型，不填默认查询全部。参数可选值为 0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多。）
 - 接口名称：【全仓】查询计划委托当前委托
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_trigger_openorders

### 27、修改查询止盈止损订单当前委托(逐仓)接口（请求参数新增选填字段:trade_type，表示交易类型，不填默认查询全部。参数可选值为 0:全部,3: 买入平空,4: 卖出平多。）
 - 接口名称：【逐仓】查询止盈止损订单当前委托
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_tpsl_openorders

### 28、修改查询止盈止损订单当前委托(全仓)接口（请求参数新增选填字段:trade_type，表示交易类型，不填默认查询全部。参数可选值为 0:全部,3: 买入平空,4: 卖出平多。）
 - 接口名称：【全仓】查询止盈止损订单当前委托
 - 接口类型：私有接口
 - 接口URL：/linear-swap-api/v1/swap_cross_tpsl_openorders


## 1.0.6 2021年01月12号 【1 新增获取预估结算价接口。2-13 新增止盈止损订单接口。14-35 修改接口,新增字段。 新增【合约策略订单】一级菜单，将本次新增的双向止盈止损相关接口以及原有的计划委托相关接口挪到该菜单下】

### 1、新增获取预估结算价
 - 接口名称: 【通用】获取预估结算价
 - 接口类型: 公共接口
 - 接口URL: /linear-swap-api/v1/swap_estimated_settlement_price

### 2、新增对仓位设置止盈止损订单(逐仓)
 - 接口名称: 【逐仓】对仓位设置止盈止损订单
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_tpsl_order

### 3、新增对仓位设置止盈止损订单(全仓)
 - 接口名称: 【全仓】对仓位设置止盈止损订单
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_tpsl_order

### 4、新增止盈止损订单撤单接口(逐仓)
 - 接口名称: 【逐仓】止盈止损订单撤单
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_tpsl_cancel

### 5、新增止盈止损订单撤单接口(全仓)
 - 接口名称: 【全仓】止盈止损订单撤单
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_tpsl_cancel

### 6、新增止盈止损订单全部撤单接口(逐仓)
 - 接口名称: 【逐仓】止盈止损订单全部撤单
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_tpsl_cancelall

### 7、新增止盈止损订单全部撤单接口(全仓)
 - 接口名称: 【全仓】止盈止损订单全部撤单
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_tpsl_cancelall

### 8、新增查询止盈止损订单当前委托接口(逐仓)
 - 接口名称: 【逐仓】查询止盈止损订单当前委托
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_tpsl_openorders

### 9、新增查询止盈止损订单当前委托接口(全仓)
 - 接口名称: 【全仓】查询止盈止损订单当前委托
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_tpsl_openorders

### 10、新增查询止盈止损订单历史委托接口(逐仓)
 - 接口名称: 【逐仓】查询止盈止损订单历史委托
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_tpsl_hisorders

### 11、新增查询止盈止损订单历史委托接口(全仓)
 - 接口名称: 【全仓】查询止盈止损订单历史委托
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_tpsl_hisorders

### 12、新增查询开仓单关联的止盈止损订单详情接口(逐仓)
 - 接口名称: 【逐仓】查询开仓单关联的止盈止损订单详情
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_relation_tpsl_order

### 13、新增查询开仓单关联的止盈止损订单详情接口(全仓)
 - 接口名称: 【全仓】查询开仓单关联的止盈止损订单详情
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_relation_tpsl_order

### 14、修改合约下单接口(逐仓)（新增选填入参：tp_trigger_price（止盈触发价格）、tp_order_price（止盈委托价格）、tp_order_price_type（止盈委托类型）、sl_trigger_price（止损触发价格）、sl_order_price（止损委托价格）、sl_order_price_type（止损委托类型）。）
 - 接口名称: 【逐仓】合约下单
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_order

### 15、修改合约下单接口(全仓)（新增选填入参：tp_trigger_price（止盈触发价格）、tp_order_price（止盈委托价格）、tp_order_price_type（止盈委托类型）、sl_trigger_price（止损触发价格）、sl_order_price（止损委托价格）、sl_order_price_type（止损委托类型）。）
 - 接口名称: 【全仓】合约下单
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_order

### 16、修改合约批量下单接口(逐仓)（在入参orders_data中新增选填参数：tp_trigger_price（止盈触发价格）、tp_order_price（止盈委托价格）、tp_order_price_type（止盈委托类型）、sl_trigger_price（止损触发价格）、sl_order_price（止损委托价格）、sl_order_price_type（止损委托类型）。）
 - 接口名称: 【逐仓】合约批量下单
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_batchorder

### 17、修改合约批量下单接口(全仓)（在入参orders_data中新增选填参数：tp_trigger_price（止盈触发价格）、tp_order_price（止盈委托价格）、tp_order_price_type（止盈委托类型）、sl_trigger_price（止损触发价格）、sl_order_price（止损委托价格）、sl_order_price_type（止损委托类型）。）
 - 接口名称: 【全仓】合约批量下单
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_batchorder

### 18、修改获取合约订单信息接口(逐仓)（新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【逐仓】获取合约订单信息
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_order_info

### 19、修改获取合约订单信息接口(全仓)（新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【全仓】获取合约订单信息
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_order_info

### 20、修改获取订单明细信息接口(逐仓)（新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【逐仓】获取订单明细信息	
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_order_detail

### 21、修改获取订单明细信息接口(全仓)（新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【全仓】获取订单明细信息	
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_order_detail

### 22、修改获取合约当前未成交委托接口(逐仓)（新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【逐仓】获取合约当前未成交委托
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_openorders

### 23、修改获取合约当前未成交委托接口(全仓)（新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【全仓】获取合约当前未成交委托
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_openorders

### 24、修改获取合约历史委托接口(逐仓)（新增入参：sort_by(表示：排序字段，可选值为“create_date”，“update_time”)。新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),update_time（表示：订单的更新时间）,在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【逐仓】获取合约历史委托
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_hisorders

### 25、修改获取合约历史委托接口(全仓)（新增入参：sort_by(表示：排序字段，可选值为“create_date”，“update_time”)。新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),update_time（表示：订单的更新时间）,在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【全仓】获取合约历史委托
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_hisorders

### 26、修改订阅订单成交数据接口(逐仓)（新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【逐仓】订阅订单成交数据
 - 接口类型: 私有接口
 - 订阅主题: orders.$contract_code

### 27、修改订阅订单成交数据接口(全仓)（新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【全仓】订阅订单成交数据
 - 接口类型: 私有接口
 - 订阅主题: orders_cross.$contract_code

### 28、修改订阅订单撮合数据接口(逐仓)（新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【逐仓】订阅订单撮合数据	
 - 接口类型: 私有接口
 - 订阅主题: matchOrders.$contract_code

### 29、修改订阅订单撮合数据接口(全仓)（新增返回参数：is_tpsl(表示是否设置止盈止损，1：是；0：否),在返回参数order_source订单来源新增枚举值（tpsl:止盈止损触发））
 - 接口名称: 【全仓】订阅订单撮合数据	
 - 接口类型: 私有接口
 - 订阅主题: matchOrders_cross.$contract_code

### 30、修改获取计划委托历史委托接口(逐仓)（新增入参：sort_by(表示：排序字段，可选值为“create_date”，“update_time”)。新增返回参数：update_time（表示：订单的更新时间））
 - 接口名称: 【逐仓】获取计划委托历史委托	
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_trigger_hisorders

### 31、修改获取计划委托历史委托接口(全仓)（新增入参：sort_by(表示：排序字段，可选值为“create_date”，“update_time”)。新增返回参数：update_time（表示：订单的更新时间））
 - 接口名称: 【全仓】获取计划委托历史委托	
 - 接口类型: 私有接口
 - 接口URL: /linear-swap-api/v1/swap_cross_trigger_hisorders

### 32、修改获取当前可用合约总持仓量（在返回参数data中新增trade_volume：最近24小时成交量（张），trade_amount：最近24小时成交量（币）trade_turnover：最近24小时成交额、这三个字段 ）
 - 接口名称: 【通用】获取当前可用合约总持仓量
 - 接口类型: 公共接口
 - 接口URL: /linear-swap-api/v1/swap_open_interest

### 33、修改订阅Market Detail数据（在返参tick中新增ask表示卖一，bid表示买一。）
 - 接口名称: 【通用】订阅Market Detail数据
 - 接口类型: 公共接口
 - 订阅主题: market.$contract_code.detail

### 34、修改获取合约信息（在返参data下新增delivery_time，表示交割时间（毫秒时间戳））
 - 接口名称: 【通用】获取合约信息
 - 接口类型: 公共接口
 - 接口URL: /linear-swap-api/v1/swap_contract_info

### 35、修改订阅合约信息变动（在返参data下新增delivery_time，表示交割时间（毫秒时间戳））
 - 接口名称: 【通用】订阅合约信息变动
 - 接口类型: 公共接口
 - 订阅主题: public.$contract_code.contract_info


## 1.0.5 2020年12月18日 【新增：订阅系统状态更新推送的 WebSocket 接口】

### 1、新增订阅系统状态更新推送的 WebSocket 接口
  - 接口名称：【通用】订阅系统状态更新
  - 接口类型: 公共接口
  - 订阅主题：public.$service.heartbeat

## 1.0.4 2020年12月11日 【1-33 新增全仓模式接口。34-60 修改接口,新增字段】

### 1、新增全仓模式查询平台阶梯调整系数

  - 接口名称：【全仓】查询平台阶梯调整系数

  - 接口类型：公共接口

  - 接口URL：/linear-swap-api/v1/swap_cross_adjustfactor

### 2、新增全仓模式查询系统划转权限

  - 接口名称：【全仓】查询系统划转权限

  - 接口类型：公共接口

  - 接口URL：/linear-swap-api/v1/swap_cross_transfer_state  

### 3、新增全仓模式查询系统交易权限

  - 接口名称：【全仓】查询系统交易权限

  - 接口类型：公共接口

  - 接口URL：/linear-swap-api/v1/swap_cross_trade_state 

### 4、新增全仓模式获取用户账户信息

  - 接口名称：【全仓】获取用户账户信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_account_info     

### 5、新增全仓模式获取用户持仓信息

  - 接口名称：【全仓】获取用户持仓信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_position_info 

### 6、新增全仓模式查询母账户下所有子账户资产信息

  - 接口名称：【全仓】查询母账户下所有子账户资产信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_sub_account_list  

### 7、新增全仓模式查询单个子账户资产信息

  - 接口名称：【全仓】查询单个子账户资产信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_sub_account_info 

### 8、新增全仓模式查询单个子账户持仓信息

  - 接口名称：【全仓】查询单个子账户持仓信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_sub_position_info   

### 9、新增全仓模式查询用户当前的划转限制

  - 接口名称：【全仓】查询用户当前的划转限制

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_transfer_limit 

### 10、新增全仓模式用户持仓量限制的查询

  - 接口名称：【全仓】用户持仓量限制的查询

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_position_limit

### 11、新增全仓模式获取用户资产和持仓信息

  - 接口名称：【全仓】获取用户资产和持仓信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_account_position_info 

### 12、新增全仓模式查询用户可用杠杆倍数

  - 接口名称：【全仓】查询用户可用杠杆倍数

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_available_level_rate  

### 13、新增全仓模式切换杠杆

  - 接口名称：【全仓】切换杠杆

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_switch_lever_rate  

### 14、新增全仓模式合约下单

  - 接口名称：【全仓】合约下单

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_order  

### 15、新增全仓模式合约批量下单

  - 接口名称：【全仓】合约批量下单

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_batchorder 

### 16、新增全仓模式撤销订单

  - 接口名称：【全仓】撤销订单

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_cancel  

### 17、新增全仓模式全部撤单

  - 接口名称：【全仓】全部撤单

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_cancelall 

### 18、新增全仓模式获取合约订单信息

  - 接口名称：【全仓】获取合约订单信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_order_info  

### 19、新增全仓模式获取订单明细信息

  - 接口名称：【全仓】获取订单明细信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_order_detail  

### 20、新增全仓模式获取合约当前未成交委托

  - 接口名称：【全仓】获取合约当前未成交委托

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_openorders  

### 21、新增全仓模式获取合约历史委托

  - 接口名称：【全仓】获取合约历史委托

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_hisorders 

### 22、新增全仓模式获取历史成交记录

  - 接口名称：【全仓】获取历史成交记录

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_matchresults   

### 23、新增全仓模式闪电平仓下单

  - 接口名称：【全仓】闪电平仓下单

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_lightning_close_position 

### 24、新增全仓模式合约计划委托下单

  - 接口名称：【全仓】合约计划委托下单

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_trigger_order   

### 25、新增全仓模式合约计划委托撤单

  - 接口名称：【全仓】合约计划委托撤单

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_trigger_cancel 

### 26、新增全仓模式合约计划委托全部撤单

  - 接口名称：【全仓】合约计划委托全部撤单

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_trigger_cancelall  

### 27、新增全仓模式获取计划委托当前委托

  - 接口名称：【全仓】获取计划委托当前委托

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_trigger_openorders  

### 28、新增全仓模式获取计划委托历史委托

  - 接口名称：【全仓】获取计划委托历史委托

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_cross_trigger_hisorders 

### 29、新增全仓模式订阅订单成交数据

  - 接口名称：【全仓】订阅订单成交数据

  - 接口类型：私有接口

  - 订阅主题：orders_cross.$contract_code 

### 30、新增全仓模式订阅资产变动数据

  - 接口名称：【全仓】订阅资产变动数据

  - 接口类型：私有接口

  - 订阅主题：accounts_cross.$margin_account  

### 31、新增全仓模式订阅持仓变动更新数据

  - 接口名称：【全仓】订阅持仓变动更新数据

  - 接口类型：私有接口

  - 订阅主题：positions_cross.$contract_code   

### 32、新增全仓模式订阅撮合订单成交数据

  - 接口名称：【全仓】订阅撮合订单成交数据

  - 接口类型：私有接口

  - 订阅主题：matchOrders_cross.$contract_code 

### 33、新增全仓模式订阅计划委托订单变动

  - 接口名称：【全仓】订阅计划委托订单变动

  - 接口类型：私有接口

  - 订阅主题：trigger_order_cross.$contract_code

### 34、查询合约信息接口新增字段（新增入参support_margin_mode；返参data中也新增support_margin_mode字段；表示合约支持的保证金模式）

  - 接口名称：查询合约信息

  - 接口类型：公共接口

  - 接口URL：linear-swap-api/v1/swap_contract_info

### 35、查询平台阶梯调整系数新增返回字段（在返参中新增margin_mode字段：表示保证金模式）

  - 接口名称：查询平台阶梯调整系数

  - 接口类型：公共接口

  - 接口URL：/linear-swap-api/v1/swap_adjustfactor

### 36、查询系统状态接口新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：查询系统状态

  - 接口类型：公共接口

  - 接口URL：/linear-swap-api/v1/swap_api_state

### 37、获取用户账户信息接口新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取用户账户信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_account_info

### 38、查询单个子账户资产信息接口新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：查询单个子账户资产信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_sub_account_info

### 39、查询用户账户和持仓信息新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：查询用户账户和持仓信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_account_position_info

### 40、查询母账户下所有子账户资产信息新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：查询母账户下所有子账户资产信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_sub_account_list

### 41、获取用户持仓信息新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取用户持仓信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_position_info

### 42、获取单个子账户持仓信息新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取单个子账户持仓信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_sub_position_info

### 43、查询财务记录接口新增入参字段（新增入参contract_code：表示合约代码）

  - 接口名称：查询财务记录

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_financial_record

### 44、获取订单明细信息新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取订单明细信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_order_detail

### 45、获取合约当前未成交委托新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取合约当前未成交委托

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_openorders

### 46、获取合约历史委托新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取合约历史委托

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_hisorders

### 47、获取历史成交记录新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取历史成交记录

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_matchresults

### 48、获取计划委托当前委托新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取计划委托当前委托

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_trigger_openorders

### 49、获取计划委托历史委托新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取计划委托历史委托

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_trigger_hisorders

### 50、获取用户合约划转限制新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取用户合约划转限制

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_transfer_limit  

### 51、获取用户合约持仓量限制新增返回字段（在返参中新增margin_mode字段，表示保证金模式）

  - 接口名称：获取用户合约持仓量限制

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_position_limit

### 52、获取用户当前合约杠杆倍数新增返回字段（在返参中新增margin_mode字段，表示保证金模式）

  - 接口名称：获取用户当前合约杠杆倍数

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_available_level_rate  

### 53、切换杠杆新增返回字段（在返参中新增margin_mode字段，表示保证金模式）

  - 接口名称：切换杠杆

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_switch_lever_rate

### 54、订阅订单成交数据新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：订阅订单成交数据

  - 接口类型：私有接口

  - 订阅主题：orders.$contract_code

### 55、订阅撮合订单成交数据新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：订阅撮合订单成交数据

  - 接口类型：私有接口

  - 订阅主题：matchOrders.$contract_code

### 56、订阅计划委托订单更新新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：订阅计划委托订单更新

  - 接口类型：私有接口

  - 订阅主题：trigger_order.$contract_code

### 57、订阅持仓变动数据新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：订阅持仓变动数据

  - 接口类型：私有接口

  - 订阅主题：positions.$contract_code

### 58、订阅资产变动数据新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：订阅资产变动数据

  - 接口类型：私有接口

  - 订阅主题：accounts.$contract_code

### 59、订阅合约信息变动数据新增返回字段（返参中新增support_margin_mode字段，表示合约支持的保证金模式。）

  - 接口名称：订阅合约信息变动数据

  - 接口类型：公共接口

  - 订阅主题：public.$contract_code.contract_info 

### 60、获取合约订单信息新增返回字段（在返参中新增margin_account字段：表示保证金账户；以及margin_mode字段：表示保证金模式）

  - 接口名称：获取合约订单信息

  - 接口类型：私有接口

  - 接口URL：/linear-swap-api/v1/swap_order_info

## 1.0.3 2020年12月2日 【修改获取订单明细信息接口（查询无成交撤单数据时，如果不传“created_at”和“order_type”参数，由原来的只能查询到最近12小时数据，改为只能查询到最近2小时数据）；修改获取合约历史委托接口（查询无成交撤单数据时，由原来的只保留最近24小时数据，改为只保留2小时数据。）】

### 1、修改获取订单明细信息接口（查询无成交撤单数据时，如果不传“created_at”和“order_type”参数，由原来的只能查询到最近12小时数据，改为只能查询到最近2小时数据）

   - 接口名称：获取订单明细信息

   - 接口类型：私有接口

   - 接口URL：linear-swap-api/v1/swap_order_detail

### 2、修改获取合约历史委托接口（查询无成交撤单数据时，由原来的只保留最近24小时数据，改为只保留最近2小时数据。）

   - 接口名称：获取合约历史委托

   - 接口类型：私有接口

   - 接口URL：linear-swap-api/v1/swap_hisorders

## 1.0.2 2020年11月24日 【新增：查询平台历史结算记录；修改：获取强平订单接口新增返参字段，订阅强平订单数据接口新增返参字段】

### 1、新增查询平台历史结算记录接口

  - 接口名称：查询平台历史结算记录
  
  - 接口类型：公共接口
  
  - 接口URL：linear-swap-api/v1/swap_settlement_records

### 2、获取强平订单接口新增返参字段（返回参数中的 orders 参数下增加以下字段:amount 表示强平数量(币);trade_turnover 表示强平金额）

  - 接口名称：获取强平订单接口
  
  - 接口类型：公共接口
  
  - 接口URL：linear-swap-api/v1/swap_liquidation_orders

### 3、订阅强平订单数据接口新增返参字段（返回参数中的 data 参数下增加以下字段:amount 表示强平数量(币);trade_turnover 表示强平金额。）

  - 接口名称：订阅强平订单数据
  
  - 接口类型：公共接口
  
  - 订阅主题：public.$contract_code.liquidation_orders

## 1.0.1 2020年10月29日 【修改：切换杠杆成功时 WS 资产接口推送更新信息，切换杠杆成功时 WS 持仓接口推送更新信息】

### 1、订阅资产接口推送更新（返参event新增事件类型，switch_lever_rate表示切换倍数。在用户切换倍数成功时，需推送一次最新的资产信息，event为switch_lever_rate。）

   - 接口名称：订阅资产变动数据

   - 接口类型：私有接口

   - 订阅主题：accounts.$contract_code

### 2、订阅持仓接口推送更新（返参event新增事件类型，switch_lever_rate表示切换杠杆。在用户切换杠杆倍数成功时，需推送一次最新的持仓信息（若用户持仓量为0，则不会触发推送），event 为 switch_lever_rate。）
   
   - 接口名称：订阅持仓变动数据

   - 接口类型：私有接口

   - 订阅主题：positions.$contract_code

## 1.0.0 2020年10月26日14:00(GMT+8)

# 合约交易接入说明

## 合约交易接口列表

### 接口列表

  权限类型  |    接口数据类型   |  接口模式 | 请求方法      |          类型  |   描述                     |   需要验签  |
----------- |  ------------------ | ------------- |---------------------------------------- |  ---------- |  ------------------------------- |  --------------  |
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_contract_info                             | GET    |      【通用】获取合约信息                        |       否          |
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_index                                     | GET    |      【通用】获取合约指数信息                    |       否          |                     
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_price_limit                               | GET    |      【通用】获取合约最高限价和最低限价          |       否          |           
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_open_interest                             | GET    |      【通用】获取当前可用合约总持仓量            |       否          |            
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_risk_info                                 | GET    |      【通用】查询合约风险准备金和预估分摊比例    |       否          |
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_insurance_fund                            | GET    |      【通用】获取风险准备金历史数据              |       否          |
读取  | 基础信息接口 |  逐仓   | /linear-swap-api/v1/swap_adjustfactor                              | GET    |      【逐仓】查询平台阶梯调整系数                |       否          |
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_his_open_interest                         | GET    |      【通用】获取平台持仓量                      |       否          |
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_elite_account_ratio                       | GET    |      【通用】精英账户多空持仓对比-账户数         |       否          |
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_elite_position_ratio                      | GET    |      【通用】精英账户多空持仓对比-持仓量         |       否          |
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_liquidation_orders                        | GET    |      【通用】获取强平订单                        |       否          |
读取  | 基础信息接口 |  通用   | /linear-swap-api/v1/swap_settlement_records                        | GET    |      【通用】平台历史结算记录                    |       否          |
读取  | 基础信息接口 |  逐仓   | /linear-swap-api/v1/swap_api_state                                 | GET    |      【逐仓】查询系统状态                        |       否          |
读取  | 市场行情接口 |  通用   | /linear-swap-api/v1/swap_funding_rate                              | GET    |      【通用】获取合约的资金费率                  |       否          |
读取  | 市场行情接口 |  通用   | /linear-swap-api/v1/swap_historical_funding_rate                   | GET    |      【通用】获取合约的历史资金费率              |       否          |
读取  | 市场行情接口 |  通用   | /linear-swap-ex/market/depth                                       | GET    |      【通用】获取行情深度数据                    |       否          |
读取  | 市场行情接口 |  通用   | /linear-swap-ex/market/history/kline                               | GET    |      【通用】获取K线数据                         |       否          |
读取  | 市场行情接口 |  通用   | /index/market/history/linear_swap_mark _price_kline               | GET    |      【通用】获取标记价格的 K 线数据                 |  否  |
读取  | 市场行情接口 |  通用   | /linear-swap-ex/market/detail/merged                               | GET    |      【通用】获取聚合行情                        |       否          |
读取  | 市场行情接口 |  通用   | /linear-swap-ex/market/detail/batch_merged                        | GET    |      【通用】批量获取聚合行情                 |  否  |
读取  | 市场行情接口 |  通用   | /index/market/history/linear_swap_basis                            | GET    |      【通用】获取基差数据                        |       否          |
读取  | 市场行情接口 |  通用   | /index/market/history/linear_swap_premium_index_kline              | GET    |      【通用】获取溢价指数K线数据                 |       否          |
读取  | 市场行情接口 |  通用   | /index/market/history/linear_swap_estimated_rate_kline             | GET    |      【通用】获取预测资金费率的K线数据           |       否          |
读取  | 市场行情接口 |  通用   | /linear-swap-ex/market/trade                                       | GET    |      【通用】获取市场最近成交记录                |       否          |
读取  | 市场行情接口 |  通用   | /linear-swap-ex/market/history/trade                               | GET    |      【通用】批量获取最近的交易记录               |     否         |
读取  | 市场行情接口  | 通用  | /linear-swap-api/v1/swap_estimated_settlement_price                 | GET    |     【通用】获取预估结算价      |      否          |
读取  | 基础信息接口 |  全仓    | /linear-swap-api/v1/swap_cross_adjustfactor                          | GET    |     【全仓】查询平台阶梯调整系数                                                |       否          |
读取  | 基础信息接口 |  全仓    | /linear-swap-api/v1/swap_cross_transfer_state                        | GET    |     【全仓】查询系统划转权限                        |       否          |
读取  | 基础信息接口 |  全仓    | /linear-swap-api/v1/swap_cross_trade_state                           | GET    |     【全仓】查询系统交易权限                        |       否          |
读取  | 账户接口    |  逐仓  |  /linear-swap-api/v1/swap_account_info                              | POST   |      【逐仓】获取用户的合约账户信息               |     是         |
读取  | 账户接口    |  逐仓  |  /linear-swap-api/v1/swap_position_info                             | POST   |      【逐仓】获取用户的合约持仓信息               |     是         |
读取  | 账户接口    |  逐仓  |  /linear-swap-api/v1/swap_available_level_rate                      | POST   |      【逐仓】查询用户可用杠杆倍数          |     是         |
读取  | 账户接口    |  逐仓  |  /linear-swap-api/v1/swap_sub_account_list                          | POST   |      【逐仓】查询母账户下所有子账户资产信息       |     是         |
读取  | 账户接口    |  逐仓  |  /linear-swap-api/v1/swap_sub_account_info                          | POST   |      【逐仓】查询母账户下的单个子账户资产信息     |     是         |
读取  | 账户接口    |  逐仓  |  /linear-swap-api/v1/swap_sub_position_info                         | POST   |      【逐仓】查询母账户下的单个子账户持仓信息     |     是         |
读取  | 账户接口    |  通用  |  /linear-swap-api/v1/swap_financial_record                          | POST   |      【通用】查询用户财务记录                     |     是         |
读取  |  账户接口   |   逐仓    |  /linear-swap-api/v1/swap_user_settleme nt_records  |                 POST        |  【逐仓】查询用户结算记录                |  是  |
读取  |  账户接口   |   全仓    |  /linear-swap-api/v1/swap_cross_user_set tlement_records  |                 POST        |  【全仓】查询用户结算记录                |  是  |
读取  | 账户接口    |  通用  |  /linear-swap-api/v1/swap_order_limit                               | POST   |      【通用】获取用户的合约下单量限制             |     是         |
读取  | 账户接口    |  通用  |  /linear-swap-api/v1/swap_fee                                       | POST   |      【通用】获取用户的合约手续费费率             |     是         |
读取  | 账户接口    |  逐仓 |   /linear-swap-api/v1/swap_transfer_limit                            | POST   |      【逐仓】获取用户的合约划转限制               |     是         |
读取  | 账户接口    |  逐仓  |  /linear-swap-api/v1/swap_position_limit                            | POST   |      【逐仓】获取用户的合约持仓量限制             |     是         |
读取  | 账户接口    |  逐仓  |  /linear-swap-api/v1/swap_account_position_info                     | POST   |      【逐仓】获取用户资产和持仓信息               |     是         |
交易  | 账户接口    |  通用  |  /linear-swap-api/v1/swap_master_sub_transfer                       | POST   |      【通用】母子账户划转                         |     是         |
读取  | 账户接口    |  通用  |  /linear-swap-api/v1/swap_master_sub_transfer_record                | POST   |      【通用】获取母账户下的所有母子账户划转记录   |     是         |
交易  | 账户接口    |  通用  |  /linear-swap-api/v1/swap_transfer_inner                            | POST   |      【通用】同账号不同保证金账户的划转           |     是         |
读取  | 账户接口    |  通用  |  /linear-swap-api/v1/swap_api_trading_status                        | GET    |      【通用】获取用户API指标禁用信息              |     是         |
读取  | 账户接口    |  全仓  |  /linear-swap-api/v1/swap_cross_account_info                          | POST    |     【全仓】获取用户的合约账户信息              |       是          |
读取  | 账户接口    |  全仓  |  /linear-swap-api/v1/swap_cross_position_info                         | POST    |     【全仓】获取用户的合约持仓信息               |       是          |
读取  | 账户接口    |  全仓  |  /linear-swap-api/v1/swap_cross_sub_account_list                      | POST    |     【全仓】查询母账户下所有子账户资产信息       |       是          |
读取  | 账户接口    |  全仓  |  /linear-swap-api/v1/swap_cross_sub_account_info                      | POST    |     【全仓】查询母账户下的单个子账户资产信息   |       是          |
读取  | 账户接口    |  全仓  |  /linear-swap-api/v1/swap_cross_sub_position_info                     | POST    |     【全仓】查询母账户下的单个子账户持仓信息    |       是          |
读取  | 账户接口    |  全仓  |  /linear-swap-api/v1/swap_cross_transfer_limit                        | POST    |     【全仓】获取用户的合约划转限制           |       是          |
读取  | 账户接口    |  全仓  |  /linear-swap-api/v1/swap_cross_position_limit                        | POST    |     【全仓】获取用户的合约持仓量限制        |       是          |
读取  | 账户接口    |  全仓  |  /linear-swap-api/v1/swap_cross_account_position_info                 | POST    |     【全仓】获取用户资产和持仓信息          |       是          |
读取  | 账户接口    |  全仓  |  /linear-swap-api/v1/swap_cross_available_level_rate                   | POST    |     【全仓】获取用户当前合约杠杆倍数        |       是          |
交易  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_order                                     | POST   |      【逐仓】合约下单                             |     是         |
交易  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_batchorder                                | POST   |      【逐仓】合约批量下单                         |     是         |
交易  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_switch_lever_rate                         | POST   |      【逐仓】切换杠杆                          |     是         |
交易  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_cancel                                    | POST   |      【逐仓】撤销合约订单                         |     是         |
交易  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_cancelall                                 | POST   |      【逐仓】撤销全部合约单                       |     是         |
读取  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_order_info                                | POST   |      【逐仓】获取用户的合约订单信息               |     是         |
读取  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_order_detail                              | POST   |      【逐仓】获取用户的合约订单明细信息           |     是         |
读取  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_openorders                                | POST   |      【逐仓】获取用户的合约当前未成交委托         |     是         |
读取  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_hisorders                                 | POST   |      【逐仓】获取用户的合约历史委托               |     是         |
读取  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_matchresults                              | POST   |      【逐仓】获取用户的合约历史成交记录           |     是         |
交易  | 交易接口    |  逐仓  |  /linear-swap-api/v1/swap_lightning_close_position                  | POST   |      【逐仓】合约闪电平仓下单                     |     是         |
交易  | 策略接口    |  逐仓  |  /linear-swap-api/v1/swap_trigger_order                             | POST   |      【逐仓】合约计划委托下单                     |     是          |
交易  | 策略接口    |  逐仓  |  /linear-swap-api/v1/swap_trigger_cancel                            | POST   |      【逐仓】合约计划委托撤单                     |     是         |
交易  | 策略接口    |  逐仓  |  /linear-swap-api/v1/swap_trigger_cancelall                         | POST   |      【逐仓】合约计划委托全部撤单                 |     是         |
读取  | 策略接口    |  逐仓  |  /linear-swap-api/v1/swap_trigger_openorders                        | POST   |      【逐仓】获取计划委托当前委托                 |     是         |
读取  | 策略接口    |  逐仓  |  /linear-swap-api/v1/swap_trigger_hisorders                         | POST   |      【逐仓】获取计划委托历史委托                 |     是         |
交易  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_switch_lever_rate                     | POST    |     【全仓】切换杠杆         |       是          |
交易  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_order                                 | POST    |     【全仓】合约下单           |       是          |
交易  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_batchorder                            | POST    |     【全仓】合约批量下单        |       是          |
交易  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_cancel                                | POST    |     【全仓】撤销合约订单        |       是          |
交易  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_cancelall                             | POST    |     【全仓】撤销全部合约单     |       是          |
读取  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_order_info                            | POST    |     【全仓】获取用户的合约订单信息             |       是          |
读取  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_order_detail                          | POST    |     【全仓】获取用户的合约订单明细信息         |       是          |
读取  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_openorders                            | POST    |     【全仓】获取用户的合约当前未成交委托       |       是          |
读取  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_hisorders                             | POST    |     【全仓】获取用户的合约历史委托             |       是          |
读取  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_matchresults                          | POST    |     【全仓】获取用户的合约历史成交记录         |       是          |
交易  | 交易接口    |  全仓  |  /linear-swap-api/v1/swap_cross_lightning_close_position              | POST    |     【全仓】合约闪电平仓下单           |       是          |
交易  | 策略接口    |  全仓  |  /linear-swap-api/v1/swap_cross_trigger_order                         | POST    |     【全仓】合约计划委托下单           |       是          |
交易  | 策略接口    |  全仓  |  /linear-swap-api/v1/swap_cross_trigger_cancel                        | POST    |     【全仓】合约计划委托撤单           |       是          |
交易  | 策略接口    |  全仓  |  /linear-swap-api/v1/swap_cross_trigger_cancelall                     | POST    |     【全仓】合约计划委托全部撤单       |       是          |
读取  | 策略接口    |  全仓  |  /linear-swap-api/v1/swap_cross_trigger_openorders                    | POST    |     【全仓】获取计划委托当前委托       |       是          |
读取  | 策略接口    |  全仓  |  /linear-swap-api/v1/swap_cross_trigger_hisorders                     | POST    |     【全仓】获取计划委托历史委托       |       是          |
交易  | 策略接口  | 逐仓 |  /linear-swap-api/v1/swap_tpsl_order                           | POST    |     【逐仓】对仓位设置止盈止损订单       |       是          |
交易  | 策略接口  | 逐仓 |  /linear-swap-api/v1/swap_tpsl_cancel                           | POST    |    【逐仓】止盈止损订单撤单       |       是          |
交易  | 策略接口  | 逐仓 |  /linear-swap-api/v1/swap_tpsl_cancelall                       | POST    |     【逐仓】止盈止损订单全部撤单       |       是          |
读取  | 策略接口  | 逐仓 |  /linear-swap-api/v1/swap_tpsl_openorders                      | POST    |     【逐仓】止盈止损订单当前委托       |       是          |
读取  | 策略接口  | 逐仓 |  /linear-swap-api/v1/swap_tpsl_hisorders                       | POST    |     【逐仓】止盈止损订单历史委托       |       是          |
读取  | 策略接口  | 逐仓 |  /linear-swap-api/v1/swap_relation_tpsl_order                  | POST    |     【逐仓】查询开仓单关联的止盈止损订单       |       是          |
交易  | 策略接口  | 全仓 |  /linear-swap-api/v1/swap_cross_tpsl_order                           | POST    |     【全仓】对仓位设置止盈止损订单       |       是          |
交易  | 策略接口  | 全仓 |  /linear-swap-api/v1/swap_cross_tpsl_cancel                           | POST    |    【全仓】止盈止损订单撤单       |       是          |
交易  | 策略接口  | 全仓 |  /linear-swap-api/v1/swap_cross_tpsl_cancelall                       | POST    |     【全仓】止盈止损订单全部撤单       |       是          |
读取  | 策略接口  | 全仓 |  /linear-swap-api/v1/swap_cross_tpsl_openorders                      | POST    |     【全仓】止盈止损订单当前委托       |       是          |
读取  | 策略接口  | 全仓 |  /linear-swap-api/v1/swap_cross_tpsl_hisorders                       | POST    |     【全仓】止盈止损订单历史委托       |       是          |
读取  | 策略接口  | 全仓 |  /linear-swap-api/v1/swap_cross_relation_tpsl_order                  | POST    |     【全仓】查询开仓单关联的止盈止损订单       |       是          |
交易  | 账户接口    |  通用  |  https://api.huobi.pro/v2/account/transfer                         | POST   |      【通用】现货-USDT本位永续账户间进行资金的划转              |     是        |

## 访问地址

访问地址 | 适用站点 | 适用功能 | 适用交易对 |
------ | ---- | ---- | ------ |
https://api.hbdm.com| 火币合约|   API     | 火币合约的交易品种  |

### 备注

 如果api.hbdm.com无法访问，可以使用api.btcgateway.pro来做调试，AWS服务器用户推荐使用api.hbdm.vn；


## 签名认证

### 签名说明

API 请求在通过 internet 传输的过程中极有可能被篡改，为了确保请求未被更改，除公共接口（基础信息，行情数据）外的私有接口均必须使用您的 API Key 做签名认证，以校验参数或参数值在传输途中是否发生了更改。

一个合法的请求由以下几部分组成：

- 方法请求地址：即访问服务器地址 api.hbdm.com，比如 api.hbdm.com/linear-swap-api/v1/swap_order 。

- API 访问密钥（AccessKeyId）：您申请的 API Key 中的 Access Key。

- 签名方法（SignatureMethod）：用户计算签名的基于哈希的协议，此处使用 HmacSHA256。

- 签名版本（SignatureVersion）：签名协议的版本，此处使用2。

- 时间戳（Timestamp）：您发出请求的时间 (UTC 时区) (UTC 时区) (UTC 时区) 。如：2017-05-11T16:22:06。在查询请求中包含此值有助于防止第三方截取您的请求。

- 必选和可选参数：每个方法都有一组用于定义 API 调用的必需参数和可选参数。可以在每个方法的说明中查看这些参数及其含义。 请一定注意：对于 GET 请求，每个方法自带的参数都需要进行签名运算； 对于 POST 请求，每个方法自带的参数不进行签名认证，即 POST 请求中需要进行签名运算的只有 AccessKeyId、SignatureMethod、SignatureVersion、Timestamp 四个参数，其它参数放在 body 中。

- 签名：签名计算得出的值，用于确保签名有效和未被篡改。


### 创建 API Key

您可以在 <a href='https://www.hbg.com/zh-cn/apikey/'>这里 </a> 创建 API Key。

API Key 包括以下两部分

- `Access Key`  API 访问密钥
  
- `Secret Key`  签名认证加密所使用的密钥（仅申请时可见）

<aside class="notice">
创建 API Key 时可以选择绑定 IP 地址，未绑定 IP 地址的 API Key 有效期为90天。
</aside>
<aside class="notice">
API Key 具有包括交易、借贷和充提币等所有操作权限。
</aside>
<aside class="warning">
这两个密钥与账号安全紧密相关，无论何时都请勿向其它人透露。
</aside>


### 签名步骤

规范要计算签名的请求 因为使用 HMAC 进行签名计算时，使用不同内容计算得到的结果会完全不同。所以在进行签名计算前，请先对请求进行规范化处理。下面以查询某订单详情请求为例进行说明：

查询某订单详情

`https://api.hbdm.com/linear-swap-api/v1/swap_order?`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`&SignatureMethod=HmacSHA256`

`&SignatureVersion=2`

`&Timestamp=2017-05-11T15:19:30`

#### 1. 请求方法（GET 或 POST），后面添加换行符 “\n”


`GET\n`

#### 2. 添加小写的访问地址，后面添加换行符 “\n”

`
api.hbdm.com\n
`

#### 3. 访问方法的路径，后面添加换行符 “\n”

`
/linear-swap-api/v1/swap_order \n
`

#### 4. 按照ASCII码的顺序对参数名进行排序。例如，下面是请求参数的原始顺序，进行过编码后


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

<aside class="notice">
使用 UTF-8 编码，且进行了 URI 编码，十六进制字符必须大写，如 “:” 会被编码为 “%3A” ，空格被编码为 “%20”。
</aside>
<aside class="notice">
时间戳（Timestamp）需要以YYYY-MM-DDThh:mm:ss格式添加并且进行 URI 编码。
</aside>


#### 5. 经过排序之后

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

#### 6. 按照以上顺序，将各参数使用字符 “&” 连接


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30`

#### 7. 组成最终的要进行签名计算的字符串如下

`POST\n`

`api.hbdm.com\n`

`/linear-swap-api/v1/swap_order\n`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30`


#### 8. 用上一步里生成的 “请求字符串” 和你的密钥 (Secret Key) 生成一个数字签名

`4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o=`

1. 将上一步得到的请求字符串和 API 私钥作为两个参数，调用HmacSHA256哈希函数来获得哈希值。

2. 将此哈希值用base-64编码，得到的值作为此次接口调用的数字签名。

#### 9. 将生成的数字签名加入到请求的路径参数里

最终，发送到服务器的 API 请求应该为

`https://api.hbdm.com/linear-swap-api/v1/swap_order?AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&Signature=4F65x5A2bLyMWVQj3Aqp%2BB4w%2BivaA7n5Oi2SuYtCJ9o%3D`

1. 把所有必须的认证参数添加到接口调用的路径参数里

2. 把数字签名在URL编码后加入到路径参数里，参数名为“Signature”。

## 访问次数限制

* 交割合约、币本位永续合约、期权合约和USDT本位永续合约都分开限频。

* 公开行情接口和用户私有接口都有访问次数限制

* 普通用户，需要密钥的私有接口，每个UID 3秒最多 72 次请求(交易接口3秒最多 36 次请求，查询接口3秒最多 36 次请求) (该UID的所有币种和不同到期日的合约的所有私有接口共享该限制) 。<a href=https://docs.huobigroup.com/docs/usdt_swap/v1/cn/#ab0b26742c>查看API接口类型列表(其中读取即查询,交易即交易)</a>

* 其他非行情类的公开接口，比如获取指数信息，限价信息，交割结算、平台持仓信息等，所有用户都是每个IP3秒最多120次请求（所有该IP的非行情类的公开接口请求共享3秒120次的额度）

- 行情类的公开接口，比如：获取K线数据、获取聚合行情、市场行情、获取行情深度数据、获取溢价指数K线、获取实时预测资金费率k线，获取基差数据、获取市场最近成交记录：

    （1） restful接口：同一个IP, 所有业务（交割合约、币本位永续合约、期权合约和USDT本位永续合约）总共1秒最多800个请求 

    （2） websocket：req请求，同一时刻最多请求50次；sub请求，无限制，服务器主动推送数据
    
- WebSocket私有订单成交推送接口(需要API KEY验签)

     一个UID最多同时建立30个私有订单成交推送WS链接。该用户在一个品种(包含该品种的所有周期的合约)上，仅需要维持一个订单推送WS链接即可。
   
     注意: 订单推送WS的限频，跟用户RESTFUL私有接口的限频是分开的，相互不影响。
     
- 查询与交易API接口返回的header中会有限频信息。比如：查询订单信息接口(/linear-swap-api/v1/swap_account_info)，返回的header中的ratelimit-limit即查询接口的总限制频率次数，ratelimit-remaining即查询接口的剩余总限制频率次数。下单接口(/linear-swap-api/v1/swap_order)，返回的header中的ratelimit-limit即交易接口的总限制频率次数，ratelimit-remaining即交易接口的剩余总限制频率次数。 <a href=https://docs.huobigroup.com/docs/usdt_swap/v1/cn/#ab0b26742c>查看API接口类型列表(其中读取即查询,交易即交易)</a>

- 所有API接口返回数据中增加限频信息

  将在api接口response中的header返回以下字段：
  
  ratelimit-limit： 单轮请求数上限，单位：次数
  
  ratelimit-interval：请求数重置的时间间隔，单位：毫秒
  
  ratelimit-remaining：本轮剩余可用请求数，单位：次数
  
  ratelimit-reset：请求数上限重置时间，单位：毫秒

  如果触发了撤单率限制，您的api接口response返回header中会包括字段：

  recovery-time：禁用的恢复时间戳，单位为毫秒，表示禁用结束时间，可恢复访问的时间戳；

  如果不在禁用期间，header不返回recovery-time字段；
  
- 一个uid对应计划委托下单接口请求1秒5次、一个uid对应计划委托撤单接口请求1秒5次、一个uid对应计划委托全部撤单接口请求1秒5次。

## 撤单率限制【暂未启用】

- 当用户通过API在10分钟内特定订单价格类型的委托单总笔数大于或等于3000笔时，系统会自动计算撤单率，如果撤单率大于99%，则禁止该用户通过API特定价格类型进行下单5分钟（如果下单会报：1084  您的合约API挂单接口被禁用,请于{0} (GMT+8) 后再试）；

- 当API用户在1小时的总禁用次数达到3次时，则禁止用户通过API特定价格类型进行下单30分钟（如果下单会报：1084  您的合约API挂单接口被禁用,请于{0} (GMT+8) 后再试），待解禁恢复访问后，总禁用次数重置，且之前周期统计过的次数不计入新周期的总禁用次数;

- 其他客户端挂撤单以及API撤单将不受影响，每次禁用会以短信和邮件形式通知；

- 被禁用的API下单类型仅包括：限价委托、Post_only、FOK、IOC四种订单价格类型，其他下单方式如lightning（闪电平仓下单），opponent(对手价下单)，optimal_5（最优5档），optimal_10(最优10档下单），optimal_20（最优20档下单），opponent_ioc（对手价-IOC下单），lightning_ioc（闪电平仓-IOC下单），optimal_5_ioc（最优5档-IOC下单），optimal_10_ioc（最优10档-IOC下单），optimal_20_ioc（最优20档-IOC下单），opponent_fok（对手价-FOK下单），lightning_fok（闪电平仓-FOK下单），optimal_5_fok（最优5档-FOK下单），optimal_10_fok（最优10档-FOK下单），optimal_20_fok（最优20档-FOK下单）等在禁用期间将仍然可用；

- HTTP返回的header信息：

  - 禁用期间下单类型为被禁用的四种类型时，接口返回信息header中会包括字段："recovery-time：禁用的恢复时间戳"，单位为毫秒，表示禁用结束时间，可恢复访问的时间戳；如果不在禁用期间，header中不返回该字段；

- 委托单总笔数与撤单率的计算是基于UID，母子UID是分开单独计算的。计算撤单率的时间周期为10分钟/次（开始时间从00:00开始,结束时间00:10。每10分钟一个周期。）；

- 指标说明：
 	- 撤单率 = 无效撤单总笔数 / 委托单总笔数（订单来源均为API）。
  - 委托单总笔数=同时满足以下所有条件的委托单总笔数：
      - 订单来源为API并且订单类型为报单（order Type = 1）；
    
      - 订单价格类型为限价委托、Post_only、FOK和IOC四种订单价格类型；
    
      - 委托单的下单时间在【当周期开始时间-3秒，当周期结束时间】内的委托单总笔数；
 	
    - 无效撤单总笔数=同时满足以下所有条件的委托单总笔数：
      - 订单来源为API并且订单类型为报单（order Type = 1）；
    
      - 订单价格类型为限价委托、Post_only、FOK和IOC四种订单价格类型；
    
      - 订单状态为已撤销（status = 7）；
    
      - 订单成交数量为0；
    
      - 撤单时间与下单时间间隔小于等于3秒；
    
      - 委托单的撤单时间在当周期内的委托单。
      
- 为了保证API系统的稳定性和交易性能，请您在高峰期时段尽量降低API订单的撤单量和撤单率，以避免频繁触发API的限制机制，以下是降低撤单率的建议：

  - 1．订单的价格更靠近盘口；

  - 2、适当延长下单与撤单的时间间隔；

  - 3、适当增加单笔订单金额，减少下单次数；

  - 4、尽量增加订单成交率:

      - 1) 优先使用对手价、最优5档、最优10档、最优20档、闪电平仓、opponent_ioc（对手价-IOC下单）、lightning_ioc（闪电平仓-IOC下单）、optimal_5_ioc（最优5档-IOC下单）、optimal_10_ioc（最优10档-IOC下单）、optimal_20_ioc（最优20档-IOC下单）、opponent_fok（对手价-FOK下单）、lightning_fok（闪电平仓-FOK下单）、optimal_5_fok（最优5档-FOK下单）、optimal_10_fok（最优10档-FOK下单）、optimal_20_fok（最优20档-FOK下单）等成交概率大的委托方式下单；

      - 2) IOC订单、FOK订单、Post_only订单尽量摆在买卖第一档的位置上；

  - 5、适当延长策略轮询时间。


## 停服维护

当该业务系统停服维护期间，除了以下2个提供给用户查询系统状态的接口能够正常使用外（<a href='https://docs.huobigroup.com/docs/usdt_swap/v1/cn/#cd63bde415'>获取当前系统状态</a>、<a href='https://docs.huobigroup.com/docs/usdt_swap/v1/cn/#bef5ec9210'>查询系统是否可用</a>），该业务所有rest接口都会固定返回响应报文:`{"status": "maintain"}`。websocket推送接口在停服维护时，除了WebSocket系统状态更新的推送接口可以正常调用外（<a href='https://docs.huobigroup.com/docs/usdt_swap/v1/cn/#b200f80f2c'>WebSocket系统状态更新接口</a>），其他推送接口都会返回1006的错误码。

>Response

```json
{
    "status": "maintain"
}
``` 

#### 2个接口为：
 - 查询系统是否可用：https://api.hbdm.com/heartbeat/
 - statuspage查询系统状态：https://status-linear-swap.huobigroup.com/api/v2/summary.json

除了以上两个rest接口获取系统维护停服信息外，也可以通过订阅WebSocket系统状态更新接口获取系统维护停服信息

## 获取当前系统状态

此接口返回当前的系统状态，包含当前系统维护计划和故障进度等。

如您需要通过邮件、短信、Webhook、RSS/Atom feed接收以上信息，可点击<a href='https://status-linear-swap.huobigroup.com/'>这里</a>进入页面进行订阅。当前订阅依赖Google服务，订阅前请确保您可正常访问Google的服务，否则将订阅失败。

```shell
curl "https://status-linear-swap.huobigroup.com/api/v2/summary.json"
```

### HTTP 请求

- GET `https://status-linear-swap.huobigroup.com/api/v2/summary.json`

### 请求参数

此接口不接受任何参数。

> Response:

```json
{
  "page": {  // 合约页面基本信息
    "id": "p0qjfl24znv5",  // 页面id
    "name": "Huobi Futures-USDT-margined Swaps",  // 页面名称
    "url": "https://status-linear-swap.huobigroup.com", // 页面地址
    "time_zone": "Asia/Singapore", // 时区
    "updated_at": "2020-02-07T10:25:14.717Z" // 页面最新一次更新时间
  },
  "components": [  // 系统组件及状态
    {
      "id": "h028tnzw1n5l",  // 组件id
      "name": "Deposit", // 组件名称
      "status": "operational", // 组件状态
      "created_at": "2019-12-05T02:07:12.372Z",  // 组件创建时间
      "updated_at": "2020-02-07T09:27:15.563Z", // 组件更新时间
      "position": 1,
      "description": null,
      "showcase": true,
      "group_id": "gtd0nyr3pf0k",  
      "page_id": "p0qjfl24znv5", 
      "group": false,
      "only_show_if_degraded": false
    }
  ],
  "incidents": [ // 系统故障事件及状态
        {
            "id": "rclfxz2g21ly",  // 事件id
            "name": "Market data is delayed",  // 事件名称
            "status": "investigating",  // 事件状态
            "created_at": "2020-02-11T03:15:01.913Z",  // 事件创建时间
            "updated_at": "2020-02-11T03:15:02.003Z",   // 事件更新时间
            "monitoring_at": null,
            "resolved_at": null,
            "impact": "minor",  // 事件影响程度
            "shortlink": "http://stspg.io/pkvbwp8jppf9",
            "started_at": "2020-02-11T03:15:01.906Z",
            "page_id": "p0qjfl24znv5",
            "incident_updates": [ 
                {
                    "id": "dwfsk5ttyvtb",  
                    "status": "investigating",  
                    "body": "Market data is delayed",  
                    "incident_id": "rclfxz2g21ly",   
                    "created_at": "2020-02-11T03:15:02.000Z",    
                    "updated_at": "2020-02-11T03:15:02.000Z",   
                    "display_at": "2020-02-11T03:15:02.000Z",    
                    "affected_components": [  
                        {
                            "code": "nctwm9tghxh6",  
                            "name": "Market data",  
                            "old_status": "operational",  
                            "new_status": "degraded_performance"   
                        }
                    ],
                    "deliver_notifications": true,
                    "custom_tweet": null,
                    "tweet_id": null
                }
            ],
            "components": [  
                {
                    "id": "nctwm9tghxh6",    
                    "name": "Market data", 
                    "status": "degraded_performance", 
                    "created_at": "2020-01-13T09:34:48.284Z", 
                    "updated_at": "2020-02-11T03:15:01.951Z", 
                    "position": 8,
                    "description": null,
                    "showcase": false,
                    "group_id": null,
                    "page_id": "p0qjfl24znv5",
                    "group": false,
                    "only_show_if_degraded": false
                }
            ]
        }
    ],
      "scheduled_maintenances": [  // 系统计划维护事件及状态
        {
            "id": "k7g299zl765l", // 事件id
            "name": "Schedule maintenance", // 事件名称
            "status": "scheduled", // 事件状态
            "created_at": "2020-02-11T03:16:31.481Z",  // 事件创建时间
            "updated_at": "2020-02-11T03:16:31.530Z",  // 事件更新时间
            "monitoring_at": null,
            "resolved_at": null,
            "impact": "maintenance", // 事件影响
            "shortlink": "http://stspg.io/md4t4ym7nytd",
            "started_at": "2020-02-11T03:16:31.474Z",
            "page_id": "p0qjfl24znv5",
            "incident_updates": [  
                {
                    "id": "8whgr3rlbld8",  
                    "status": "scheduled", 
                    "body": "We will be undergoing scheduled maintenance during this time.", 
                    "incident_id": "k7g299zl765l", 
                    "created_at": "2020-02-11T03:16:31.527Z",  
                    "updated_at": "2020-02-11T03:16:31.527Z",  
                    "display_at": "2020-02-11T03:16:31.527Z",  
                    "affected_components": [  
                        {
                            "code": "h028tnzw1n5l",  
                            "name": "Deposit And Withdraw - Deposit",  
                            "old_status": "operational",  
                            "new_status": "operational"  
                        }
                    ],
                    "deliver_notifications": true,
                    "custom_tweet": null,
                    "tweet_id": null
                }
            ],
            "components": [ 
                {
                    "id": "h028tnzw1n5l",  
                    "name": "Deposit", 
                    "status": "operational", 
                    "created_at": "2019-12-05T02:07:12.372Z",  
                    "updated_at": "2020-02-10T12:34:52.970Z",  
                    "position": 1,
                    "description": null,
                    "showcase": false,
                    "group_id": "gtd0nyr3pf0k",
                    "page_id": "p0qjfl24znv5",
                    "group": false,
                    "only_show_if_degraded": false
                }
            ],
            "scheduled_for": "2020-02-15T00:00:00.000Z",  // 计划维护开始时间
            "scheduled_until": "2020-02-15T01:00:00.000Z"  // 计划维护结束时间
        }
    ],
    "status": {  // 系统整体状态
        "indicator": "minor",   // 系统状态指标
        "description": "Partially Degraded Service"  // 系统状态描述
    }
}
```

### 返回字段

|字段名称 | 数据类型 | 描述
|--------- |  -----------|  -----------
|page    |                     | status page页面基本信息
|{id        |  string                   | 页面id
|name      |      string                | 页面名称
|url     |    string                  | 页面地址
|time_zone     |     string                 | 时区
|updated_at}     |    string                  | 页面更新时间
|components  |                      | 系统组件及状态
|[{id        |  string                    | 组件id
|name        |    string                  | 组件名称，如Order submission、Order cancellation、Deposit等
|status        |    string                  | 组件状态，取值范围为：operational，degraded_performance，partial_outage，major_outage，under maintenance
|created_at        |    string                  | 组件创建时间
|updated_at        |    string                  | 组件更新时间
|.......}]        |                     | 其他字段明细，请参考返回示例
|incidents  |           | 系统故障事件及状态，若当前无故障则返回为空
|[{id        |       string               | 事件id
|name        |      string                | 事件名称
|status        |     string                 | 事件状态，取值范围为：investigating，identified，monitoring，resolved
|created_at        |       string               | 事件创建时间
|updated_at        |      string                | 事件更新时间
|.......}]        |                     | 其他字段明细，请参考返回示例
|scheduled_maintenances|                     | 系统计划维护事件及状态，若当前无计划维护则返回为空
|[{id        |     string                 | 事件id
|name        |      string                | 事件名称
|status        |       string               | 事件状态，取值范围为：scheduled，in progress，verifying，completed
|created_at        |     string                 | 事件创建时间
|updated_at        |     string                 | 事件更新时间
|scheduled_for       |      string                | 计划维护开始时间
|scheduled_until       |     string                 | 计划维护结束时间
|.......}]        |                     | 其他字段明细，请参考返回示例
|status   |                       | 系统整体状态
|{indicator        |    string                  | 系统状态指标，取值范围为：none，minor，major，critical，maintenance
|description}     |      string                | 系统状态描述，取值范围为：All Systems Operational，Minor Service Outager，Partial System Outage，Partially Degraded Service，Service Under Maintenance




## 查询系统是否可用  

- Interface `https://api.hbdm.com/heartbeat/`

### 备注：
 -  注意请求时地址后面的“/”一定要带上。

### 返回参数
| 参数名称 |  类型  |   描述         |
| ------------------ | ------------------ | ------------- | 
| status             | string                   | "ok" 或 "error"... 
| \<data\>             | dict object                 | 
| heartbeat             | int                   | 交割合约 1: 可用 0: 不可用(即停服维护) 
| swap_heartbeat             | int                   | 币本位永续 1: 可用 0: 不可用(即停服维护) 
| estimated_recovery_time             | long                   | null: 正常. 交割合约预计恢复时间， 单位:毫秒
| swap_estimated_recovery_time             | long                   | null: 正常. 币本位永续合约预计恢复时间，单位：毫秒.
| option_heartbeat             | int                   | 期权合约 1: 可用 0: 不可用(即停服维护) 
| option_estimated_recovery_time             | long                   | null: 正常. 期权合约预计恢复时间，单位：毫秒.
| linear_swap_heartbeat             | long                   | USDT本位永续 1: 可用 0: 不可用(即停服维护)
| linear_swap_estimated_recovery_time             | long                   | null: 正常. USDT本位永续合约预计恢复时间，单位：毫秒.
| \</data\>             |                  | 


> 返回数据

```json

{
    "status":"ok",
    "data":{
        "heartbeat":1,
        "estimated_recovery_time":null,
        "swap_heartbeat":1,
        "swap_estimated_recovery_time":null,
        "option_heartbeat":1,
        "option_estimated_recovery_time":null,
        "linear_swap_heartbeat":1,
        "linear_swap_estimated_recovery_time":null
    },
    "ts":1557714418033
}
```

## 获取当前系统时间戳

 get `https://api.hbdm.com/api/v1/timestamp`

### 请求参数
   无
   
> 返回数据

```json

{
    "status": "ok",
    "ts": 1578124684692
}

```
### 返回参数
| 参数名称                   | 是否必须 | 类型      | 描述                 | 取值范围                                     |
| ---------------------- | ---- | ------- | ------------------ | ---------------------------------------- |
| status                 | true | string  | 请求处理结果             |                                          |
| ts                     | true | long    | 当前系统时间戳                |                                          |

#### 备注
 - 可以用于校对系统时间。

## 错误码详情

错误代码	 | 错误描述|
----- | ---------------------- |
403	|	无效身份                |
1000  | 系统异常
1001  | 系统未准备就绪
1002  | 查询异常
1003  | 操作redis异常
1004  | 系统繁忙,请稍后再试
1010  | 用户不存在
1011  | 用户会话不存在,请重试
1012  | 账户不存在
1013  | 合约品种不存在
1014  | 合约不存在
1015  | 指数价格不存在
1016  | 对手价不存在
1017  | 查询订单不存在
1018  | 主账号不存在
1019  | 主账号不在开通子账号白名单里
1020  | 您的子账号数量已超出限制,请联系客服
1021  | 开户失败。您的主账号尚未开通合约交易权限,请前往开通
1030  | 输入错误
1031  | 非法的请求来源
1032  | 访问次数超出限制
1033  | 合约周期字段值错误
1034  | 报单价格类型字段值错误
1035  | 报单方向字段值错误
1036  | 报单开平字段值错误
1037  | 倍数不符合要求,请联系客服
1038  | 下单价格超出精度限制,请修改后下单
1039  | 买入价必须低于{0}{1},卖出价必须高于{2}{3}
1040  | 下单数量不能为空或者不能小于0, 请修改后下单
1041  | 下单数量超出限制 ({0}张),请修改后下单
1042  | 下单数量+挂单数量+持仓数量超过了单用户多仓持仓限制({0}张),请修改后下单
1043  | 下单数量+挂单数量+持仓数量超过了单用户空仓持仓限制({0}张), 请修改后下单
1044  | 触发平台限仓,请修改后下单
1045  | 当前有挂单,无法切换倍数
1046  | 当前合约持仓不存在
1047  | 可用担保资产不足
1048  | 可平量不足
1049  | 暂不支持市价开仓
1050  | 客户报单号重复
1051  | 没有可撤销的订单
1052  | 批量撤单、下单的订单数量超过平台限制数量
1053  | 无法获取最新价格区间
1054  | 无法获取最新价
1055  | 价格不合理, 下单后将导致账户权益小于0 , 请修改价格后下单
1056  | 结算中,暂时无法下单/撤单
1057  | 暂停交易中,暂时无法下单
1058  | 停牌中,暂时无法下单
1059  | 交割中,暂时无法下单/撤单
1060  | 合约处于非交易状态,暂时无法下单
1061  | 订单不存在
1062  | 撤单中,请耐心等待
1063  | 订单已成交
1064  | 报单主键冲突
1065  | 客户报单号不是整数
1066  | {0}字段不能为空
1067  | {0}字段不合法
1068  | 导出错误
1069  | 价格不合理
1070  | 数据为空,无法导出
1071  | 订单已撤,无法撤单
1072  | 卖出价必须低于{0}{1}
1073  | 仓位异常,请联系客服
1074  | 下单异常,请联系客服
1075  | 价格不合理, 下单后将导致担保资产率小于0 , 请修改价格后下单
1076  | 盘口无数据,请稍后再试
1077  | 交割结算中,当前品种资金查询失败
1078  | 交割结算中,部分品种资金查询失败
1079  | 交割结算中,当前品种持仓查询失败
1080  | 交割结算中,部分品种持仓查询失败
1081  | {0}合约计划委托订单数量不得超过{1}
1082  | 触发类型参数错误
1083  | 您的仓位已进入强平接管,暂时无法下单
1084  | 您的合约API挂单接口被禁用,请于{0} (GMT+8) 后再试
1085  | 计划委托下单失败,请修改价格再次下单或联系客服
1086  | {0}合约暂时限制{1}端开仓,请联系客服
1087  | {0}合约暂时限制{1}端平仓,请联系客服
1088  | {0}合约暂时限制{1}端撤单,请联系客服
1089  | {0}账户暂时限制划转,请联系客服
1090  | 担保资产率小于0, 无法下单
1091  | 账户权益小于0, 无法下单
1092  | 闪电平仓取盘口第{0}档的价格, 下单后将导致账户权益小于0 , 请改为手动输入价格或使用对手价下单
1093  | 闪电平仓取盘口第{0}档的价格, 下单后将导致担保资产率小于0 , 请改为手动输入价格或使用对手价下单
1094  | 倍数不能为空, 请切换倍数或联系客服
1095  | 合约处于非交易状态, 暂时无法切换倍数
1100  | 您没有开仓权限,请联系客服
1101  | 您没有平仓权限,请联系客服
1102  | 您没有转入权限,请联系客服
1103  | 您没有转出权限,请联系客服
1104  | 合约交易受限,当前禁止交易
1105  | 合约交易受限,当前只能平仓
1106  | 合约交割结算中,暂时无法划转
1108  | Dubbo调用异常
1109  | 子账号没有开仓权限,请联系客服
1110  | 子账号没有平仓权限,请联系客服
1111  | 子账号没有入金权限,请联系客服
1112  | 子账号没有出金权限,请联系客服
1113  | 子账号没有交易权限,请登录主账号授权
1114  | 子账号没有划转权限,请登录主账号授权
1115  | 您没有访问此子账号的权限
1200  | 登录失败,请重试
1220  | 您尚未开通合约交易,无访问权限
1221  | 币币账户总资产不满足合约开通条件
1222  | 开户天数不满足合约开通条件
1223  | VIP等级不满足合约开通条件
1224  | 您所在的国家/地区不满足合约开通条件
1225  | 开通合约失败
1226  | 合约已开户,无法重复开户
1227  | 火币合约暂不支持子账户,请返回退出子账户,切换主账户登录
1228  | 您尚未开通合约交易, 请先开通
1229  | 重复同意协议
1230  | 您尚未做风险认证
1231  | 您尚未做身份认证
1232  | 您上传的图片格式/大小不符合要求,请重新上传
1233  | 您尚未开通高倍数协议 (使用高倍数请先使用主账号登录web或APP端同意高倍数协议)
1234  | {0}合约开仓委托订单数量不得超过{1}
1235  | {0}合约平仓委托订单数量不得超过{1}
1250  | 无法获取HT_token
1251  | 无法获取BTC净资产,请稍后再试
1252  | 无法获取币币账户资产,请稍后再试
1253  | 签名验证错误
1254  | 子账号无权限开通合约，请前往web端登录主账号开通
1300  | 划转失败
1301  | 可划转余额不足
1302  | 系统划转错误
1303  | 单笔转出的数量不能低于{0}{1}
1304  | 单笔转出的数量不能高于{0}{1}
1305  | 单笔转入的数量不能低于{0}{1}
1306  | 单笔转入的数量不能高于{0}{1}
1307  | 您当日累计转出量超过{0}{1}, 暂无法转出
1308  | 您当日累计转入量超过{0}{1}, 暂无法转入
1309  | 您当日累计净转出量超过{0}{1}, 暂无法转出
1310  | 您当日累计净转入量超过{0}{1}, 暂无法转入
1311  | 超过平台当日累计最大转出量限制, 暂无法转出
1312  | 超过平台当日累计最大转入量限制, 暂无法转入
1313  | 超过平台当日累计最大净转出量限制, 暂无法转出
1314  | 超过平台当日累计最大净转入量限制, 暂无法转入
1315  | 划转类型错误
1316  | 划转冻结失败
1317  | 划转解冻失败
1318  | 划转确认失败
1319  | 查询可划转金额失败
1320  | 此合约在非交易状态中, 无法进行系统划转
1321  | 划转失败, 请稍后重试或联系客服
1322  | 划转金额必须大于0
1323  | 服务异常, 划转失败, 请稍后再试
1325  | 设置交易单位失败
1326  | 获取交易单位失败
1327  | 无划转权限, 划转失败, 请联系客服
1328  | 无划转权限, 划转失败, 请联系客服
1329  | 无划转权限, 划转失败, 请联系客服
1330  | 无划转权限, 划转失败, 请联系客服
1331  | 超出划转精度限制(8位), 请修改后操作
1332  | 永续合约不存在
1333  | 开通跟单吃单协议失败
1334  | 查询跟单吃单协议失败
1335  | 查询跟单吃单二次确认设置失败
1336  | 更新跟单吃单二次确认设置失败
1337  | 查询跟单吃单设置失败
1338  | 更新跟单吃单设置失败
1339  | 昵称含有不合法词汇, 请修改
1340  | 昵称已被使用, 请修改
1341  | 报名阶段已结束
1342  | 子账号无法设置昵称
1343  | 指标失效, 请重新设置
1344  | 抱歉, 目前可最多对{0}个合约创建行情提醒
1345  | 抱歉, {0}合约目前可最多创建{1}个提醒
1346  | 该指标已存在, 请勿重复设置
1347  | {0}参数错误, 请修改
1348  | 该合约不支持全仓模式
1349  | 委托单倍数与当前持仓的倍数不符, 请先切换倍数
1401  | 委托价必须小于行权价
1403  | {0}合约止盈止损订单的委托数量不得超过{1}  
1404  | 止盈止损订单仅支持与开仓订单绑定 
1405  | 止盈价不得{0}{1}{2} 
1406  | 您的抽奖次数已用完 
1407  | 止损价不得{0}{1}{2}  
1408  | 该止盈止损委托单未生效, 无法撤销
1409  | 您没有止盈止损订单权限,请联系客服
12001  | 无效的提交时间
12002  | 错误的签名版本
12003  | 错误的签名方法
12004  | 密钥已经过期
12005  | ip地址错误
12006  | 提交时间不能为空
12007  | 公钥错误
12008  | 校验失败
12009  | 用户被锁定或不存在

## API 最佳实践

### 1、/linear-swap-api/v1/swap_hisorders 历史委托查询接口：

- 为了保证时效性和降低延迟，强烈建议用户使用/linear-swap-api/v1/swap_order_info获取用户订单信息接口来查询订单信息，获取合约订单信息接口从内存里面查询，无延迟，接口响应速度更快。

- 如果用户一定要使用/linear-swap-api/v1/swap_hisorders 历史委托查询接口，请尽量输入更多的查询条件，trade_type（推荐传0查询全部）、type、status、create_date尽量都输入，并且查询日期create_date参数输入尽量小的整数，最好只查询一天的数据；

 

### 2、/linear-swap-api/v1/swap_matchresults 获取历史成交记录接口：

- 为了提升查询的性能和响应速度，查询条件 trade_type（推荐传0查询全部） 、contract_code 、create_date 尽量都输入，并且create_date输入尽量小的整数，最好只查询一天的数据；

 

### 3、/linear-swap-api/v1/swap_financial_record 查询用户财务记录接口：

- 为了提升查询的性能和响应速度，查询条件type（推荐不填查询全部）、create_date，尽量都输入，并且查询日期create_date参数输入尽量小的整数，最好只查询一天的数据；

 

### 4、/linear-swap-api/v1/swap_order_detail 获取订单明细接口：

- 请求参数没有带上created_at等参数查询订单时，可能会发生查询结果延迟。建议您在使用此接口时请求字段带上：created_at（下单时间戳）和 order_type(订单类型，默认填1)，会直接查询数据库，查询结果会更及时。

- 查询条件created_at使用13位long类型时间戳（包含毫秒时间），如果输入准确的时间戳，查询性能将会提升。

- 例如:"2019/10/18 10:26:22"转换为时间戳为：1571365582123。也可以直接从swap_order下单接口返回报文中的ts中获取时间戳作为参数查询接口/linear-swap-api/v1/swap_order_detail获取订单明细，同时created_at禁止传0；；

 

### 5、订阅Market Depth 数据的WebSocket：

- 获得150档深度数据，使用step0, step1, step2, step3, step4, step5, step14, step15；

- 获得20档深度数据，使用 step6, step7, step8, step9, step10, step11, step12, step13；

- 由于每100ms推送一次150档全量数据，数据量比较大，如果客户端网络带宽不足或者处理不及时，webSocket断开可能比较频繁，强烈建议使用step6, step7, step8, step9, step10, step11, step12, step13 取20档数据。比如订阅20档数据

`{`

  `"sub": "market.BTC-USDT.depth.step6",`

  `"id": "id5"`

`}`
 

- 我们也推荐使用增量订阅市场深度数据，增量深度数据有20档不合并数据和150档不合并数据，首次或者重连都推送全量数据，之后会推送增量数据，每30MS检查一次，如果有更新则推送，没有更新则不推送。需要维护好本地的深度数据。

`{`

  `"sub": "market.BTC-USDT.depth.size_20.high_freq",`

  `"data_type":"incremental",`

  `"id": "id1"`

`}`
 

### 6、/linear-swap-api/v1/swap_order合约下单和/linear-swap-api/v1/swap_batchorder合约批量下单接口：

- 推荐传参数client_order_id（用户级别唯一），主要防止下单和批量下单接口由于网络或其它原因接口超时或者没有返回，可以根据client_order_id通过请求接口/linear-swap-api/v1/swap_order_info来快速获取订单是否下单正常或者快速获取订单信息。


## 代码实例

- <a href='https://github.com/hbdmapi/huobi_usdt_swap_Java'>Java</a>

- <a href='https://github.com/hbdmapi/hbdm_Python'>Python</a>

- <a href='https://github.com/hbdmapi/huobi_futures_Postman'>Postman</a>

- <a href='https://github.com/hbdmapi/huobi_futures_CSharp'>CSharp</a>

- <a href='https://github.com/hbdmapi/huobi_futures_Golang'>Golang</a>

- <a href='https://github.com/hbdmapi/huobi_futures_Cpp'>C++</a>


### 备注：USDT本位永续代码使用方式与币本位永续和交割合约类似，可以参考币本位永续和交割合约。

# 常见问题

## 接入验签相关

### Q1: USDT本位永续合约API Key和现货是否同一个？

USDT本位永续合约API Key和现货API Key是同一个，两个是一样的。您可以在 <a href='https://www.hbg.com/zh-cn/apikey/'>这里 </a> 创建 API Key。

### Q2: 为什么经常出现断线、超时的错误？

如果是在大陆网络环境去请求API接口，网络连接很不稳定，很容易出现超时。建议使用AWS东京C区服务器进行访问。

国内网络可以使用api.btcgateway.pro或者api.hbdm.vn来进行调试,如果仍然无法请求，请在国外服务器上进行运行。

### Q3: 为什么WebSocket总是断开连接？

由于网络环境不同，很容易导致websocket断开连接(websocket: close 1006 (abnormal closure))，目前最佳实践是建议您将服务器放置在AWS东京C区，并且使用api.hbdm.vn域名；同时需要做好断连重连操作；行情心跳与订单心跳均需要按照《Websocket心跳以及鉴权接口》的行情心跳与订单心跳回复不同格式的Pong消息：<a href='https://docs.huobigroup.com/docs/usdt_swap/v1/cn/#472585d15d'>这里</a>。以上操作可以有效减少断连情况。

### Q4: api.hbdm.com与api.hbdm.vn有什么区别？

api.hbdm.vn域名使用的是AWS的CDN服务，理论上AWS服务器用户使用此域名会更快更稳定；api.hbdm.com域名使用的是Cloudflare的CDN服务。

### Q5: 市商享受的colocation服务是指什么以及使用注意事项？

colo相当于是 创建一个VPC节点，直接连了火币合约的内网，会减少客户服务器和火币合约服务器的通讯时间（绕过CDN）。

火币交割合约 的Colocation和 永续合约 是共用的，即连接永续合约Colocation的域名与交割合约是一样的；

但请您注意：colo需要使用：api.hbdm.com 进行签名（鉴权），避免返回403:Verification failure [校验失败] 的错误。

### Q6: 为什么签名认证总返回失败(403:Verification failure [校验失败]) ？

USDT本位永续签名过程和币本位永续、交割类似，除了参考以下注意事项外，请参照币本位永续或者交割的demo代码来验证签名是否成功，demo代码验证通过后，再去核对您自己的签名代码。币本位永续的demo代码在 <a href='https://docs.huobigroup.com/docs/coin_margined_swap/v1/cn/#2cff7db524'>  这里 </a>   查看。交割的demo代码在<a href='https://docs.huobigroup.com/docs/dm/v1/cn/#2cff7db524'>  这里</a>  查看。期权的demo代码在<a href='https://docs.huobigroup.com/docs/option/v1/cn/#2cff7db524'>  这里</a>  查看。USDT本位永续的demo代码在 <a href='https://docs.huobigroup.com/docs/usdt_swap/v1/cn/#2cff7db524'>  这里 </a>   查看。

1. 检查 API Key 是否有效，是否复制正确

2. 是否有绑定 IP 白名单

3. 检查时间戳是否是 UTC 时间

4. 检查参数是否按字母排序

5. 检查编码，使用 UTF-8 编码

6. 检查签名是否有 base64 编码

7. 对于 GET 请求，每个方法自带的参数都需要进行签名运算

8. 对于 POST 请求，每个方法自带的参数不进行签名认证

9. 检查签名结果是否有进行 URI 编码，十六进制字符必须大写，如 “:” 会被编码为 “%3A”  ，空 格被编码为 “%20”

10. websocket构建签名与restful类似，websocket构建json请求的数据不需要URL编码。

11. 签名时所带Host应与请求接口时Host相同。如果您使用了代理，代理可能会改变请求Host，可以尝试去掉代理；您使用的网络连接库可能会把端口包含在Host内，可以尝试在签名用到的Host中包含端口，如“api.hbdm.com:443"

12. Api Key 与 Secret Key中是否存在隐藏特殊字符，影响签名.

### Q7: 公开行情根据ip限速，需要私钥的根据uid限速是吗？

是的。私有的根据UID来限速，不是根据API—KEY限速，母子帐号是分开分别限速，互不影响。

### Q8: 第三方框架集成火币合约是否有推荐？

目前已经有异步量化框架开源，集成了火币交割合约与永续合约： <a href=https://github.com/hbdmapi/hbdm_Python> 异步量化框架地址 </a>，有使用反馈或者问题请在github issue区进行提问。

## 行情及WS推送相关

### Q1: 全量行情orderbook订阅和增量orderbook订阅是多长时间推送？

全量orderbook深度推送(market.$contract_code.depth.$type)是100MS检查一次，有更新则推送，至少1秒会推送1次。增量orderbook深度推送(market.$contract_code.depth.size_${size}.high_freq)是30MS检查一次，有更新则推送，没有更新则不推送。

### Q2: 市场公开逐笔成交是多长时间推送？

市场公开逐笔成交market.$contract_code.trade.detail是有成交则推送。

### Q3: 有没有历史K线数据或者历史的公开市场逐笔成交数据？

历史K线数据可以通过API接口/linear-swap-ex/market/history/kline去获取，只填写from,to参数，不写size参数，最多只能获取连续两年的数据。

历史的公开市场逐笔成交数据目前没有，您可以通过订阅market.$contract_code.trade.detail来本地进行存储。

### Q4: 如何获取K线上的MACD等技术指标？

API没有获取K线上的MACD等技术指标接口，您可以参考TradingView等网站来计算。

### Q5: 文档里的时间戳timestamp定义是什么？

文档里的时间戳是指格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现在的总秒数或者总毫秒数。

### Q6: 获取行情深度数据中请求参数type的 150档，20档具体是指？

订阅行情深度market.$contract_code.depth.$type,150档指当前盘口的买卖盘的订单，将价格顺序切分为150个小区间，统计每个小区间的挂单数；20档指当前盘口的买卖盘的订单，将价格顺序切分为20个小区间，统计每个小区间的挂单数。

### Q7: 获取行情深度数据中请求参数type的“合并深度”是什么意思？

订阅行情深度(market.$contract_code.depth.$type)：

step1和step7 按5位小数合并，买盘向下、卖盘向上
step2和step8 按4位小数合并，买盘向下、卖盘向上
step3和step9 按3位小数合并，买盘向下、卖盘向上
step4和step10 按2位小数合并，买盘向下、卖盘向上
step5和step11 按1位小数合并，买盘向下、卖盘向上
step12和step14 按个位数合并，买盘向下、卖盘向上
step13和step15 按十位数合并，买盘向下、卖盘向上
step4 合并为0.01 例如，下买单价格 100.123， 100.245，
盘口就显示下单价格 100.12， 100.24
如果是卖单 盘口显示价格： 100.13， 100.25

（“向下”和“向上”即是否四舍五入，如买盘向下则不进一位，卖盘向上则进一位）
step0到step5,step14,step15是150档；
step6到step13是20档；
step6是不合并小数；
结合以上举例说明：

假设当前价格1.123456  6位小数点，如果我单选step1，如果价格是买盘，显示价格是 1.12345（不四舍五入），如果是卖盘，就是1.12346（四舍五入）；

同理，如果我选择step7也是同样的，如果价格是买盘，显示价格是 1.12345（不四舍五入），如果是卖盘，就是1.12346（四舍五入）；

假设是TRX 选择20档 那么step6是不合并，如果当前价格是1.123456 6位小数点，选择step6，不论买卖盘口还是1.123456 6位小数；

假设是TRX 选择20档 那么step11按1位小数合并，假设当前价格1.123456 6位小数点，如果我单选step11，如果价格是买盘，显示价格是 1.1（不四舍五入），如果是卖盘，就是1.1（四舍五入)。

### Q8: websocket的持仓变动频道，每次是返回全量数据还是增量变化的数据？

订阅持仓推送："topic": "positions.BTC-USDT"，推送的是最新的持仓（包括持仓量、可平仓数量、冻结数量），没有变化就不推送。

### Q9: websocket持仓订阅频道，未实现盈亏有变化会推送吗?

订阅持仓推送："topic": "positions.BTC-USDT", 如果持仓有变动，包括开仓/平仓/交割等，会推送仓位变化，若只是单纯的未实现盈亏不会推送。

### Q10: WS中的market detail 和 trade detail 具体什么区别和含义?

Market Detail(market.$contract_code.detail)  是市场聚合行情，0.5s检测1次，有成交则推送。包含了此时间段的开盘价、收盘价、最高价、最低价和成交数量；Trade Detail(market.$contract_code.trade.detail) 是有成交更新就会推送，包括成交价格、成交数量和成交方向等数据。

### Q11: 订阅market depth增量数据返回参数的两个ts分别是什么？

增量depth订阅：market.$contract_code.depth.size_${size}.high_freq，外层ts是到行情服务器开始转发这笔数据的系统时间戳，里层ts是orderbook的检测时间点。

### Q12: 通过ws订阅market depth数据和market depth增量数据的区别是什么？订阅market depth增量数据多久推送一次？

market.$contract_code.depth.$type是全量数据，market.$contract_code.depth.size_${size}.high_freq是增量数据，全量数据是100ms检查一次，至少1秒推送1次；增量30MS检查1次，无更新不推送。

目前market depth增量数据market.$contract_code.depth.size_${size}.high_freq是30MS检测一次，不是随机检测，30m检查一次更新，但是有二台机同时进行，每两次的时间间隔最小可能是0，但30ms内最多推送6次，最大时间间隔无上限，30ms内最少推送次数为0。

### Q13: 增量数据market.$contract_code.depth.size_${size}.high_freq推送如何维护本地数据？

增量数据首次会推送全量数据，之后推送的为增量数据。

(1) 把增量的价格与上一个全量做比较，相同的价格把挂单量替换；

(2) 没有相同价格的添加到本地全量数据；

(3) 如果某个价格挂单没有了，会推送类似[8100, 0]这样的数据，把本地相同价格的移除；

(4) 同一个websocket连接，增量数据version是递增的；如果 version不递增，您需要重新订阅并重新维护本地全量数据；

### Q14:获取合约的历史资金费率（/linear-swap-api/v1/swap_historical_funding_rate）返回字段中“当期资金费率（funding_rate）”和“实际资金费率（realized_rate）”的区别？

在正常情况下当期资金费率和实际资金费率是相等的。只有在支付资金费率会导致用户爆仓时，会少收或不收资金费率（少收或不收的资金费率值就是实际资金费率）。当期资金费率不变。

## 交易相关

### Q1: USDT本位永续的资金费率结算周期是什么？资金费率结算时通过哪些接口可以查询状态？

温馨提示您，USDT本位永续合约每8小时为一期，每期结束时进行结算。即00:00-08:00为一期，结算时间为08:00；08:00-16:00为一期，结算时间为16:00；16:00-次日00:00为一期，结算时间为00:00。以上时间均为新加坡时间。

(1)在结算时不能下单和撤单，若用户在结算时下单或撤单会返回错误码"1056"，提示结算中无法下单和撤单。
建议您在结算时间点每隔几秒钟轮询获取合约信息接口：linear-swap-api/v1/swap_contract_info，当返回报文中contract_status返回状态码为5、6、7、8中的任意一个数字时表示在结算中，当contract_status返回状态码为1时是表示结算完成可以正常下单和撤单。


(2)在结算时查询资金和持仓会返回错误码，返回的错误码及错误码表示的含义如下：

  1.	错误码"1077"表示"交割结算中，当前品种资金查询失败"；
  2.	错误码"1078"表示"交割结算中，部分品种资金查询失败"；
  3.	错误码"1079"表示"交割结算中，当前品种持仓查询失败"；
  4.	错误码"1080"表示"交割结算中，部分品种持仓查询失败"；

建议您从返回的报文里读取状态码，如果状态码出现上述四种类型，请不要用这个返回的数据。

### Q2: API返回1004错误码是什么原因？

由于近段时间平台系统订单堆积情况比较严重，我们的技术人员正在努力解决和优化中，如果近段时间出现系统繁忙的情况或者出现以下提示：

{“status”:”error”,”err_code”:1004,”err_msg”:”System busy. Please try again later.”,”ts”: }

请您耐心等待，在此过程中请不要进行重复的下单和撤单，以避免造成重复下单以及对系统性能造成额外的压力，在此期间，建议您可以通过Web和APP端进行下单和撤单。

### Q3: 同样的order id 和 match id，可以有N多个Trade，比如，用户是一笔大的taker单，吃掉了N个maker的订单，那么，就会对应有N个trade，如何标识这些不同的trade？

订单明细信息接口/linear-swap-api/v1/swap_order_detail返回的的字段id是全局唯一的交易标识。如果一个maker单，分多次match掉的话是每次推送只推match的部分，撮合一笔推送一笔。

### Q4: USDT本位永续合约交易全链路延时多少？

目前USDT本位永续合约全链路(从开始下单到订单的订单状态可以查询)正常情况下大约在30-50MS左右,来行情时延迟会比平时大，可能会在秒级别。

### Q5: API接口返回Connection Reset 或者 Max retris 或者 Timed out 是什么原因？

出现连接重置或者网络超时，一般是网络不稳定导致，可以尝试将服务器放置在AWS东京C区，并使用api.hbdm.vn来尝试，可以有效减少网络超时等错误。

### Q6: API接口下单时出错没有order_id如何来查询订单状态？

如果由于网络原因等API下单超时或者失败，没有返回order_id，可以通过下单时加入client_order_id自定义订单号来进行查询订单状态。

### Q7: WS 订阅私有账户，订单或者仓位一段时间，连接断开如何办？

WS订阅私有账户，订单，仓位时，请注意也要定时维护好心跳，与市场行情的心跳格式不同，详情请参照菜单《Websocket心跳以及鉴权接口》里的订单推送心跳。同时如果连接断开，请做好重连逻辑。

### Q8: 合约资产接口中的“获取合约订单信息”的订单状态1和2都是准备提交有什么不同？3已提交又是什么？

1是准备提交，2是定序的提交，是内部流程的提交。可以认为已经被系统接受了，在系统的流程中。3是已委托到市场。

### Q9: API有获取总资产BTC的接口吗？

没有的。

### Q10: API撤单成功为什么查询订单却是成交？

请注意撤单成功或者下单成功只代表您撤单命令或者下单命令的成功，并不代表订单已经撤销，您可以通过该接口/linear-swap-api/v1/swap_order_info去查询订单状态。

### Q11: API查询订单状态为10是否一定失败？

通过/linear-swap-api/v1/swap_order_info查询订单状态，如果status为10，表示订单失败，不会成功。

### Q12: API一般从撤单开始到撤单成功需要多久？

撤单命令执行成功一般几十ms，实际撤单状态要查询订单状态/linear-swap-api/v1/swap_order_info获取。

### Q13: 获取历史强平订单的方法？

需要获取历史强平订单，可以通过：获取合约历史委托（/linear-swap-api/v1/swap_hisorders【逐仓】或/linear-swap-api/v1/swap_cross_hisorders【全仓】）、获取历史成交记录（/linear-swap-api/v1/swap_matchresults【逐仓】或/linear-swap-api/v1/swap_cross_matchresults【全仓】）这两个接口中的返回字段order_source(订单来源)来判断，当order_source返回的为“risk”说明这个订单就是被强平的订单。


## 错误码相关

### Q1: 1030错误是什么原因？

如果您出现比如查询订单或者下单时遇到：{"status":"error","err_code":1030,"err_msg":"Abnormal service. Please try again later.","ts":1588093883199}类似错误，说明您的输入的请求参数值或者类型不对，请打印出您的request请求body及完整URL参数，并请一一核对对应API文档接口参数。常见的比如volume张数必须是整数。

### Q2: 1048错误是什么原因？

如果您出现{'index': 1, 'err_code': 1048, 'err_msg': 'Insufficient close amount available. '}类似错误，说明此时可平仓量不足，您平仓时需查询目前已有的仓位张数再去平仓。

### Q3: API返回1032错误码是什么原因？

1032代表您的访问次数超出限制，币本位永续合约、交割合约、期权合约和USDT本位永续合约都分开限制频率，请查看合约交易接入说明中的访问次数限制，并且可以在api接口response中的header打印当前的频率限制次数来看是否超出限制频率。建议加大请求间隔延时避免超出限制频率。

## 全仓模式和逐仓模式的区别与使用

1、全仓模式下，全仓账户中的USDT会为每个品种合约的仓位提供担保，即全仓下所有品种合约的仓位共享一个账户权益，账户中的盈亏、占用担保资产、担保资产率等数据合并计算；逐仓模式下，USDT本位永续合约各品种合约的账户权益单独计算各品种合约下的仓位担保资产，盈亏互不影响。

2、全仓模式与逐仓模式使用不同的保证金账户，资产互相独立，可同时进行两个模式的交易，也可同时拥有两个模式的仓位。例如在BTC-USDT合约市场下，全仓模式交易的保证金账户为USDT，而逐仓模式交易的保证金账户为BTC-USDT。

3、API用户可通过API接口【获取合约信息：/linear-swap-api/v1/swap_contract_info】的support_margin_mode字段（合约支持的保证金模式），来查看合约是否支持全仓模式或逐仓模式。

4、API接口分为三种模式类型，【全仓】、【逐仓】和【通用】，这三个模式类型标注在API接口名称以及接口列表上。其中【全仓】表示该API接口仅支持全仓模式使用，【逐仓】表示该API接口仅支持逐仓模式调用，【通用】则表示该API接口不区分全仓和逐仓，即逐仓模式和全仓模式均可调用。

## 如何更有效的解决问题

  您在反馈API错误时，需要附上您的请求URL，请求request的原始的完整body以及完整请求URL参数，服务器的回复response的原始完整log。如果是websocket订阅，需要您提供订阅的地址，订阅的主题，server推送的原始完整log。

  如果是订单相关问题，在使用API订单查询接口/linear-swap-api/v1/swap_order_info请求后保留返回的完整log，并提供您的UID以及订单号。


# 合约市场行情接口

## 【通用】获取合约信息 

###  示例

- GET `/linear-swap-api/v1/swap_contract_info`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_contract_info?contract_code=BTC-USDT"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

###  请求参数

| 参数名称      | 是否必须 | 类型   | 描述     | 取值范围                                   |
| ------------- | -------- | ------ | -------- | ------------------------------------------ |
| contract_code | false    | string | 合约代码，不填查询所有合约 | BTC-USDT  |
| support_margin_mode | false | string | 合约支持的保证金模式  | cross：仅支持全仓模式；isolated：仅支持逐仓模式；all：全逐仓都支持  |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "contract_size": 0.001,
            "price_tick": 0.1,
            "delivery_time": "",
            "create_date": "20201110",
            "contract_status": 1,
            "settlement_date": "1609782000000",
            "support_margin_mode": "all"
        }
    ],
    "ts": 1603694455082
}
```

###  返回参数

| 参数名称 | 是否必须 | 类型 | 描述  | 取值范围 |
| -------------------- | ---- | ------- | ---------------- | ---------------------------------------- |
| status  | true | string  | 请求处理结果 | "ok" , "error"  |
| \<data\> |   true   |  object array   |   |   |
| symbol  | true | string  | 品种代码  | "BTC","ETH"...   |
| contract_code   | true | string  | 合约代码 |  "BTC-USDT" ...   |
| contract_size  | true | decimal | 合约面值，即1张合约对应多少标的币种（如BTC-USDT合约则面值单位就是BTC） | 0.1，0.01... |
| price_tick  | true | decimal | 合约价格最小变动精度 | 0.001, 0.01... |
| settlement_date  | true | string  | 合约下次结算时间    | 时间戳，如"1490759594752"  |
| delivery_time	  | true | string  | 交割时间（合约无需交割时，该字段值为空字符串），单位：毫秒   |  |
| create_date   | true | string  | 合约上市日期    | 如"20180706" |
| contract_status      | true | int     | 合约状态  | 合约状态: 0:已下市、1:上市、2:待上市、3:停牌，4:待开盘、5:结算中、6:交割中、7:结算完成、8:交割完成 |
| support_margin_mode | true | string | 合约支持的保证金模式  | cross：全仓模式；isolated：逐仓模式；all：全逐仓都支持 |
| \</data\>   |      |         |        |       |
| ts     | true | long    | 响应生成时间点，单位：毫秒    |     |   

## 【通用】获取合约指数信息

###  示例

- GET `/linear-swap-api/v1/swap_index`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_index?contract_code=BTC-USDT"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

###  请求参数

| 参数名称  | 是否必须 | 类型 | 描述  | 取值范围 |
| ------------- | ------ | ----- | ---------------------------------------- | ---- |
| contract_code | false | string | 指数代码 | "BTC-USDT","ETH-USDT"...    |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "index_price": 13076.329865680000000000,
            "index_ts": 1603694592011,
            "contract_code": "BTC-USDT"
        }
    ],
    "ts": 1603694596400
}
```

###  返回参数

| 参数名称   | 是否必须 | 类型      | 描述   | 取值范围           |
| -------------------- | ---- | ------- | ------------- | -------------- |
| status               | true | string  | 请求处理结果        | "ok" , "error" |
| \<data\> |   true   |   object array      |    |       |
| contract_code    | true | string  | 指数代码     | "BTC-USDT","ETH-USDT"... |
| index_price    | true | decimal | 指数价格    |                |
| index_ts   | true | long    | 响应生成时间点，单位：毫秒 |     |
| \</data\>   |      |         |        |                |
| ts   | true | long    | 时间戳，单位：毫秒     |                |

## 【通用】获取合约最高限价和最低限价

###  示例

- GET `/linear-swap-api/v1/swap_price_limit`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_price_limit?contract_code=BTC-USDT"

```
#### 备注
 - 该接口支持全仓模式和逐仓模式

###  请求参数

| 参数名称  | 是否必须 | 类型 | 描述  | 取值范围 |
| ------------- | ------ | ----- | ---------------------------------------- | ---- |
| contract_code | true |  string | 合约代码 |    BTC-USDT    |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "high_limit": 13596.800000000000000000000000000000000000,
            "low_limit": 12550.900000000000000000000000000000000000
        }
    ],
    "ts": 1603694645979
}
```

###  返回参数

| 参数名称   | 是否必须 | 类型      | 描述   | 取值范围              |
| -------------------- | ---- | ------- | ------------- | ---------------------------------------- |
| status  | true | string  | 请求处理结果        | "ok"  |
| \<data\> |   true   |  object array       |         |    |
| symbol   | true | string  | 品种代码          | "BTC","ETH" ...   |
| contract_code        | true | string  | 合约代码          | 如 "BTC-USDT" ...    |
| high_limit           | true | decimal | 最高买价          |   |
| low_limit            | true | decimal | 最低卖价          |  |
| \<data\>   |      |         |     |   |
| ts                   | true | long    | 响应生成时间点，单位：毫秒 |  |

## 【通用】获取当前可用合约总持仓量 

###  示例

- GET `/linear-swap-api/v1/swap_open_interest`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_open_interest?contract_code=BTC-USDT"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

###  请求参数

| 参数名称  | 是否必须 | 类型 | 描述  | 取值范围 |
| ------------- | ------ | ----- | ---------------------------------------- | ---- |
| contract_code | false |  string | 合约代码 |    "BTC-USDT",不填查询所有合约|

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "volume": 1489,
            "amount": 1.489,
            "symbol": "BTC",
            "value": 44670,
            "contract_code": "BTC-USDT",
            "trade_amount": 38.88,
            "trade_volume": 3888,
            "trade_turnover": 1030337.082
        }
    ],
    "ts": 1603694760141
}
```

###  返回参数

| 参数名称    | 是否必须 | 类型      | 描述            | 取值范围  |
| -------------------- | ---- | ------- | ------------- | ---------------------------------------- |
| status    | true | string  | 请求处理结果        | "ok" , "error"      |
| \<data\>|    true  |   object array      |               |   |
| symbol     | true | string  | 品种代码          | "BTC", "ETH" ...  |
| contract_code        | true | string  | 合约代码          | "BTC-USDT" ...  |
| amount               | true | decimal | 持仓量(币)，单边数量       | |
| volume               | true | decimal | 持仓量(张)，单边数量        | |
| value               | true | decimal | 总持仓额（单位为合约的计价币种，如USDT）      | |
| trade_amount               | true | decimal | 最近24小时成交量（币）（当前时间-24小时）,值是买卖双边之和	      | |
| trade_volume               | true | decimal | 最近24小时成交量（张）（当前时间-24小时）,值是买卖双边之和   | |
| trade_turnover               | true | decimal | 最近24小时成交额	（当前时间-24小时）,值是买卖双边之和       | |
| \</data\>   |      |         |       ||
| ts                   | true | long    | 响应生成时间点，单位：毫秒 | |

#### 备注

- 持仓量（币）= 持仓量（张）*合约面值
- 总持仓额 = 持仓量（张）* 合约面值 * 最新价 

## 【通用】获取行情深度数据

###  示例

- GET `/linear-swap-ex/market/depth`

```shell

curl "https://api.hbdm.com/linear-swap-ex/market/depth?contract_code=BTC-USDT&type=step0"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

###  请求参数

| 参数名称  | 是否必须 | 类型 | 描述  | 取值范围 |
| ------------- | ------ | ----- | ---------------------------------------- | ---- |
| contract_code | true <img width=250/> |  string <img width=250/> | 合约代码  <img width=250/>  | "BTC-USDT" ...  |
| type   | true |  string| 深度类型 |  (150档数据)  step0, step1, step2, step3, step4, step5, step14, step15（合并深度1-5,14-15）；step0时，不合并深度, (20档数据)  step6, step7, step8, step9, step10, step11, step12, step13（合并深度7-13）；step6时，不合并深度     |

>tick 说明:

```
    "tick": {
      "id": 消息id.
      "ts": 消息生成时间，单位：毫秒.
      "bids": 买盘,[price(挂单价), vol(此价格挂单张数)], //按price降序.
      "asks": 卖盘,[price(挂单价), vol(此价格挂单张数)]  //按price升序.
      "ch": 数据所属的 channel,
      "mrid": 订单ID,
      "ts": 时间戳,
      "version": 版本
    }
```

> Response:

```json

{
    "ch": "market.BTC-USDT.depth.step0",
    "status": "ok",
    "tick": {
        "asks": [
            [
                13084.2,
                168
            ],
            [
                13085.6,
                1
            ]
        ],
        "bids": [
            [
                13084,
                38
            ],
            [
                13069.9,
                1
            ]
        ],
        "ch": "market.BTC-USDT.depth.step0",
        "id": 1603694838,
        "mrid": 131471527,
        "ts": 1603694838167,
        "version": 1603694838
    },
    "ts": 1603694838240
}
    
```

###  返回参数

| 参数名称   | 是否必须 | 数据类型   | 描述  | 取值范围           |
| ------ | ---- | ------ | --------------------------------------- | -------------- |
| ch     | true | string | 数据所属的 channel，格式： market.period         |                |
| status | true | string | 请求处理结果                                  | "ok" , "error" |
| \<tick\> |  true    |   object     |               |                |
| asks   | true | array | 卖盘,[price(挂单价), vol(此价格挂单张数)], 按price升序 |                |
| bids   | true | array | 买盘,[price(挂单价), vol(此价格挂单张数)], 按price降序 |                |
| ch     | true | string | 数据所属的 channel，格式： market.period         |                |
| id     | true | long | 消息id        |                |
| mrid   | true | long | 订单ID                                    |                |
| ts   | true | long | 消息生成时间，单位：毫秒.  |                |
| version   | true | long | 版本                                    |                |
| \</tick\>            |      |        |               |                |
| ts     | true | long | 响应生成时间点，单位：毫秒 |                |


### 备注

- 合并深度仅改变显示方式，不改变实际成交价格。

- step1至step5, step14, step15是进行了深度合并后的150档深度数据，step7至step13是进行了深度合并后的20档深度数据，对应精度如下：

| Depth 类型 | 精度 |
|----|----|
|step1、step7|0.00001|
|step2、step8|0.0001|
|step3、step9|0.001|
|step4、step10|0.01|
|step5、step11|0.1|
|step14、step12|1|
|step15、step13|10|

## 【通用】获取K线数据

###  示例

- GET `/linear-swap-ex/market/history/kline`

```shell

curl "https://api.hbdm.com/linear-swap-ex/market/history/kline?contract_code=BTC-USDT&period=1day&from=1587052800&to=1591286400"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

###  请求参数

| 参数名称   | 是否必须 | 类型      | 描述    | 取值范围 |
| ------ | ---- | ------- | ---- | ---------------------------------------- |
| contract_code | true | string  | 合约代码 |  "BTC-USDT" ...  |
| period | true | string  | K线类型   | 1min, 5min, 15min, 30min, 60min,4hour,1day,1week,1mon |
| size   | false | int | 获取数量，默认150 |  [1,2000]  |
| from   | false | long | 开始时间戳 10位 单位S |   |
| to   | false | long | 结束时间戳 10位 单位S |  |

### 备注

- 1、size与from&to 必填其一，若全不填则返回空数据。
- 2、如果填写from，也要填写to。最多可获取连续两年的数据。
- 3、如果size、from、to 均填写，会忽略from、to参数。

> Data说明：

```

"data": [
  {
    "id": K线id,
    "vol": 成交量(张)，买卖双边成交量之和,
    "count": 成交笔数,
    "open": 开盘价,
    "close": 收盘价,当K线为最晚的一根时，是最新成交价
    "low": 最低价,
    "high": 最高价,
    "amount": 成交量(币), 即 sum(每一笔成交量(张)*单张合约面值/该笔成交价),
    "trade_turnover": 成交额，即 sum（每一笔成交张数 * 合约面值 * 成交价格）
   }
]

```

> Response:

```json

{
    "ch": "market.BTC-USDT.kline.1min",
    "data": [
        {
            "amount": 0.004,
            "close": 13076.8,
            "count": 1,
            "high": 13076.8,
            "id": 1603695060,
            "low": 13076.8,
            "open": 13076.8,
            "trade_turnover": 52.3072,
            "vol": 4
        }
    ],
    "status": "ok",
    "ts": 1603695099234
}
```

###  返回参数

| 参数名称   | 是否必须 | 数据类型   | 描述                              | 取值范围           |
| ------ | ---- | ------ | ------------------------------- | -------------- |
| ch     | true | string | 数据所属的 channel，格式： market.period |                |
| \<data\> |   true   |    object array    |               |                |
| id     | true | long | K线ID,也就是K线时间戳，K线起始时间    |                |
| vol     | true | decimal | 成交量(张)。 值是买卖双边之和 |                |
| count     | true | decimal | 成交笔数。 值是买卖双边之和 |                |
| open     | true | decimal | 开盘价        |                |
| close     | true | decimal | 收盘价,当K线为最晚的一根时，是最新成交价        |                |
| low     | true | decimal | 最低价        |                |
| high     | true | decimal | 最高价        |                |
| amount     | true | decimal | 成交量(币), 即 (成交量(张)*单张合约面值)。 值是买卖双边之和 |                |
| trade_turnover     | true | decimal | 成交额，即 sum（每一笔成交张数\*合约面值\*成交价格）。 值是买卖双边之和  |                |
| \</data\>            |      |        |               |                |
| status | true | string | 请求处理结果                          | "ok" , "error" |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                |


## 【通用】获取标记价格的K线数据

 - GET `/index/market/history/linear_swap_mark_price_kline`

#### 备注：
 - 该接口支持全仓模式和逐仓模式。

### 请求参数：
| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约代码         |         | "BTC-USDT","ETH-USDT"...                           |
| period          | true     | string  | K线类型               |         | 1min, 5min, 15min, 30min, 60min,4hour,1day, 1week,1mon     |
| size  | true     | int    | K线获取数量     |  | [1,2000] |

#### 备注：

- 最多一次2000条数据
- 入参大小写不敏感，均支持

> Response：

```json
{
    "ch": "market.BTC-USDT.mark_price.5min",
    "data": [
        {
            "amount": "0",
            "close": "31078.68",
            "count": "0",
            "high": "31078.68",
            "id": 1611105300,
            "low": "31078.68",
            "open": "31078.68",
            "trade_turnover": "0",
            "vol": "0"
        },
        {
            "amount": "0",
            "close": "31078.68",
            "count": "0",
            "high": "31078.68",
            "id": 1611105600,
            "low": "31078.68",
            "open": "31078.68",
            "trade_turnover": "0",
            "vol": "0"
        }
    ],
    "status": "ok",
    "ts": 1611106791703
}
```

### 返回参数：
| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| ch     | true | string | 数据所属的 channel，格式： market.period |                | |
| \<data\> |   true   |    object array    |               |                | |
| id     | true | long | k线id        |                | |
| vol     | true | string | 成交量(张)，数值为0        |                | |
| count     | true | string | 成交笔数，数值为0        |                | |
| open     | true | string | 开盘值        |                | |
| close     | true | string | 收盘值        |                | |
| low     | true | string | 最低值        |                | |
| high     | true | string | 最高值        |                | |
| amount     | true | string | 成交量(币), 数值为0        |                | |
| trade_turnover     | true | string | 成交额, 数值为0        |                | |
| \</data\>            |      |        |               |                | |
| status | true | string | 请求处理结果                          | "ok" , "error" | |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | |


## 【通用】获取聚合行情

###  示例

- GET `/linear-swap-ex/market/detail/merged`

```shell

curl "https://api.hbdm.com/linear-swap-ex/market/detail/merged?contract_code=BTC-USDT"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

###  请求参数

| 参数名称   | 是否必须 | 类型     | 描述  | 取值范围 |
| ------ | ---- | ------ | ---------------------------------------- | ---- |
| contract_code | true | string | 合约代码 | "BTC-USDT" ...   |

>tick说明:

```

    "tick": {
      "id": K线id,
      "vol": 成交量（张），买卖双边成交量之和,
      "count": 成交笔数,
      "open": 开盘价,
      "close": 收盘价,当K线为最晚的一根时，是最新成交价
      "low": 最低价,
      "high": 最高价,
      "amount": 成交量(币), 即 sum(每一笔成交量(张)*单张合约面值/该笔成交价)
      "bid": [买1价,买1量(张)],
      "ask": [卖1价,卖1量(张)],
        "trade_turnover": 成交额，即 sum（每一笔成交张数 * 合约面值 * 成交价格）
     }
     
```

> Response:

```json

{
    "ch": "market.BTC-USDT.detail.merged",
    "status": "ok",
    "tick": {
        "amount": "12.526",
        "ask": [
            13084.2,
            131
        ],
        "bid": [
            13082.9,
            38
        ],
        "close": "13076.8",
        "count": 2920,
        "high": "13205.3",
        "id": 1603695162,
        "low": "12877.5",
        "open": "12916.2",
        "trade_turnover": "163247.3982",
        "ts": 1603695162580,
        "vol": "12526"
    },
    "ts": 1603695162580
}
    
```

###  返回参数

| 参数名称   | 是否必须 | 数据类型   | 描述  | 取值范围           |
| ------ | ---- | ------ | ---------------------------------------- | -------------- |
| ch     | true | string | 数据所属的 channel，格式： market.$contract_code.detail.merged |                |
| status | true | string | 请求处理结果     | "ok" , "error" |
| \<tick\> |true  | object |  开盘价和收盘价（从当天零点(UTC+8)开始）         |                |
| id   | true | long | K线ID,也就是K线时间戳     |
| amount   | true | string | 成交量(币), 即 (成交量(张)*单张合约面值)（最近24（当前时间-24小时）小时成交量币）。 值是买卖双边之和 |                |
| ask   | true | array | [卖1价,卖1量(张)] |                |
| bid   | true | array | [买1价,买1量(张)] |                |
| open     | true | string | 开盘价     |                |
| close     | true | string | 收盘价,当K线为最晚的一根时，是最新成交价       |                |
| count     | true | decimal | 成交笔数（当前时间-24小时）小时成交笔数）。 值是买卖双边之和  |                |
| high   | true | string | 最高价                                    |                |
| low   | true | string | 最低价  |                |
| vol   | true | string | 成交量（张），买卖双边成交量之和 （最近24（当前时间-24小时）小时成交量张）。 值是买卖双边之和  |                |
| trade_turnover     | true | string | 成交额，即 sum（每一笔成交张数 \* 合约面值 \* 成交价格）（当前时间-24小时）小时成交额）。 值是买卖双边之和 |                |
| ts   | true | long | 时间戳   |                |
| \</tick\>            |      |        |               |                |
| ts     | true | long | 响应生成时间点，单位：毫秒                            |                |


## 【通用】批量获取聚合行情

 - GET `/linear-swap-ex/market/detail/batch_merged`

### 请求参数

| 参数名称   | 是否必须 | 类型     | 描述  | 取值范围 |
| ------ | ---- | ------ | ---------------------------------------- | ---- |
| contract_code | false | string | 合约代码，不填返回全部合约的聚合行情 | "BTC-USDT" ...   |

#### 备注

 - 该接口支持全仓模式和逐仓模式。
 - 该接口更新频率为50ms

> Response:

```json
{
    "status":"ok",
    "ticks":[
        {
            "id":1611109206,
            "ts":1611109206797,
            "ask":[
                3,
                15
            ],
            "bid":[
                2.5,
                1
            ],
            "contract_code":"EOS-USDT",
            "open":"2.5",
            "close":"2.5",
            "low":"2.5",
            "high":"2.5",
            "amount":"0.4",
            "count":2,
            "vol":"4",
            "trade_turnover":"1.1"
        }
    ],
    "ts":1611109206830
}
```

###  返回参数

| 参数名称   | 是否必须 | 数据类型   | 描述  | 取值范围           |
| ------ | ---- | ------ | ---------------------------------------- | -------------- |
| status | true | string | 请求处理结果     | "ok" , "error" |
| \<ticks\> |true  |  object array |           |                |
| contract_code   | true | string  | 合约代码 | "BTC-USDT" ...  |
| id   | true | long | K线id |                |
| amount   | true | string | 成交量(币)    |                |
| ask   | true | array | [卖1价,卖1量(张)] |                |
| bid   | true | array | [买1价,买1量(张)] |                |
| open     | true | string | 开盘价     |                |
| close     | true | string | 收盘价,当K线为最晚的一根时，是最新成交价       |                |
| count     | true | decimal | 成交笔数       |                |
| high   | true | string | 最高价                                    |                |
| low   | true | string | 最低价  |                |
| vol   | true | string | 成交量（张），买卖双边成交量之和                                    |                |
| trade_turnover     | true | string | 成交额       |                |
| ts   | true | long | 时间戳   |                |
| \</ticks\>            |      |        |               |                |
| ts     | true | long | 响应生成时间点，单位：毫秒                            |                |


## 【通用】获取市场最近成交记录

###  示例

- GET `/linear-swap-ex/market/trade`

```shell

curl "https://api.hbdm.com/linear-swap-ex/market/trade?contract_code=BTC-USDT"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

###  请求参数

| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围                                     |
| ------ | ---- | ------ | ---- |---------------------------------------- |
| contract_code | true | string | 合约代码 |  "BTC-USDT" ...  |

>Tick说明：

```
    "tick": {
      "id": 订单唯一id（品种唯一）,
      "ts": 最新成交时间,
      "data": [
        {
                  "id": 成交唯一id（品种唯一）,
                  "price": 成交价钱,
                  "amount": 成交量(张)，买卖双边成交量之和,
                  "direction": 主动成交方向,
                  "ts": 成交时间
        }
      ]
    }
```


> Response:

```json

{
    "ch": "market.BTC-USDT.trade.detail",
    "status": "ok",
    "tick": {
        "data": [
            {
                "amount": "6",
                "ts": 1603695230083,
                "id": 1314755250000,
                "price": "13083",
                "direction": "buy"
            }
        ],
        "id": 1603695235127,
        "ts": 1603695235127
    },
    "ts": 1603695235127
}
    
```

###  返回参数

| 参数名称   | 是否必须 | 类型     | 描述  | 取值范围         |
| ------ | ---- | ------ | ---------------------------------------- |------------ |
| ch     | true | string | 数据所属的 channel，格式： market.$symbol.trade.detail |      |
| status | true | string |     | "ok","error" |
| \<tick\>    | true | object |           |      |
| id     | true | long | 订单唯一id（品种唯一）       |      |
| ts     | true | long | 最新成交时间       |      |
| \<data\>    | true | object array |        |      |
| amount     | true | string | 成交量(张)。 值是买卖双边之和 |      |
| direction     | true | string | 主动成交方向       |      |
| id     | true | long | 成交唯一id（品种唯一）      |      |
| price     | true | string | 成交价       |      |
| ts     | true | long | 成交时间       |      |
| \</data\>    |  |  |              |      |
| \</tick\>    |  |  |              |      |
| ts     | true | long | 发送时间       |      |

## 【通用】批量获取最近的交易记录

###  示例

- GET `/linear-swap-ex/market/history/trade`

```shell

curl "https://api.hbdm.com/linear-swap-ex/market/history/trade?contract_code=BTC-USDT&size=100"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

###  请求参数：

| 参数名称   | 是否必须  | 数据类型   | 描述    | 取值范围   |
| ------ | ----- | ------ | --------- | ---------------------------------------- |
| contract_code | true  | string | 合约代码      |    "BTC-USDT" ... |
| size   | true | int | 获取交易记录的数量，默认1 |  [1, 2000]   |

> data说明：

```
    "data": {
         "id": 订单唯一id（品种唯一）,
      "ts": 最新成交时间,
      "data": [
        {
          "id": 成交唯一id（品种唯一）,
          "price": 成交价,
          "amount": 成交量(张)，买卖双边成交量之和,
          "direction": 主动成交方向,
          "ts": 成交时间
        }
      ]
    }
    
```

> Response:

```json

{
    "ch": "market.BTC-USDT.trade.detail",
    "data": [
        {
            "data": [
                {
                    "amount": 2,
                    "direction": "buy",
                    "id": 1314767870000,
                    "price": 13081.3,
                    "ts": 1603695383124
                }
            ],
            "id": 131476787,
            "ts": 1603695383124
        }
    ],
    "status": "ok",
    "ts": 1603695388965
}
    
```

###  返回参数

| 参数名称   | 是否必须 | 数据类型   | 描述  | 取值范围         |
| ------ | ---- | ------ | ---------------------------------------- | ------------ |
| ch     | true | string | 数据所属的 channel，格式： market.$contract_code.trade.detail |              |
| \<data\> | true | object array |           |      |       |
| \<data\>  | true | object array |           |      |       |
| amount     | true | decimal | 成交量(张)。 值是买卖双边之和 |      |            |
| direction     | true | string | 主动成交方向       |      |            |
| id     | true | long | 成交唯一id（品种唯一）     |      |            |
| price     | true | decimal | 成交价格       |      |            |
| ts     | true | long | 成交时间       |      |            |
| \</data\>    |  |  |              |      |            |
| id     | true | long | 订单唯一id（品种唯一）    |      |            |
| ts     | true | long | 最新成交时间       |      |            |
| \</data\>    |  |  |              |      |            |
| status | true | string |                                          | "ok"，"error" |
| ts     | true | long | 响应生成时间点，单位：毫秒                            |              |

## 【通用】查询合约风险准备金余额和预估分摊比例

- GET `/linear-swap-api/v1/swap_risk_info`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_risk_info?contract_code=BTC-USDT"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围  |
| ------ | ----- | ------ | ---- | ---------------------------- | ---- |
| contract_code | false | string | 合约代码 |   "BTC-USDT",不填返回所有合约  |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "contract_code": "BTC-USDT",
            "insurance_fund": 499937.059826600000000000,
            "estimated_clawback": 0
        }
    ],
    "ts": 1603695455942
}

```

### 返回参数

| 参数名称   | 是否必须 | 类型      | 描述            | 取值范围           |
| ------------------ | ---- | ------- | ------------- | -------------- |
| status             | true | string  | 请求处理结果        | "ok" , "error" |
| ts                 | true | long    | 响应生成时间点，单位：毫秒 |                |
|\<data\>        |   true   |   object array      |               |                |
| estimated_clawback | true | decimal | 预估分摊比例        |                |
| insurance_fund     | true | decimal | 风险准备金余额       |                |
| contract_code             | true | string  | 合约代码          | "BTC-USDT" ... |
| \</data\>          |      |         |               |                |

## 【通用】查询合约风险准备金余额历史数据

- GET `/linear-swap-api/v1/swap_insurance_fund`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_insurance_fund?contract_code=BTC-USDT"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围           |
| ------ | ---- | ------ | ---- | -------------- |
| contract_code | true | string | 合约代码 |"BTC-USDT" ...   |
|page_index | false | int  |页码，不填默认第1页|  1|
|page_size  | false | int  |不填默认100，不得多于100|100 |

> Response:

```json

{
    "status": "ok",
    "data": {
        "total_page": 5,
        "current_page": 1,
        "total_size": 5,
        "symbol": "BTC",
        "contract_code": "BTC-USDT",
        "tick": [
            {
                "insurance_fund": 499937.059826600000000000,
                "ts": 1603612800000
            }
        ]
    },
    "ts": 1603695552425
}

```

### 返回参数

| 参数名称  | 是否必须 | 类型      | 描述    | 取值范围           |
| -------------- | ---- | ------- | ------------- | -------------- |
| status         | true | string  | 请求处理结果        | "ok" , "error" |
| ts             | true | long    | 响应生成时间点，单位：毫秒 |     |
| \<data\>       |   true   |   object      |               | 字典数据           |
| symbol         | true | string  | 品种代码          | "BTC","ETH"... |
| contract_code         | true | string  | 合约代码          |   "BTC-USDT" ... |
| \<tick\>  |   true  |  object array       |     |                |
| insurance_fund | true | decimal | 风险准备金余额       |                |
| ts             | true | long    | 数据时间点，单位：毫秒   |       |
| \</tick\>      |      |         |               |                |
|total_page|	true	|int	|总页数	| |
|current_page|	true|	int	|当前页	| |
|total_size|	true	|int	|总条数| |
| \</data\>      |      |         |               |                |

## 【逐仓】查询平台阶梯调整系数

- GET `/linear-swap-api/v1/swap_adjustfactor`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_adjustfactor?contract_code=BTC-USDT"

```

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围           |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | false | string | 合约代码 |  "BTC-USDT"... ,如果缺省，默认返回所有合约 |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "margin_mode": "isolated",
            "list": [
                {
                    "lever_rate": 125,
                    "ladders": [
                        {
                            "ladder": 0,
                            "min_size": 0,
                            "max_size": 8999,
                            "adjust_factor": 0.650000000000000000
                        },
                        {
                            "ladder": 1,
                            "min_size": 9000,
                            "max_size": 89999,
                            "adjust_factor": 0.800000000000000000
                        },
                        {
                            "ladder": 2,
                            "min_size": 90000,
                            "max_size": null,
                            "adjust_factor": 0.850000000000000000
                        }
                    ]
                }
            ]
        }
    ],
    "ts": 1603695606565
}

```

### 返回参数

| 参数名称     | 是否必须 | 类型      | 描述     | 取值范围           |
| ----------------- | ---- | ------- | ------------- | -------------- |
| status            | true | string  | 请求处理结果        | "ok" , "error" |
| ts                | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>          |  true    |   object array     |               |          |
| symbol            | true | string  | 品种代码           | "BTC","ETH"...|
| contract_code            | true | string  |   合约代码       |  "BTC-USDT" ... |
| margin_mode            | true | string  |   保证金模式	       |  	isolated：逐仓模式 |
| \<list\>          |   true   |   object array   |         |                |
| lever_rate        | true | decimal | 杠杆倍数          |                |
| \<ladders\>  |    true  |  object array      |               |                |
| min_size          | true | decimal | 净持仓量的最小值      |                |
| max_size          | true | decimal | 净持仓量的最大值      |                |
| ladder            | true | int     | 档位            |                |
| adjust_factor     | true | decimal | 调整系数          |                |
| \</ladders\> |      |         |           |                |
| \</tick\>         |      |         |         |                |
| \</data\>         |      |         |        |                |

## 【全仓】查询平台阶梯调整系数

 - GET `/linear-swap-api/v1/swap_cross_adjustfactor`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围           |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | false | string | 合约代码 |  "BTC-USDT"... ,如果缺省，默认返回所有合约 |

> Response:

```json

{
    "status":"ok",
    "data":[
        {
            "symbol":"BTC",
            "contract_code":"BTC-USDT",
            "margin_mode":"cross",
            "list":[
                {
                    "lever_rate":1,
                    "ladders":[
                        {
                            "ladder":0,
                            "min_size":0,
                            "max_size":999,
                            "adjust_factor":0.005
                        },
                        {
                            "ladder":1,
                            "min_size":1000,
                            "max_size":9999,
                            "adjust_factor":0.11
                        },
                        {
                            "ladder":2,
                            "min_size":10000,
                            "max_size":19999,
                            "adjust_factor":0.015
                        },
                        {
                            "ladder":3,
                            "min_size":20000,
                            "max_size":29999,
                            "adjust_factor":0.02
                        },
                        {
                            "ladder":4,
                            "min_size":30000,
                            "max_size":null,
                            "adjust_factor":0.025
                        }
                    ]
                }
            ]
        }
    ],
    "ts":1606905299391
}

```

### 返回参数

| 参数名称     | 是否必须 | 类型      | 描述     | 取值范围           |
| ----------------- | ---- | ------- | ------------- | -------------- |
| status            | true | string  | 请求处理结果        | "ok" , "error" |
| ts                | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>          |  true    |   object array     |               |          |
| symbol            | true | string  | 品种代码           | "BTC","ETH"...|
| contract_code            | true | string  |   合约代码       |  "BTC-USDT" ... |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| \<list\>          |   true   |   object array   |         |                |
| lever_rate        | true | decimal | 杠杆倍数          |                |
| \<ladders\>  |    true  |  object array      |               |                |
| min_size          | true | decimal | 净持仓量的最小值      |                |
| max_size          | true | decimal | 净持仓量的最大值      |                |
| ladder            | true | int     | 档位            |   从0档开始             |
| adjust_factor     | true | decimal | 调整系数          |                |
| \</ladders\> |      |         |           |                |
| \</list\>         |      |         |         |                |
| \</data\>         |      |         |        |                |


## 【通用】获取预估结算价

 - GET `/linear-swap-api/v1/swap_estimated_settlement_price`

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | false  | string | 合约代码，不填返回所有合约     |      "BTC-USDT" ...                                        |

> Response

```json
{
    "status": "ok",
    "data": [
        {
            "contract_code": "BTC-USDT",
            "estimated_settlement_price": null,
            "settlement_type": "settlement"
        }
    ],
    "ts": 1609751036345
}
```

### 返回参数

| 参数名称                   | 是否必须 | 类型      | 描述                 | 取值范围                                     |
| ---------------------- | ---- | ------- | ------------------ | ---------------------------------------- |
| status                 | true | string  | 请求处理结果             |                                          |
| \<data\> | true     |  object  array      |                    |                                          |
| contract_code          | true | string  | 合约代码               | "BTC-USDT" ...                          |
| estimated_settlement_price              | true | decimal  |  本期预估结算价/预估交割价（结算类型为交割时为预估交割价；结算时为预估结算价；）  |                                  |
| settlement_type        | true | string | 本期结算类型         |  “delivery”：交割，“settlement”：结算            |
| \</data\>            |      |         |                    |                                          |
| ts                     | true | long    | 接口响应时间（毫秒）                |                                          |

#### 备注
- 结算类型为结算时，预估结算价字段（estimated_settlement_price）在结算前10分钟到结算开始才计算和更新展示，其他时间点（包括结算中）则estimated_settlement_price为空，其他字段正常展示。
- 结算类型为交割时，预估交割价字段（estimated_settlement_price）在交割前10分钟到交割开始才计算和更新展示，其他时间点（包括交割中）则estimated_settlement_price为空，其他字段正常展示。
- 每6秒计算并更新一次预估结算价。


## 【通用】平台持仓量的查询

### 实例

- GET `/linear-swap-api/v1/swap_his_open_interest`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_his_open_interest?contract_code=BTC-USDT&period=60min&amount_type=1"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述     | 取值范围  |
| ------------- | ----- | ------ | ------ | ---------------------------------------- |
| contract_code        | true  | string | 合约代码   | "BTC-USDT" ...                          |
| period        | true  | string | 时间周期类型 | 1小时:"60min"，4小时:"4hour"，12小时:"12hour"，1天:"1day" |
| size          | false | int    | 获取数量   | 默认为：48，取值范围 [1,200]                      |
| amount_type   | true  | int    | 计价单位   | 1:张，2:币                                   |

> Response:

```json

{
    "status": "ok",
    "data": {
        "symbol": "BTC",
        "tick": [
            {
                "volume": 2124.0000000000000000,
                "amount_type": 1,
                "ts": 1603695600000,
                "value": 27771.93720000000000000000000000000000000
            }
        ],
        "contract_code": "BTC-USDT"
    },
    "ts": 1603695899986
}
```

### 返回参数

| 参数名称          | 是否必须 | 类型      | 描述            | 取值范围     |
| ------------- | ---- | ------- | ------------- | ---------------------------------------- |
| status        | true | string  | 请求处理结果        | "ok" , "error"                           |
| ts            | true | long    | 响应生成时间点，单位：毫秒 |                                          |
| \<data\>      |  true    |   object      | 字典数据          |                                          |
| symbol        | true | string  | 品种代码          | "BTC","ETH"...                           |
| contract_code | true | string  | 合约代码          |  "BTC-USDT" ... |
| \<tick\>      |  true    |  object array       |               |                                          |
| volume        | true | decimal | 持仓量。 |                                          |
| amount_type   | true | int     | 计价单位（表示持仓量的计价单位） | 1:张，2:币                                  |
| value               | true | decimal | 总持仓额（单位为合约的计价币种，如USDT）     | |
| ts            | true | long    | 统计时间          |                                          |
| \</tick\>     |      |         |               |  |
| \</data\>     |      |         |               |  |

#### 注意：
  
- 总持仓额 = 持仓量（张）* 合约面值 * 最新价 
- tick字段：数组内的数据按照时间倒序排列；

## 【通用】精英账户多空持仓对比-账户数

- GET `/linear-swap-api/v1/swap_elite_account_ratio`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_elite_account_ratio?contract_code=BTC-USDT&period=5min"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述     | 取值范围  |
| ------------- | ----- | ------ | ------ | ---------------------------------------- |
| contract_code        | true  | string | 合约代码   | "BTC-USDT" ...                          |
| period        | true  | string | 时间周期类型 | 5min, 15min, 30min, 60min,4hour,1day |

> Response:

```json

{
    "status": "ok",
    "data": {
        "list": [
            {
                "buy_ratio": 0.2940,
                "sell_ratio": 0.6760,
                "locked_ratio": 0.0300,
                "ts": 1603591200000
            }
        ],
        "symbol": "BTC",
        "contract_code": "BTC-USDT"
    },
    "ts": 1603696167089
}

```

### 返回参数

| 参数名称   | 是否必须 | 类型      | 描述            | 取值范围           |
| ----------------- | ---- | ------- | ------------- | -------------- |
| status            | true | string  | 请求处理结果        | "ok" , "error" |
| ts                | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>          |  true    |   object      |               |          |
| symbol            | true | string  | 品种代码          | "BTC","ETH"...|
| contract_code            | true | string  | 合约代码          | "BTC-USDT" ...  |
| \<list\>          |   true   |   object array   |         |                |
| buy_ratio        | true | decimal | 净多仓的账户比例          |                |
| sell_ratio        | true | decimal | 净空仓的账户比例          |                |
| locked_ratio        | true | decimal | 锁仓的账户比例          |                |
| ts        | true | long | 生成时间          |                |
| \</list\>         |      |         |         |                |
| \</data\>         |      |         |        |                |

## 【通用】精英账户多空持仓对比-持仓量

- GET `/linear-swap-api/v1/swap_elite_position_ratio`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_elite_position_ratio?contract_code=BTC-USDT&period=1day"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围          |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | true | string | 合约代码 | "BTC-USDT" ...  |
| period | true | string | 周期 | 5min, 15min, 30min, 60min,4hour,1day |

> Response:

```json

{
    "status": "ok",
    "data": {
        "list": [
            {
                "buy_ratio": 0.5000,
                "sell_ratio": 0.5000,
                "ts": 1603591200000
            }
        ],
        "symbol": "BTC",
        "contract_code": "BTC-USDT"
    },
    "ts": 1603696275437
}

```

### 返回参数

| 参数名称              | 是否必须 | 类型      | 描述            | 取值范围           |
| ----------------- | ---- | ------- | ------------- | -------------- |
| status            | true | string  | 请求处理结果        | "ok" , "error" |
| ts                | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>          |  true    |   object      |               |          |
| symbol            | true | string  | 品种代码          | "BTC","ETH"... |
| contract_code            | true | string  | 合约代码          | "BTC-USDT" ... |
| \<list\>          |   true   |   object array   |         |                |
| buy_ratio        | true | decimal | 多仓的总持仓量占比          |                |
| sell_ratio        | true | decimal | 空仓的总持仓量占比          |                |
| ts        | true | long | 生成时间          |                |
| \</list\>         |      |         |         |                |
| \</data\>         |      |         |        |                |

## 【逐仓】查询系统状态

- GET `/linear-swap-api/v1/swap_api_state`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_api_state?contract_code=BTC-USDT"

```

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称  | 是否必须 | 类型 | 描述  | 取值范围 |
| ------------- | ------ | ----- | ---------------------------------------- | ---- |
| contract_code | false | string | 合约代码 |   "BTC-USDT"... ,如果缺省，默认返回所有合约    |


> Response:   


```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT",
            "open": 1,
            "close": 1,
            "cancel": 1,
            "transfer_in": 1,
            "transfer_out": 1,
            "master_transfer_sub": 1,
            "sub_transfer_master": 1,
            "master_transfer_sub_inner_in": 1,
            "master_transfer_sub_inner_out": 1,
            "sub_transfer_master_inner_in": 1,
            "sub_transfer_master_inner_out": 1,
            "transfer_inner_in": 1,
            "transfer_inner_out": 1
        }
    ],
    "ts": 1603696366019
}
```

### 返回参数

| 参数名称   | 是否必须 | 类型     | 描述            | 取值范围           |
| -------------------- | ---- | ------ | ------------- | -------------- |
| status               | true | string | 请求处理结果        | "ok" , "error" |
| ts                   | true | long   | 响应生成时间点，单位：毫秒 |                |
| \<data\> |  true    |  object array      |               |                |
| symbol       | true | string | 品种代码         |   "BTC","ETH"...              |
| contract_code | true | string | 合约代码         |    "BTC-USDT"...  |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如]“BTC-USDT” |
| open       | true | int | 开仓下单权限："1"表示可用，“0”表示不可用         |             |
| close       | true | int | 平仓下单权限："1"表示可用，“0”表示不可用           |          |
| cancel       | true | int | 撤单权限："1"表示可用，“0”表示不可用         |    |
| transfer_in       | true | int | 从币币转入的权限："1"表示可用，“0”表示不可用           |              |
| transfer_out       | true | int | 转出至币币的权限："1"表示可用，“0”表示不可用          |          |
| master_transfer_sub       | true | int | 从母账号划转到子账号的权限："1"表示可用，“0”表示不可用            |              |
| sub_transfer_master       | true | int | 从子账号划转到母账号的权限："1"表示可用，“0”表示不可用         |         |
| master_transfer_sub_inner_in       | true | int | 母账号划转到子账号的转入权限-跨账户："1"表示可用，“0”表示不可用            |              |
| master_transfer_sub_inner_out       | true | int | 母账号划转到子账号的转出权限-跨账户："1"表示可用，“0”表示不可用            |              |
| sub_transfer_master_inner_in       | true | int | 子账号划转到母账号的转入权限-跨账户："1"表示可用，“0”表示不可用         |         |
| sub_transfer_master_inner_out       | true | int | 子账号划转到母账号的转出权限-跨账户："1"表示可用，“0”表示不可用         |         |
| transfer_inner_in       | true | int | 同账号不同保证金账户划转的转入权限："1"表示可用，“0”表示不可用         |         |
| transfer_inner_out       | true | int | 同账号不同保证金账户划转的转出权限："1"表示可用，“0”表示不可用         |         |
| \</data\>            |      |        |               |                |

## 【全仓】查询系统划转权限

 - GET `/linear-swap-api/v1/swap_cross_transfer_state`

#### 备注
 - 该接口仅支持全仓模式。

###  请求参数

| 参数名称  | 是否必须 | 类型 | 描述  | 取值范围 |
| ------------- | ------ | ----- | ---------------------------------------- | ---- |
| margin_account | false | string |  保证金账户，不填则返回所有全仓保证金账户 |   "USDT"，目前只有一个全仓账户（USDT）    |

> Response 

```json

{
    "status": "ok",
    "data": [
        {
            "margin_mode": "cross",
            "margin_account": "USDT",
            "transfer_in": 1,
            "transfer_out": 1,
            "master_transfer_sub": 1,
            "sub_transfer_master": 1,
            "master_transfer_sub_inner_in": 1,
            "master_transfer_sub_inner_out": 1,
            "sub_transfer_master_inner_in": 1,
            "sub_transfer_master_inner_out": 1,
            "transfer_inner_in": 1,
            "transfer_inner_out": 1
        }
    ],
    "ts": 1606905619516
}
```

###  返回参数

| 参数名称   | 是否必须 | 类型     | 描述            | 取值范围           |
| -------------------- | ---- | ------ | ------------- | -------------- |
| status               | true | string | 请求处理结果        | "ok" , "error" |
| ts                   | true | long   | 响应生成时间点，单位：毫秒 |                |
| \<data\> |  true    |  object array      |               |                |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| transfer_in       | true | int | 从币币转入的权限："1"表示可用，“0”表示不可用           |              |
| transfer_out       | true | int | 转出至币币的权限："1"表示可用，“0”表示不可用          |          |
| master_transfer_sub       | true | int | 从母账号划转到子账号的权限："1"表示可用，“0”表示不可用            |              |
| sub_transfer_master       | true | int | 从子账号划转到母账号的权限："1"表示可用，“0”表示不可用         |         |
| master_transfer_sub_inner_in       | true | int | 母账号划转到子账号的转入权限-跨账户："1"表示可用，“0”表示不可用            |              |
| master_transfer_sub_inner_out       | true | int | 母账号划转到子账号的转出权限-跨账户："1"表示可用，“0”表示不可用            |              |
| sub_transfer_master_inner_in       | true | int | 子账号划转到母账号的转入权限-跨账户："1"表示可用，“0”表示不可用         |         |
| sub_transfer_master_inner_out       | true | int | 子账号划转到母账号的转出权限-跨账户："1"表示可用，“0”表示不可用         |         |
| transfer_inner_in       | true | int | 同账号不同保证金账户划转的转入权限："1"表示可用，“0”表示不可用         |         |
| transfer_inner_out       | true | int | 同账号不同保证金账户划转的转出权限："1"表示可用，“0”表示不可用         |         |
| \</data\>            |      |        |               |                |

      

## 【全仓】查询系统交易权限

 - GET `/linear-swap-api/v1/swap_cross_trade_state`

#### 备注
 - 该接口仅支持全仓模式。

###  请求参数

| 参数名称  | 是否必须 | 类型 | 描述  | 取值范围 |
| ------------- | ------ | ----- | ---------------------------------------- | ---- |
| contract_code | false | string | 合约代码 |   "BTC-USDT"... ,如果缺省，默认返回所有支持全仓的合约    |

> Response

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "margin_mode": "cross",
            "margin_account": "USDT",
            "open": 1,
            "close": 1,
            "cancel": 1
        }
    ],
    "ts": 1606905935710
}

```
        
###  返回参数

| 参数名称   | 是否必须 | 类型     | 描述            | 取值范围           |
| -------------------- | ---- | ------ | ------------- | -------------- |
| status               | true | string | 请求处理结果        | "ok" , "error" |
| ts                   | true | long   | 响应生成时间点，单位：毫秒 |                |
| \<data\> |  true    |  object array      |               |                |
| symbol       | true | string | 品种代码         |   "BTC","ETH"...              |
| contract_code | true | string | 合约代码         |    "BTC-USDT"...  |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| open       | true | int | 开仓下单权限："1"表示可用，“0”表示不可用         |             |
| close       | true | int | 平仓下单权限："1"表示可用，“0”表示不可用           |          |
| cancel       | true | int | 撤单权限："1"表示可用，“0”表示不可用         |    |
| \</data\>            |      |        |               |                |       

## 【通用】获取合约的资金费率

- GET `/linear-swap-api/v1/swap_funding_rate`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_funding_rate?contract_code=BTC-USDT"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | true | string | 合约代码 |"BTC-USDT" ...  |

> Response: 

```json

{
    "status": "ok",
    "data": {
        "estimated_rate": "0.000100000000000000",
        "funding_rate": "0.000100000000000000",
        "contract_code": "BTC-USDT",
        "symbol": "BTC",
        "fee_asset": "USDT",
        "funding_time": "1603699200000",
        "next_funding_time": "1603728000000"
    },
    "ts": 1603696494714
}
```

### 返回参数

| 参数名称    | 是否必须 | 类型      | 描述            | 取值范围           |
| ----------------- | ---- | ------- | ------------- | -------------- |
| status            | true | string  | 请求处理结果        | "ok" , "error" |
| ts                | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>          |  true    |   object      |               |          |
| symbol        | true | string | 品种代码          |             |
| contract_code        | true | string | 合约代码          |   "BTC-USDT" ...             |
| fee_asset        | true | string | 资金费币种   |  "USDT"...              |
| funding_time        | true | string |当期资金费率时间        |                |
| funding_rate        | true | string | 当期资金费率          |                |
| estimated_rate        | true | string | 下一期预测资金费率   |                |
| next_funding_time        | true | string | 下一期资金费率时间         |                |
| \</data\>         |      |         |        |                |

## 【通用】获取合约的历史资金费率

- GET `/linear-swap-api/v1/swap_historical_funding_rate`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_historical_funding_rate?contract_code=BTC-USDT"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | true | string | 合约代码 |"BTC-USDT" ...  |
| page_index | false | int | 页码，不填默认第1页 |  |
| page_size | false | int | 不填默认20，不得多于50  |  |

> Response:

```json

{
    "status": "ok",
    "data": {
        "total_page": 14,
        "current_page": 1,
        "total_size": 14,
        "data": [
            {
                "avg_premium_index": "0.000049895833333333",
                "funding_rate": "0.000100000000000000",
                "realized_rate": "0.000100000000000000",
                "funding_time": "1603670400000",
                "contract_code": "BTC-USDT",
                "symbol": "BTC",
                "fee_asset": "USDT"
            }
        ]
    },
    "ts": 1603696680599
}

```

### 返回参数

| 参数名称    | 是否必须 | 类型      | 描述            | 取值范围           |
| ----------------- | ---- | ------- | ------------- | -------------- |
| status            | true | string  | 请求处理结果        | "ok" , "error" |
| ts                | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>          |  true    |   object      |               |          |
| \<data\>          |  true    |   object      |               |          |
| symbol        | true | string | 品种代码          |             |
| contract_code        | true | string | 合约代码          |   "BTC-USDT" ...             |
| fee_asset        | true | string | 资金费币种   |  "USDT"...              |
| funding_time        | true | string |资金费率时间        |                |
| funding_rate        | true | string | 当期资金费率          |                |
| realized_rate        | true | string | 实际资金费率   |                |
| avg_premium_index               | true     | string    | 平均溢价指数           |  |
| \</data\>         |      |         |        |                |
| total_page        | true | int | 总页数   |                |
| current_page        | true | int | 当前页   |                |
| total_size        | true | int | 总条数   |                |
| \</data\>         |      |         |        |                |

## 【通用】获取强平订单

- GET `/linear-swap-api/v1/swap_liquidation_orders`

```shell

curl "https://api.hbdm.com/linear-swap-api/v1/swap_liquidation_orders?contract_code=BTC-USDT&trade_type=0&create_date=90"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | true | string | 合约代码 |"BTC-USDT" ...  |
| trade_type | true | int | 交易类型 | 0:全部,5: 卖出强平,6: 买入强平 |
| create_date | true | int | 日期 | 7，90（7天或者90天） |
| page_index | false | int | 页码,不填默认第1页 | |
| page_size | false | int | 不填默认20，不得多于50    |  |

> Response:

```json

{
    "status": "ok",
    "data": {
        "orders": [
            {
                "contract_code": "BTC-USDT",
                "symbol": "BTC",
                "direction": "sell",
                "offset": "close",
                "volume": 624,
                "price": 16701.4,
                "created_at": 1606380004694,
                "amount": 0.624,
                "trade_turnover": 10421.6736
            }
        ],
        "total_page": 10,
        "current_page": 1,
        "total_size": 10
    },
    "ts": 1603696886350
}

```

### 返回参数

| 参数名称    | 是否必须 | 类型      | 描述            | 取值范围           |
| ----------------- | ---- | ------- | ------------- | -------------- |
| status            | true | string  | 请求处理结果        | "ok" , "error" |
| ts                | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>          |  true    |   object      |               |          |
| \<orders\>          |   true   |   object array   |         |                |
| symbol        | true | string | 品种代码          |             |
| contract_code        | true | string | 合约代码          |   "BTC-USDT" ...             |
| created_at        | true | long | 强平时间   |                |
| direction        | true | string | "buy":买 "sell":卖          |                |
| offset        | true | string | "open":开 "close":平            |                |
| price        | true | decimal | 破产价格   |                |
| volume        | true | decimal | 强平数量（张）         |                |
| amount        | true | decimal | 强平数量（币）         |                |
| trade_turnover        | true | decimal | 强平金额（计价币种）         |                |
| \</orders\>         |      |         |         |                |
| total_page        | true | int | 总页数   |                |
| current_page        | true | int | 当前页   |                |
| total_size        | true | int | 总条数   |                |
| \</data\>         |      |         |        |                |

## 【通用】查询平台历史结算记录

- GET `/linear-swap-api/v1/swap_settlement_records`

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code        | true  | string | 合约代码          | "BTC-USDT","ETH-USDT"...                           |
| start_time   | false  | long    | 起始时间（时间戳，单位毫秒）        |  取值范围：[(当前时间 - 90天), 当前时间] ，默认取当前时间- 90天   |
| end_time   | false  | long    | 结束时间（时间戳，单位毫秒）        | 取值范围：(start_time, 当前时间)，默认取当前时间  |
| page_index        | false  | int |    页码，不填默认第1页       |                        |
| page_size        | false  | int | 页长，不填默认20，不得多于50         |                          |

> Response: 

```json
{
    "status": "ok",
    "data": {
        "total_page": 108,
        "current_page": 1,
        "total_size": 108,
        "settlement_record": [
            {
                "symbol": "BTC",
                "contract_code": "BTC-USDT",
                "settlement_time": 1606377600000,
                "clawback_ratio": 0,
                "settlement_price": 17600.1,
                "settlement_type": "settlement"
            }
        ]
    },
    "ts": 1606383650761
}
```

### 返回参数

| 参数名称                   | 是否必须 | 类型      | 描述                 | 取值范围                                     |
| ---------------------- | ---- | ------- | ------------------ | ---------------------------------------- |
| status            | true | string  | 请求处理结果        | "ok" , "error" |
| ts                | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>          |  true    |   object array    |               |          |
| \<settlement_record\>          |  true    |   object array    |               |          |
| symbol        | true | string | 品种代码          |             |
| contract_code        | true | string | 合约代码          |   "BTC-USDT" ...             |
| settlement_time        | true | long | 结算时间（时间戳，单位毫秒）（当settlement_type为交割时，该时间为交割时间；当settlement_type为结算时，该时间为结算时间；）          |             |
| clawback_ratio        | true | decimal | 分摊比例        |             |
| settlement_price        | true | decimal | 结算价格（当settlement_type为交割时，该价格为交割价格；当settlement_type为结算时，该价格为结算价格；）          |              |
| settlement_type        | true | string | 结算类型         |  “delivery”：交割，“settlement”：结算            |
| \</settlement_record\>         |      |         |         |                |
| total_page        | true | int | 总页数   |                |
| current_page        | true | int | 当前页   |                |
| total_size        | true | int | 总条数   |                |
| \</data\>         |      |         |        |                |

## 【通用】获取合约的溢价指数K线

- GET `/index/market/history/linear_swap_premium_index_kline`

```shell

curl "https://api.hbdm.com/index/market/history/linear_swap_premium_index_kline?contract_code=BTC-USDT&period=1min&size=1"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称    | 是否必须 | 类型 | 描述        | 取值范围                                |
| ----------- | -------- | ------ | ------------- | ---------------------------------------- |
| contract_code      | true     | string | 合约代码         |  "BTC-USDT","ETH-USDT"...                           |
| period          | true     | string  | K线类型               |  1min, 5min, 15min, 30min, 60min,4hour,1day, 1week,1mon     |
| size  | true     | int    | K线获取数量     |   [1,2000] |

> Response:

```json

{
    "ch": "market.BTC-USDT.premium_index.1min",
    "data": [
        {
            "amount": "0",
            "close": "0.0000079166666666",
            "count": "0",
            "high": "0.0000079166666666",
            "id": 1603696920,
            "low": "0.0000079166666666",
            "open": "0.0000079166666666",
            "trade_turnover": "0",
            "vol": "0"
        }
    ],
    "status": "ok",
    "ts": 1603696958348
}

```

### 返回参数

| 参数名称    | 是否必须 |类型 | 描述        |  取值范围                                 |
| ----------- | -------- | ------ | ------------- | ---------------------------------------- |
| ch     | true | string | 数据所属的 channel，格式： market.period |                | 
| \<data\> |   true   |    object array    |               |                | 
| id     | true | long | k线id        |                | 
| vol     | true | string | 成交量(张)，数值为0        |                | 
| count     | true | string | 成交笔数，数值为0        |                | 
| open     | true | string | 开盘值（溢价指数）        |                | 
| close     | true | string | 收盘值（溢价指数）        |                | 
| low     | true | string | 最低值（溢价指数）        |                | 
| high     | true | string | 最高值（溢价指数）        |                | 
| amount     | true | string | 成交量(币), 数值为0        |                | 
| trade_turnover     | true | string | 成交额, 数值为0        |                | 
| \</data\>            |      |        |               |                | 
| status | true | string | 请求处理结果                          | "ok" , "error" | 
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | 

## 【通用】获取实时预测资金费率的K线数据

- GET `/index/market/history/linear_swap_estimated_rate_kline`

```shell

curl "https://api.hbdm.com/index/market/history/linear_swap_estimated_rate_kline?contract_code=BTC-USDT&period=1min&size=1"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称    | 是否必须 | 类型 | 描述        | 默认值 | 取值范围                                |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约代码         |         | "BTC-USDT","ETH-USDT"...                           |
| period          | true     | string  | K线类型               |         | 1min, 5min, 15min, 30min, 60min,4hour,1day, 1week,1mon     |
| size  | true     | int    | K线获取数量     |  | [1,2000] |                                        |

> Response:

```json

{
    "ch": "market.BTC-USDT.estimated_rate.1min",
    "data": [
        {
            "amount": "0",
            "close": "0.0001",
            "count": "0",
            "high": "0.0001",
            "id": 1603697100,
            "low": "0.0001",
            "open": "0.0001",
            "trade_turnover": "0",
            "vol": "0"
        }
    ],
    "status": "ok",
    "ts": 1603697104902
}
```

### 返回参数

| 参数名称    | 是否必须 | 类型 | 描述        | 默认值 | 取值范围                                |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| ch     | true | string | 数据所属的 channel，格式： market.period |                | |
| \<data\> |   true   |    object array    |               |                | |
| id     | true | long | k线id        |                | |
| vol     | true | string | 成交量(张)，数值为0        |                | |
| count     | true | string | 成交笔数，数值为0        |                | |
| open     | true | string | 开盘值（预测资金费率）        |                | |
| close     | true | string | 收盘值 （预测资金费率）       |                | |
| low     | true | string | 最低值 （预测资金费率）       |                | |
| high     | true | string | 最高值 （预测资金费率）       |                | |
| amount     | true | string | 成交量(币), 数值为0        |                | |
| trade_turnover     | true | string | 成交额, 数值为0        |                | |
| \</data\>            |      |        |               |                | |
| status | true | string | 请求处理结果                          | "ok" , "error" | |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | |

## 【通用】获取基差数据

- GET `/index/market/history/linear_swap_basis`

```shell

curl "https://api.hbdm.com/index/market/history/linear_swap_basis?contract_code=BTC-USDT&period=1min&size=1"

```

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称   | 是否必须 | 类型     | 描述  | 取值范围 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约代码          |       如"BTC-USDT"           |
| period          | true     | string  | 周期               |    1min,5min, 15min, 30min, 60min,4hour,1day,1week,1mon     |
| basis_price_type          | false     | string  | 基差价格类型，表示在周期内计算基差使用的价格类型， 不填，默认使用开盘价     |    开盘价：open，收盘价：close，最高价：high，最低价：low，平均价=（最高价+最低价）/2：average   |
| size  | true     | int    | 基差获取数量，默认 150 | [1,2000] |


> Response:

```json

{
    "ch": "market.BTC-USDT.basis.1min.open",
    "data": [
        {
            "basis": "15.29074235666667",
            "basis_rate": "0.001170582317307796",
            "contract_price": "13077.8",
            "id": 1603697160,
            "index_price": "13062.509257643333"
        }
    ],
    "status": "ok",
    "ts": 1603697170804
}
```

### 返回参数

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| ch     | true | string | 数据所属的 channel，格式： market.basis |                | |
| \<data\> |  | object array |  |  |
| id | true | long | 唯一标识 |  |
| contract_price | true | string | 合约最新成交价 |  |
| index_price | true | string | 指数基准价，与基差价格类型匹配 |  |
| basis | true | string | 基差=合约基准价 - 指数基准价 |  |
| basis_rate | true | string | 基差率=基差/指数基准价 |  |
| \</data\> |  |  |  |  |
| status | true | string | 请求处理结果                          | "ok" , "error" | |
| ts | true  | long | 生成时间 |  |



# 合约资产接口

## 【逐仓】获取用户账户信息

###  示例

- POST  `/linear-swap-api/v1/swap_account_info`

#### 备注
 - 该接口仅支持逐仓模式。

###  请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | false | string | 合约代码 |  "BTC-USDT"... ,如果缺省，默认返回所有合约  |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "margin_balance": 99.755058840000000000,
            "margin_position": 0,
            "margin_frozen": 12.730000000000000000,
            "margin_available": 87.025058840000000000,
            "profit_real": 0,
            "profit_unreal": 0,
            "risk_rate": 7.761218290652003142,
            "withdraw_available": 87.025058840000000000000000000000000000,
            "liquidation_price": null,
            "lever_rate": 10,
            "adjust_factor": 0.075000000000000000,
            "margin_static": 99.755058840000000000,
            "contract_code": "BTC-USDT",
            "margin_asset": "USDT",
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT"
        }
    ],
    "ts": 1603697381238
}
    
```

###  返回参数

| 参数名称  | 是否必须   | 类型      | 描述    | 取值范围           |
| -------------------- | ------ | ------- | -------------------- | -------------- |
| status               | true   | string  | 请求处理结果               | "ok" , "error" |
| ts                   | long | long    | 响应生成时间点，单位：毫秒        |                |
| \<data\> |    true    |  object array       |                      |                |
| symbol     | true   | string  | 品种代码                 | "BTC","ETH"... |
| contract_code     | true   | string  | 合约代码                 |  "BTC-USDT" ... |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_balance       | true   | decimal | 账户权益                 |                |
| margin_static        | true   | decimal | 静态权益                 |                |
| margin_position      | true   | decimal | 持仓保证金（当前持有仓位所占用的保证金） |                |
| margin_frozen        | true   | decimal | 冻结保证金                |                |
| margin_available     | true   | decimal | 可用保证金                |                |
| profit_real          | true   | decimal | 已实现盈亏                |                |
| profit_unreal        | true   | decimal | 未实现盈亏                |                |
| risk_rate            | true   | decimal | 保证金率                 |                |
| liquidation_price    | true   | decimal | 预估强平价                |                |
| withdraw_available   | true   | decimal | 可划转数量                |                |
| lever_rate           | true   | decimal | 杠杠倍数                 |                |
| adjust_factor        | true   | decimal | 调整系数                 |                |
| margin_mode          | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account       | true | string | 保证金账户  | 比如“BTC-USDT” |
| \</data\>            |        |         |                      |                |

## 【全仓】获取用户账户信息

 - POST `/linear-swap-api/v1/swap_cross_account_info`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| margin_account | false | string | 保证金账户，不填则返回所有全仓保证金账户 |  "USDT"，目前只有一个全仓账户（USDT）  |

> Response

```json
{
    "status":"ok",
    "data":[
        {
            "margin_mode":"cross",
            "margin_account":"USDT",
            "margin_asset":"USDT",
            "margin_balance":0.000000549410817836,
            "margin_static":0.000000549410817836,
            "margin_position":0,
            "margin_frozen":0,
            "profit_real":0,
            "profit_unreal":0,
            "withdraw_available":0.000000549410817836,
            "risk_rate":null,
            "contract_detail":[
                {
                    "symbol":"BTC",
                    "contract_code":"BTC-USDT",
                    "margin_position":0,
                    "margin_frozen":0,
                    "margin_available":0.000000549410817836,
                    "profit_unreal":0,
                    "liquidation_price":null,
                    "lever_rate":100,
                    "adjust_factor":0.55
                },
                {
                    "symbol":"EOS",
                    "contract_code":"EOS-USDT",
                    "margin_position":0,
                    "margin_frozen":0,
                    "margin_available":0.000000549410817836,
                    "profit_unreal":0,
                    "liquidation_price":null,
                    "lever_rate":5,
                    "adjust_factor":0.06
                }
            ]
        }
    ],
    "ts":1606906200680
}

```
     
###  返回参数

| 参数名称  | 是否必须   | 类型      | 描述    | 取值范围           |
| -------------------- | ------ | ------- | -------------------- | -------------- |
| status               | true   | string  | 请求处理结果               | "ok" , "error" |
| ts                   | long | long    | 响应生成时间点，单位：毫秒        |                |
| \<data\> |    true    |  object array       |                      |                |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_balance       | true   | decimal | 账户权益                 |                |
| margin_static        | true   | decimal | 静态权益                 |                |
| margin_position      | true   | decimal | 持仓保证金（所有全仓仓位汇总） |                |
| margin_frozen        | true   | decimal | 冻结保证金（所有全仓仓位汇总）                |                |
| profit_real          | true   | decimal | 已实现盈亏                |                |
| profit_unreal        | true   | decimal | 未实现盈亏（所有全仓仓位汇总）                |                |
| withdraw_available   | true   | decimal | 可划转数量                |                |
| risk_rate            | true   | decimal | 保证金率                 |                |
| \<contract_detail\> |    true    |  object array       |    支持全仓的所有合约的相关字段                  |                |
| symbol     | true   | string  | 品种代码                 | "BTC","ETH"... |
| contract_code     | true   | string  | 合约代码                 |  "BTC-USDT" ... |
| margin_position      | true   | decimal | 持仓保证金（当前持有仓位所占用的保证金） |                |
| margin_frozen        | true   | decimal | 冻结保证金                |                |
| margin_available     | true   | decimal | 可用保证金                |                |
| profit_unreal        | true   | decimal | 未实现盈亏                |                |
| liquidation_price | true | decimal | 预估强平价         |                |
| lever_rate           | true   | decimal | 杠杠倍数                 |                |
| adjust_factor        | true   | decimal | 调整系数                 |                |
| \</contract_detail\>            |        |         |                      |                |
| \</data\>            |        |         |                      |                |
 

## 【逐仓】获取用户持仓信息

###  示例

- POST `/linear-swap-api/v1/swap_position_info`

#### 备注
 - 该接口仅支持逐仓模式。

###  请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | false | string | 合约代码 |  "BTC-USDT"... ,如果缺省，默认返回所有合约  |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "volume": 1.000000000000000000,
            "available": 1.000000000000000000,
            "frozen": 0,
            "cost_open": 13068.000000000000000000,
            "cost_hold": 13068.000000000000000000,
            "profit_unreal": 0,
            "profit_rate": 0,
            "lever_rate": 10,
            "position_margin": 1.306800000000000000,
            "direction": "buy",
            "profit": 0,
            "last_price": 13068,
            "margin_asset": "USDT",
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT"
        }
    ],
    "ts": 1603697821846
}

```

###  返回参数

| 参数名称  | 是否必须 | 类型      | 描述   | 取值范围      |
| -------------------- | ---- | ------- | ---------------- | ---------------------------------------- |
| status               | true | string  | 请求处理结果           | "ok" , "error"                           |
| ts                   | true | long    | 响应生成时间点，单位：毫秒    |                                          |
| \<data\>             |  true    |   object array      |     |     |
| symbol               | true | string  | 品种代码             | "BTC","ETH"...                           |
| contract_code        | true | string  | 合约代码             | "BTC-USDT" ...                          |
| volume               | true | decimal | 持仓量（张）              |                                          |
| available            | true | decimal | 可平仓数量（张）            |                                          |
| frozen               | true | decimal | 冻结数量（张）             |                                          |
| cost_open            | true | decimal | 开仓均价             |                                          |
| cost_hold            | true | decimal | 持仓均价             |                                          |
| profit_unreal        | true | decimal | 未实现盈亏            |                                          |
| profit_rate          | true | decimal | 收益率              |                                          |
| profit               | true | decimal | 收益               |                                          |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| position_margin      | true | decimal | 持仓保证金            |                                          |
| lever_rate           | true | int     | 杠杠倍数             |                                          |
| direction            | true | string  | "buy":买 "sell":卖 |                                          |
| last_price           | true | decimal | 最新价              |                                          |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| \</data\>            |      |         |      |              |

#### 备注

- 如果有某个品种在结算中，不带请求参数去查询持仓，会返回错误码1080(1080  In settlement or delivery. Unable to get positions of some contracts.)。建议您带上请求参数去查询持仓，避免报错查询不到持仓。

## 【全仓】获取用户持仓信息

 - POST `/linear-swap-api/v1/swap_cross_position_info`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | false | string | 合约代码 |  "BTC-USDT"... ,如果缺省，默认返回所有合约  |

> Response:

```json
{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "volume": 2,
            "available": 2,
            "frozen": 0,
            "cost_open": 51179.1,
            "cost_hold": 51179.1,
            "profit_unreal": 0,
            "profit_rate": 0,
            "lever_rate": 100,
            "position_margin": 10.23582,
            "direction": "sell",
            "profit": 0,
            "last_price": 51179.1,
            "margin_asset": "USDT",
            "margin_mode": "cross",
            "margin_account": "USDT"
        }
    ],
    "ts": 1606962314205
}
```
     
###  返回参数

| 参数名称  | 是否必须 | 类型      | 描述   | 取值范围      |
| -------------------- | ---- | ------- | ---------------- | ---------------------------------------- |
| status               | true | string  | 请求处理结果           | "ok" , "error"                           |
| ts                   | true | long    | 响应生成时间点，单位：毫秒    |                                          |
| \<data\> |  true    |   object array      |     |     |
| symbol               | true | string  | 品种代码             | "BTC","ETH"...                           |
| contract_code        | true | string  | 合约代码             | "BTC-USDT" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| volume               | true | decimal | 持仓量（张）              |                                          |
| available            | true | decimal | 可平仓数量（张）            |                                          |
| frozen               | true | decimal | 冻结数量（张）             |                                          |
| cost_open            | true | decimal | 开仓均价             |                                          |
| cost_hold            | true | decimal | 持仓均价             |                                          |
| profit_unreal        | true | decimal | 未实现盈亏            |                                          |
| profit_rate          | true | decimal | 收益率              |                                          |
| profit               | true | decimal | 收益               |                                          |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| position_margin      | true | decimal | 持仓保证金            |                                          |
| lever_rate           | true | int     | 杠杠倍数             |                                          |
| direction            | true | string  | "buy":买 "sell":卖 |                                          |
| last_price           | true | decimal | 最新价              |                                          |
| \</data\>            |      |         |      |              |

## 【逐仓】查询用户账户和持仓信息

- post `/linear-swap-api/v1/swap_account_position_info`
  
#### 备注
 - 该接口仅支持逐仓模式。
  
### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | true | string | 合约代码 |  "BTC-USDT"...   |

### 备注：

 - 当品种上市，合约待上市或下市时，仓位信息返回为空

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "margin_balance": 99.751731640000000000,
            "margin_position": 1.306990000000000000,
            "margin_frozen": 12.730000000000000000,
            "margin_available": 85.714741640000000000,
            "profit_real": -0.005227200000000000,
            "profit_unreal": 0.001900000000000000,
            "risk_rate": 7.031347702748238760,
            "withdraw_available": 85.712841640000000000000000000000000000,
            "liquidation_price": null,
            "lever_rate": 10,
            "adjust_factor": 0.075000000000000000,
            "margin_static": 99.749831640000000000,
            "positions": [
                {
                    "symbol": "BTC",
                    "contract_code": "BTC-USDT",
                    "volume": 1.000000000000000000,
                    "available": 1.000000000000000000,
                    "frozen": 0,
                    "cost_open": 13068.000000000000000000,
                    "cost_hold": 13068.000000000000000000,
                    "profit_unreal": 0.001900000000000000,
                    "profit_rate": 0.001453933272115090,
                    "lever_rate": 10,
                    "position_margin": 1.306990000000000000,
                    "direction": "buy",
                    "profit": 0.001900000000000000,
                    "last_price": 13069.9,
                    "margin_asset": "USDT",
                    "margin_mode": "isolated",
                    "margin_account": "BTC-USDT"
                }
            ],
            "margin_asset": "USDT",
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT"
        }
    ],
    "ts": 1603697944138
}
```

### 返回参数

| 参数名称                 | 是否必须   | 类型      | 描述                   | 取值范围           |
| -------------------- | ------ | ------- | -------------------- | -------------- |
| status               | true   | string  | 请求处理结果               | "ok" , "error" |
| ts                   | long | long    | 响应生成时间点，单位：毫秒        |                |
| \<data\> |    true    |  object array       |                      |                |
| symbol     | true   | string  | 品种代码                 | "BTC","ETH"... |
| contract_code        | true | string  | 合约代码             | "BTC-USDT" ...   |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_balance       | true   | decimal | 账户权益                 |                |
| margin_static        | true   | decimal | 静态权益                 |                |
| margin_position      | true   | decimal | 持仓保证金（当前持有仓位所占用的保证金） |                |
| margin_frozen        | true   | decimal | 冻结保证金                |                |
| margin_available     | true   | decimal | 可用保证金                |                |
| profit_real          | true   | decimal | 已实现盈亏                |                |
| profit_unreal        | true   | decimal | 未实现盈亏                |                |
| risk_rate            | true   | decimal | 保证金率                 |                |
| liquidation_price    | true   | decimal | 预估强平价                |                |
| withdraw_available   | true   | decimal | 可划转数量                |                |
| lever_rate           | true   | decimal | 杠杠倍数                 |                |
| adjust_factor        | true   | decimal | 调整系数                 |                |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| \<positions\> |    true    |  object array       |                      |                |
| symbol               | true | string  | 品种代码             | "BTC","ETH"...                           |
| contract_code        | true | string  | 合约代码             |"BTC-USDT" ...         |
| volume               | true | decimal | 持仓量（张）              |                                          |
| available            | true | decimal | 可平仓数量（张）            |                                          |
| frozen               | true | decimal | 冻结数量（张）             |                                          |
| cost_open            | true | decimal | 开仓均价             |                                          |
| cost_hold            | true | decimal | 持仓均价             |                                          |
| profit_unreal        | true | decimal | 未实现盈亏            |                                          |
| profit_rate          | true | decimal | 收益率              |                                          |
| profit               | true | decimal | 收益               |                                          |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| position_margin      | true | decimal | 持仓保证金            |                                          |
| lever_rate           | true | int     | 杠杠倍数             |                                          |
| direction            | true | string  | "buy":买 "sell":卖 |                                          |
| last_price           | true | decimal | 最新价              |                                          |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| \</positions\>            |        |         |                      |                |
| \</data\>            |        |         |                      |                |

## 【全仓】查询用户账户和持仓信息

 - POST `/linear-swap-api/v1/swap_cross_account_position_info`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| margin_account | true | string | 保证金账户 |  "USDT"，目前只有一个全仓账户（USDT）  |

> Response

```json
{
    "status":"ok",
    "data":{
        "positions":[
            {
                "symbol":"BTC",
                "contract_code":"BTC-USDT",
                "volume":2,
                "available":2,
                "frozen":0,
                "cost_open":51179.1,
                "cost_hold":51179.1,
                "profit_unreal":0,
                "profit_rate":0,
                "lever_rate":100,
                "position_margin":10.23582,
                "direction":"sell",
                "profit":0,
                "last_price":51179.1,
                "margin_asset":"USDT",
                "margin_mode":"cross",
                "margin_account":"USDT"
            },
            {
                "symbol":"ETH",
                "contract_code":"ETH-USDT",
                "volume":1,
                "available":1,
                "frozen":0,
                "cost_open":50,
                "cost_hold":50,
                "profit_unreal":0,
                "profit_rate":0,
                "lever_rate":5,
                "position_margin":0.1,
                "direction":"sell",
                "profit":0,
                "last_price":50,
                "margin_asset":"USDT",
                "margin_mode":"cross",
                "margin_account":"USDT"
            }
        ],
        "margin_mode":"cross",
        "margin_account":"USDT",
        "margin_asset":"USDT",
        "margin_balance":999.488009549410817836,
        "margin_static":999.488009549410817836,
        "margin_position":10.33582,
        "margin_frozen":0,
        "profit_real":-0.511991,
        "profit_unreal":0,
        "withdraw_available":989.152189549410817836,
        "risk_rate":176.349367815895629991,
        "contract_detail":[
            {
                "symbol":"BTC",
                "contract_code":"BTC-USDT",
                "margin_position":10.23582,
                "margin_frozen":0,
                "margin_available":989.152189549410817836,
                "profit_unreal":0,
                "liquidation_price":100599.901021850363890402,
                "lever_rate":100,
                "adjust_factor":0.55
            },
            {
                "symbol":"ETH",
                "contract_code":"ETH-USDT",
                "margin_position":0.1,
                "margin_frozen":0,
                "margin_available":989.152189549410817836,
                "profit_unreal":0,
                "liquidation_price":98256.749856661148007509,
                "lever_rate":5,
                "adjust_factor":0.06
            }
        ]
    },
    "ts":1606965138763
}

```

###  返回参数

| 参数名称  | 是否必须   | 类型      | 描述    | 取值范围           |
| -------------------- | ------ | ------- | -------------------- | -------------- |
| status               | true   | string  | 请求处理结果               | "ok" , "error" |
| ts                   | long | long    | 响应生成时间点，单位：毫秒        |                |
| \<data\> |    true    |  object array       |                      |                |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_balance       | true   | decimal | 账户权益                 |                |
| margin_static        | true   | decimal | 静态权益                 |                |
| margin_position      | true   | decimal | 持仓保证金（所有全仓仓位汇总） |                |
| margin_frozen        | true   | decimal | 冻结保证金（所有全仓仓位汇总）                |                |
| profit_real          | true   | decimal | 已实现盈亏                |                |
| profit_unreal        | true   | decimal | 未实现盈亏（所有全仓仓位汇总）                |                |
| withdraw_available   | true   | decimal | 可划转数量                |                |
| risk_rate            | true   | decimal | 保证金率                 |                |
| \<contract_detail\> |    true    |  object array       |    支持全仓的所有合约的相关字段                  |                |
| symbol     | true   | string  | 品种代码                 | "BTC","ETH"... |
| contract_code     | true   | string  | 合约代码                 |  "BTC-USDT" ... |
| margin_position      | true   | decimal | 持仓保证金（当前持有仓位所占用的保证金） |                |
| margin_frozen        | true   | decimal | 冻结保证金                |                |
| margin_available     | true   | decimal | 可用保证金                |                |
| profit_unreal        | true   | decimal | 未实现盈亏                |                |
| liquidation_price | true | decimal | 预估强平价         |                |
| lever_rate           | true   | decimal | 杠杠倍数                 |                |
| adjust_factor        | true   | decimal | 调整系数                 |                |
| \</contract_detail\>            |        |         |                      |                |
| \<positions\> |    true    |  object array       |    支持全仓的所有合约的仓位                  |                |
| symbol               | true | string  | 品种代码             | "BTC","ETH"...                           |
| contract_code        | true | string  | 合约代码             | "BTC-USDT" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| volume               | true | decimal | 持仓量（张）              |                                          |
| available            | true | decimal | 可平仓数量（张）            |                                          |
| frozen               | true | decimal | 冻结数量（张）             |                                          |
| cost_open            | true | decimal | 开仓均价             |                                          |
| cost_hold            | true | decimal | 持仓均价             |                                          |
| profit_unreal        | true | decimal | 未实现盈亏            |                                          |
| profit_rate          | true | decimal | 收益率              |                                          |
| profit               | true | decimal | 收益               |                                          |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| position_margin      | true | decimal | 持仓保证金            |                                          |
| lever_rate           | true | int     | 杠杠倍数             |                                          |
| direction            | true | string  | "buy":买 "sell":卖 |                                          |
| last_price           | true | decimal | 最新价              |                                          |
| \</positions\>            |        |         |                      |                |
| \</data\>            |        |         |                      |                |

## 【逐仓】查询母账户下所有子账户资产信息

- POST `/linear-swap-api/v1/swap_sub_account_list`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | false | string | 合约代码 |  "BTC-USDT"... ,如果缺省，默认返回所有合约  |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "sub_uid": 123456789,
            "list": [
                {
                    "symbol": "BTC",
                    "margin_balance": 20,
                    "liquidation_price": null,
                    "risk_rate": null,
                    "contract_code": "BTC-USDT",
                    "margin_asset": "USDT",
                    "margin_mode": "isolated",
                    "margin_account": "BTC-USDT"
                }
            ]
        }
    ],
    "ts": 1603698380336
}
```

### 返回参数

| 参数名称  | 是否必须 | 类型      | 描述     | 取值范围           |
| ----------------- | ---- | ------- | ------------- | -------------- |
| status            | true | string  | 请求处理结果        | "ok" , "error" |
| ts                | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>          | true     |    object array     |               |                |
| sub_uid           | true | long    | 子账户UID        |                |
| \<list\>          |   true   |  object array       |               |                |
| symbol            | true | string  | 品种代码          | "BTC","ETH"...|
| contract_code            | true | string  | 合约代码          |  "BTC-USDT" ... |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_balance    | true | decimal | 账户权益          |                |
| liquidation_price | true | decimal | 预估强平价         |                |
| risk_rate         | true | decimal | 保证金率          |                |
| margin_mode       | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account    | true | string | 保证金账户  | 比如“BTC-USDT” |
| \</list\>         |      |         |               |                |
| \</data\>         |      |         |               |                |

#### 备注

  - 只返回已经开通合约交易的子账户数据.

## 【全仓】查询母账户下所有子账户资产信息   

 - POST `/linear-swap-api/v1/swap_cross_sub_account_list`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| margin_account | false | string | 保证金账户，不填则返回所有全仓保证金账户 |  "USDT"，目前只有一个全仓账户（USDT）  |

> Response

```json

{
    "status": "ok",
    "data": [
        {
            "sub_uid": 123456789,
            "list": [
                {
                    "margin_balance": 163.561708129559110889,
                    "risk_rate": 78.896729392251481019,
                    "margin_asset": "USDT",
                    "margin_mode": "cross",
                    "margin_account": "USDT"
                }
            ]
        }
    ],
    "ts": 1606962745633
}

```
### 返回参数

| 参数名称  | 是否必须 | 类型      | 描述     | 取值范围           |
| ----------------- | ---- | ------- | ------------- | -------------- |
| status            | true | string  | 请求处理结果        | "ok" , "error" |
| ts                | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>          | true     |    object array     |               |                |
| sub_uid           | true | long    | 子账户UID        |                |
| \<list\>          |   true   |  object array       |               |                |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_balance    | true | decimal | 账户权益          |                |
| risk_rate         | true | decimal | 保证金率          |                |
| \</list\>         |      |         |               |                |
| \</data\>         |      |         |               |                |                  
    
#### 备注

 - 只返回已经开通合约交易的子账户数据.   

## 【逐仓】查询单个子账户资产信息

- POST `/linear-swap-api/v1/swap_sub_account_info`

#### 备注
 - 该接口仅支持逐仓模式。

###  请求参数

| 参数名称    | 是否必须  | 类型     | 描述    | 取值范围 |
| ------- | ----- | ------ | ------- | ---------------------------- |
| contract_code  | false | string | 合约代码    |  "BTC-USDT"... ,如果缺省，默认返回所有合约  |      |
| sub_uid | true  | long   | 子账户的UID |       |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "margin_balance": 20,
            "margin_position": 0,
            "margin_frozen": 0,
            "margin_available": 20.000000000000000000,
            "profit_real": 0,
            "profit_unreal": 0,
            "risk_rate": null,
            "withdraw_available": 20.000000000000000000,
            "liquidation_price": null,
            "lever_rate": 5,
            "adjust_factor": 0.040000000000000000,
            "margin_static": 20,
            "contract_code": "BTC-USDT",
            "margin_asset": "USDT",
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT"
        }
    ],
    "ts": 1603698523200
}
  
```

### 返回参数

| 参数名称               | 是否必须 | 类型      | 描述                   | 取值范围                                   |
| ------------------ | ---- | ------- | -------------------- | -------------------------------------- |
| status             | true | string  | 请求处理结果               | "ok" , "error"                         |
| ts                 | true | long    | 响应生成时间点，单位：毫秒        |                                        |
| \<data\>           |  true    | object array    |     |    |
| symbol             | true | string  | 品种代码                 | "BTC","ETH"... |
| contract_code             | true | string  | 合约代码                 | "BTC-USDT","ETH-USDT"... |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_balance     | true | decimal | 账户权益                 |                                        |
| margin_position    | true | decimal | 持仓保证金（当前持有仓位所占用的保证金） |                                        |
| margin_frozen      | true | decimal | 冻结保证金                |                                        |
| margin_available   | true | decimal | 可用保证金                |                                        |
| profit_real        | true | decimal | 已实现盈亏                |                                        |
| profit_unreal      | true | decimal | 未实现盈亏                |                                        |
| risk_rate          | true | decimal | 保证金率                 |                                        |
| liquidation_price  | true | decimal | 预估强平价                |                                        |
| withdraw_available | true | decimal | 可划转数量                |                                        |
| lever_rate         | true | decimal | 杠杆倍数                 |                                        |
| adjust_factor      | true | decimal | 调整系数                 |                                        |
| margin_static      | true | decimal | 静态权益                   |                                        |
| margin_mode       | true | string     | 保证金模式             | isolated：逐仓模式 |
| margin_account    | true | string     | 保证金账户             | 比如“BTC-USDT” |
| \</data\>          |      |         |       |  |

#### 备注

  - 只能查询到开通合约交易的子账户信息；
  
  
## 【全仓】查询单个子账户资产信息

  - POST `/linear-swap-api/v1/swap_cross_sub_account_info`  
    
#### 备注
 - 该接口仅支持全仓模式。

###  请求参数*

| 参数名称    | 是否必须  | 类型     | 描述    | 取值范围 |
| ------- | ----- | ------ | ------- | ---------------------------- |
| sub_uid | true  | long   | 子账户的UID |       |
| margin_account | false | string | 保证金账户，不填则返回所有全仓保证金账户 |  "USDT"，目前只有一个全仓账户（USDT）  |

 > Response:

 ```json

{
    "status": "ok",
    "data": [
        {
            "margin_mode": "cross",
            "margin_account": "USDT",
            "margin_asset": "USDT",
            "margin_balance": 163.561708129559110889,
            "margin_static": 163.561708129559110889,
            "margin_position": 102.3582,
            "margin_frozen": 0,
            "profit_real": 0,
            "profit_unreal": 0,
            "withdraw_available": 61.203508129559110889,
            "risk_rate": 78.896729392251481019,
            "contract_detail": [
                {
                    "symbol": "BTC",
                    "contract_code": "BTC-USDT",
                    "margin_position": 102.3582,
                    "margin_frozen": 0,
                    "margin_available": 61.203508129559110889,
                    "profit_unreal": 0,
                    "liquidation_price": 67266.205988999911443127,
                    "lever_rate": 5,
                    "adjust_factor": 0.02
                },
                {
                    "symbol": "EOS",
                    "contract_code": "EOS-USDT",
                    "margin_position": 0,
                    "margin_frozen": 0,
                    "margin_available": 61.203508129559110889,
                    "profit_unreal": 0,
                    "liquidation_price": null,
                    "lever_rate": 5,
                    "adjust_factor": 0.06
                }
            ]
        }
    ],
    "ts": 1606963336786
}

 ```  
    
###  返回参数

| 参数名称  | 是否必须   | 类型      | 描述    | 取值范围           |
| -------------------- | ------ | ------- | -------------------- | -------------- |
| status               | true   | string  | 请求处理结果               | "ok" , "error" |
| ts                   | long | long    | 响应生成时间点，单位：毫秒        |                |
| \<data\> |    true    |  object array       |                      |                |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_balance       | true   | decimal | 账户权益                 |                |
| margin_static        | true   | decimal | 静态权益                 |                |
| margin_position      | true   | decimal | 持仓保证金（当前持有仓位所占用的保证金） |                |
| margin_frozen        | true   | decimal | 冻结保证金                |                |
| profit_real          | true   | decimal | 已实现盈亏                |                |
| profit_unreal        | true   | decimal | 未实现盈亏                |                |
| withdraw_available   | true   | decimal | 可划转数量                |                |
| risk_rate            | true   | decimal | 保证金率                 |                |
| \<contract_detail\> |    true    |  object array       |    支持全仓的所有合约的相关字段                  |                |
| symbol     | true   | string  | 品种代码                 | "BTC","ETH"... |
| contract_code     | true   | string  | 合约代码                 |  "BTC-USDT" ... |
| margin_position      | true   | decimal | 持仓保证金（当前持有仓位所占用的保证金） |                |
| margin_frozen        | true   | decimal | 冻结保证金                |                |
| margin_available     | true   | decimal | 可用保证金                |                |
| profit_unreal        | true   | decimal | 未实现盈亏                |                |
| liquidation_price | true | decimal | 预估强平价         |                |
| lever_rate           | true   | decimal | 杠杠倍数                 |                |
| adjust_factor        | true   | decimal | 调整系数                 |                |
| \</contract_detail\>            |        |         |                      |                |
| \</data\>            |        |         |                      |                |

#### 备注

  - 只能查询到开通合约交易的子账户信息；
  
  - 子账户来过合约系统但是未开通合约交易也不返回对应的数据；
 

## 【逐仓】查询单个子账户持仓信息

- POST `/linear-swap-api/v1/swap_sub_position_info`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称    | 是否必须  | 类型     | 描述    | 取值范围 |
| ------- | ----- | ------ |  ------------------ | ---- |
| contract_code  | false | string | 合约代码    |  "BTC-USDT"...，如果缺省，默认返回所有合约 |      |
| sub_uid | true  | long   | 子账户的UID |                              |      |


> Response:

```json
 
{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "volume": 1.000000000000000000,
            "available": 1.000000000000000000,
            "frozen": 0,
            "cost_open": 13038.700000000000000000,
            "cost_hold": 13038.700000000000000000,
            "profit_unreal": 0,
            "profit_rate": 0,
            "lever_rate": 10,
            "position_margin": 1.303870000000000000,
            "direction": "buy",
            "profit": 0,
            "last_price": 13038.7,
            "margin_asset": "USDT",
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT"
        }
    ],
    "ts": 1603699081114
}                                           
```

### 返回参数

| 参数名称            | 是否必须 | 类型      | 描述            | 取值范围                                     |
| --------------- | ---- | ------- | ------------- | ---------------------------------------- |
| status          | true | string  | 请求处理结果        | "ok" , "error"                           |
| ts              | true | long    | 响应生成时间点，单位：毫秒 |                                          |
| \<data\>        |  true    | object array        |               |                                          |
| symbol          | true | string  | 品种代码          | "BTC","ETH"...                           |
| contract_code   | true | string  | 合约代码          | "BTC-USDT" ...                          |
| volume          | true | decimal | 持仓量（张）           |                                          |
| available       | true | decimal | 可平仓数量（张）         |                                          |
| frozen          | true | decimal | 冻结数量（张）         |                                          |
| cost_open       | true | decimal | 开仓均价          |                                          |
| cost_hold       | true | decimal | 持仓均价          |                                          |
| profit_unreal   | true | decimal | 未实现盈亏         |                                          |
| profit_rate     | true | decimal | 收益率           |                                          |
| profit          | true | decimal | 收益            |                                          |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| position_margin | true | decimal | 持仓保证金         |                                          |
| lever_rate      | true | int     | 杠杆倍数          |                                          |
| direction       | true | string  | 仓位方向          | "buy":多 "sell":空                         |
| last_price       | true | decimal  | 最新价          |   |
| margin_mode | true | string | 保证金模式  |isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| \</data\>       |      |         |               |                                          |

## 【全仓】查询单个子账户持仓信息

 - POST `/linear-swap-api/v1/swap_cross_sub_position_info`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称    | 是否必须  | 类型     | 描述    | 取值范围 |
| ------- | ----- | ------ |  ------------------ | ---- |
| contract_code  | false | string | 合约代码    |  "BTC-USDT"...，如果缺省，默认返回所有支持全仓的合约 |      |
| sub_uid | true  | long   | 子账户的UID |                              |      |

> Response:

```json
{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "volume": 1,
            "available": 1,
            "frozen": 0,
            "cost_open": 26666.2,
            "cost_hold": 51179.1,
            "profit_unreal": 0,
            "profit_rate": -4.59624918436072631,
            "lever_rate": 5,
            "position_margin": 102.3582,
            "direction": "sell",
            "profit": -245.129,
            "last_price": 51179.1,
            "margin_asset": "USDT",
            "margin_mode": "cross",
            "margin_account": "USDT"
        }
    ],
    "ts": 1606964256589
}

````

###  返回参数

| 参数名称  | 是否必须 | 类型      | 描述   | 取值范围      |
| -------------------- | ---- | ------- | ---------------- | ---------------------------------------- |
| status               | true | string  | 请求处理结果           | "ok" , "error"                           |
| ts                   | true | long    | 响应生成时间点，单位：毫秒    |                                          |
| \<data\> |  true    |   object array      |     |     |
| symbol               | true | string  | 品种代码             | "BTC","ETH"...                           |
| contract_code        | true | string  | 合约代码             | "BTC-USDT" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| volume               | true | decimal | 持仓量（张）              |                                          |
| available            | true | decimal | 可平仓数量（张）            |                                          |
| frozen               | true | decimal | 冻结数量（张）             |                                          |
| cost_open            | true | decimal | 开仓均价             |                                          |
| cost_hold            | true | decimal | 持仓均价             |                                          |
| profit_unreal        | true | decimal | 未实现盈亏            |                                          |
| profit_rate          | true | decimal | 收益率              |                                          |
| profit               | true | decimal | 收益               |                                          |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| position_margin      | true | decimal | 持仓保证金            |                                          |
| lever_rate           | true | int     | 杠杠倍数             |                                          |
| direction            | true | string  | "buy":买 "sell":卖 |                                          |
| last_price           | true | decimal | 最新价              |                                          |
| \</data\>            |      |         |      |              |

## 【通用】查询用户财务记录

- POST `/linear-swap-api/v1/swap_financial_record`

#### 备注
 - 该接口支持全仓模式和逐仓模式

###  请求参数

| 参数名称        | 是否必须  | 类型     | 描述    | 取值范围  |
| ----------- | ----- | ------ | ---------------------- | ---------------------------------------- |
| margin_account      | true <img width=250/>  | string | 保证金账户  <img width=1000/>    | "BTC-USDT"...     |
| contract_code | false | string | 合约代码，不填查询所有  | 比如“BTC-USDT” |
| type        | false | string | 不填查询全部类型,【查询多类型中间用，隔开】 | 3:平多; 4:平空; 5:开仓手续费-吃单; 6:开仓手续费-挂单; 7:平仓手续费-吃单; 8:平仓手续费-挂单; 9:交割平多; 10:交割平空; 11:交割手续费; 12:强制平多; 13:强制平空; 14:从币币转入; 15:转出至币币; 16:结算未实现盈亏-多仓; 17:结算未实现盈亏-空仓; 19:穿仓分摊; 26:系统; 28:活动奖励; 29:返利; 30:资金费-收入; 31:资金费-支出; 34:转出到子账号合约账户; 35:从子账号合约账户转入; 36:转出到母账号合约账户; 37:从母账号合约账户转入; 38:从其他保证金账户转入; 39:转出到其他保证金账户;  |
| create_date | false | int    | 可随意输入正整数，如果参数超过90则默认查询90天的数据，默认7 |                                          |
| page_index  | false | int    | 第几页,不填默认第一页            |                                          |
| page_size   | false | int    | 不填默认20，不得多于50          |                                          |

#### 备注：
 - 若需要查询全仓账户某一个合约市场的交易类财务记录才需要使用contract_code入参，其他场景无需填写。

> Response:

```json
  
{
    "status": "ok",
    "data": {
        "total_page": 13,
        "current_page": 1,
        "total_size": 13,
        "financial_record": [
            {
                "id": 57408,
                "type": 34,
                "amount": -20.000000000000000000,
                "ts": 1603698366183,
                "contract_code": "BTC-USDT",
                "asset": "USDT",
                "margin_account": "BTC-USDT",
                "face_margin_account": "BTC-USDT"
            }
        ]
    },
    "ts": 1603699203087
}                             
                               
```

### 返回参数

| 参数名称    | 是否必须 | 类型      | 描述            | 取值范围  |
| --------------------- | ---- | ------- | ------------- | ---------------------------------------- |
| status  <img width=250/>    | true <img width=250/> | string  | 请求处理结果  <img width=1000/>  | "ok" , "error"        |
| ts                    | true | long    | 响应生成时间点，单位：毫秒 |                                          |
| \<data\>              | true    |  object       | 字典类型          |                                          |
| \<financial_record\>  | true     |  object array       |               |                                          |
| id                    | true | long    |   财务记录ID（品种唯一）      |                                          |
| ts                    | true | long    | 创建时间          |                                          |
| asset                | true | string  | 币种          | "USDT"...                           |
| contract_code                | true | string  | 合约代码         | "BTC-USDT"...                           |
| margin_account                | true | string  | 保证金账户          | "BTC-USDT"...                           |
| face_margin_account           | true | string  | 对手方保证金账户，仅在type交易类型为34、35、36、37、38、39时有值，其他类型为空字符串          | "BTC-USDT"...                           |
| type                  | true | int     | 交易类型          | 3:平多; 4:平空; 5:开仓手续费-吃单; 6:开仓手续费-挂单; 7:平仓手续费-吃单; 8:平仓手续费-挂单; 9:交割平多; 10:交割平空; 11:交割手续费; 12:强制平多; 13:强制平空; 14:从币币转入; 15:转出至币币; 16:结算未实现盈亏-多仓; 17:结算未实现盈亏-空仓; 19:穿仓分摊; 26:系统; 28:活动奖励; 29:返利; 30:资金费-收入; 31:资金费-支出; 34:转出到子账号合约账户; 35:从子账号合约账户转入; 36:转出到母账号合约账户; 37:从母账号合约账户转入; 38:从其他保证金账户转入; 39:转出到其他保证金账户;   |
| amount                | true | decimal | 金额（计价货币）            |                                          |
| \</financial_record\> |     |         |               |                                          |
| current_page          | true | int     | 当前页           |                                          |
| total_page            | true | int     | 总页数           |                                          |
| total_size            | true | int     | 总条数           |                                          |
| \</data\>             |      |         |      |     |

## 【逐仓】查询用户结算记录

 - POST `linear-swap-api/v1/swap_user_settlement_records`

#### 备注：
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true  | string | 合约code     |                                          |
| start_time   | false  | long    | 起始时间（时间戳，单位毫秒）        |  取值范围：[(当前时间 - 90天), 当前时间] ，默认取当前时间- 90天   |
| end_time   | false  | long    | 结束时间（时间戳，单位毫秒）        | 取值范围：(start_time, 当前时间]，默认取当前时间  |
| page_index	|false |	int	|页码 |不填默认第1页	|
| page_size	|false |	int	|页大小|不填默认20，不得多于50（超过则按照50进行查询）|

#### 备注:
 - 默认按照时间倒序查询，新数据排在前
 - 查询结算开始时间在起始时间之后，结束时间之前的用户结算记录数据。
 - 该接口仅支持用户查询最近90天的数据。

> Response: 

```json
{
    "status":"ok",
    "data":{
        "total_page":1,
        "current_page":1,
        "total_size":13,
        "settlement_records":[
            {
                "symbol":"BTC",
                "contract_code":"BTC-USDT",
                "margin_mode":"isolated",
                "margin_account":"BTC-USDT",
                "margin_balance_init":5000,
                "margin_balance":4891.74704672,
                "settlement_profit_real":-108.25295328,
                "settlement_time":1611040802012,
                "clawback":0,
                "funding_fee":0,
                "offset_profitloss":0,
                "fee":-2.63615328,
                "fee_asset":"USDT",
                "positions":[
                    {
                        "symbol":"BTC",
                        "contract_code":"BTC-USDT",
                        "direction":"buy",
                        "volume":12,
                        "cost_open":27900,
                        "cost_hold_pre":27900,
                        "cost_hold":27459.93,
                        "settlement_profit_unreal":-52.8084,
                        "settlement_price":27459.93,
                        "settlement_type":"settlement"
                    },
                    {
                        "symbol":"BTC",
                        "contract_code":"BTC-USDT",
                        "direction":"sell",
                        "volume":12,
                        "cost_open":27019.86,
                        "cost_hold_pre":27019.86,
                        "cost_hold":27459.93,
                        "settlement_profit_unreal":-52.8084,
                        "settlement_price":27459.93,
                        "settlement_type":"settlement"
                    }
                ]
            }
        ]
    },
    "ts":1611052289681
}
```

### 返回参数

| 参数名称                   | 是否必须 | 类型      | 描述                 | 取值范围                                     |
| ---------------------- | ---- | ------- | ------------------ | ---------------------------------------- |
| status                 | true | string  | 请求处理结果             |                                          |
| \<data\> | true     |  object      |                    |                                          |
| \<settlement_records\> | true     |  object   array    |                    |                                          |
| symbol     | true   | string  | 品种代码                 | "BTC","ETH"... |
| contract_code     | true   | string  | 合约代码                 |  "BTC-USDT" ... |
| margin_mode | true | string | 保证金模式  | cross：全仓模式；isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| margin_balance_init        | true | decimal | 本期初始账户权益         |                                          |
| margin_balance        | true | decimal | 本期结算后账户权益         |                                          |
| settlement_profit_real        | true | decimal | 本期结算已实现盈亏            |                                          |
| settlement_time     | true   | long  | 本期结算时间，交割时为交割时间                |   |
| clawback        | true | decimal |   本期分摊费用         |         |
| funding_fee        | true | decimal |  本期资金费（或本期交割费）            |                       |
| offset_profitloss        | true | decimal | 本期平仓盈亏           |                                          |
| fee        | true | decimal | 本期交易手续费           |                                          |
| fee_asset        | true | string | 手续费币种      |                                          |
| \<positions\> | true     |  object   array    |                    |                                          |
| symbol     | true   | string  | 品种代码                 | "BTC","ETH"... |
| contract_code     | true   | string  | 合约代码                 |  "BTC-USDT" ... |
| direction            | true | string  | 仓位方向  |     "buy":买 "sell":卖                                     |
| volume               | true | decimal | 本期结算前持仓量（张）              |                                          |
| cost_open            | true | decimal | 开仓均价             |                                          |
| cost_hold_pre            | true | decimal | 本期结算前持仓均价             |                                          |
| cost_hold            | true | decimal | 本期结算后持仓均价             |                                          |
| settlement_profit_unreal        | true | decimal | 本期结算未实现盈亏            |                                          |
| settlement_price        | true | decimal | 本期结算价格，交割时为交割价格            |                                          |
| settlement_type        | true | string |   结算类型          |     settlement：结算；delivery：交割；      |
| \</positions\>            |      |         |                    |                                          |
| \</settlement_records\>            |      |         |                    |                                          |
| total_page        | true | int | 总页数   |                |
| current_page        | true | int | 当前页   |                |
| total_size        | true | int | 总条数   |                |
| \</data\>            |      |         |                    |                                          |
| ts                     | true | long    | 时间戳                |                                          |


## 【全仓】查询用户结算记录

 - POST `linear-swap-api/v1/swap_cross_user_settlement_records`

#### 备注：
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| margin_account | true | string | 保证金账户 |  "USDT"，目前只有一个全仓账户（USDT）  |
| start_time   | false  | long    | 起始时间（时间戳，单位毫秒）        |  取值范围：[(当前时间 - 90天), 当前时间] ，默认取当前时间- 90天   |
| end_time   | false  | long    | 结束时间（时间戳，单位毫秒）        | 取值范围：(start_time, 当前时间]，默认取当前时间  |
| page_index	|false |	int	|页码 |不填默认第1页	|
| page_size	|false |	int	|页大小|不填默认10，不得多于25（超过则按照25进行查询）|

> Response: 

```json
{
    "status":"ok",
    "data":{
        "total_page":2,
        "current_page":1,
        "total_size":13,
        "settlement_records":[
            {
                "margin_mode":"cross",
                "margin_account":"USDT",
                "margin_balance_init":5000,
                "margin_balance":5007.6708,
                "settlement_profit_real":7.6708,
                "settlement_time":1611051602040,
                "clawback":0,
                "funding_fee":0,
                "offset_profitloss":0,
                "fee":0.6708,
                "fee_asset":"USDT",
                "contract_detail":[
                    {
                        "symbol":"BTC",
                        "contract_code":"BTC-USDT",
                        "offset_profitloss":0,
                        "fee":0.6708,
                        "fee_asset":"USDT",
                        "positions":[
                            {
                                "symbol":"BTC-USDT",
                                "contract_code":"BTC-USDT",
                                "direction":"buy",
                                "volume":9,
                                "cost_open":27911.111111111111111111,
                                "cost_hold_pre":27911.111111111111111111,
                                "cost_hold":34361.25,
                                "settlement_profit_unreal":580.5125,
                                "settlement_price":34361.25,
                                "settlement_type":"settlement"
                            },
                            {
                                "symbol":"BTC-USDT",
                                "contract_code":"BTC-USDT",
                                "direction":"sell",
                                "volume":9,
                                "cost_open":27988.888888888888888888,
                                "cost_hold_pre":27988.888888888888888888,
                                "cost_hold":34361.25,
                                "settlement_profit_unreal":-573.5125,
                                "settlement_price":34361.25,
                                "settlement_type":"settlement"
                            }
                        ]
                    }
                ]
            },
            {
                "margin_mode":"cross",
                "margin_account":"USDT",
                "margin_balance_init":5000,
                "margin_balance":5000,
                "settlement_profit_real":0,
                "settlement_time":1611047654316,
                "clawback":0,
                "funding_fee":0,
                "offset_profitloss":0,
                "fee":0,
                "fee_asset":"USDT",
                "contract_detail":[

                ]
            }
        ]
    },
    "ts":1611051729365
}
```

### 返回参数

| 参数名称                   | 是否必须 | 类型      | 描述                 | 取值范围                                     |
| ---------------------- | ---- | ------- | ------------------ | ---------------------------------------- |
| status                 | true | string  | 请求处理结果             |                                          |
| \<data\> | true     |  object      |                    |                                          |
| \<settlement_records\> | true     |  object   array    |                    |                                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式；isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| margin_balance_init        | true | decimal | 本期初始账户权益         |                                          |
| margin_balance        | true | decimal | 本期结算后账户权益         |                                          |
| settlement_profit_real        | true | decimal | 本期结算已实现盈亏            |                                          |
| settlement_time     | true   | long  | 本期结算时间，交割时为交割时间                |   |
| clawback        | true | decimal |   本期分摊费用         |         |
| funding_fee        | true | decimal |  本期总资金费（包含交割费）            |                       |
| offset_profitloss        | true | decimal | 本期总平仓盈亏           |                                          |
| fee        | true | decimal | 本期总交易手续费           |                                          |
| fee_asset        | true | string | 手续费币种      |                                          |
| \<contract_detail\> | true     |  object   array    |   支持全仓的所有合约的相关字段                |                                          |
| symbol     | true   | string  | 品种代码                 | "BTC","ETH"... |
| contract_code     | true   | string  | 合约代码                 |  "BTC-USDT" ... |
| offset_profitloss        | true | decimal | 本期该合约平仓盈亏           |                                          |
| fee        | true | decimal | 本期该合约交易手续费           |                                          |
| fee_asset        | true | string | 手续费币种      |                                          |
| \<positions\> | true     |  object   array    |   该合约仓位（结算时有持仓量的才有值）                |                                          |
| symbol     | true   | string  | 品种代码                 | "BTC","ETH"... |
| contract_code     | true   | string  | 合约代码                 |  "BTC-USDT" ... |
| direction            | true | string  | 仓位方向  |     "buy":买 "sell":卖                                     |
| volume               | true | decimal | 本期结算前持仓量（张）              |                                          |
| cost_open            | true | decimal | 开仓均价             |                                          |
| cost_hold_pre            | true | decimal | 本期结算前持仓均价             |                                          |
| cost_hold            | true | decimal | 本期结算后持仓均价             |                                          |
| settlement_profit_unreal        | true | decimal | 本期结算未实现盈亏            |                                          |
| settlement_price        | true | decimal | 本期结算价格，交割时为交割价格            |                                          |
| settlement_type        | true | string |   结算类型          |     settlement：结算；delivery：交割；      |
| \</positions\>            |      |         |                    |                                          |
| \</contract_detail\> | true     |    |                |                                          |
| \</settlement_records\>            |      |         |                    |                                          |
| total_page        | true | int | 总页数   |                |
| current_page        | true | int | 当前页   |                |
| total_size        | true | int | 总条数   |                |
| </data>            |      |         |                    |                                          |
| ts                     | true | long    | 时间戳                |                                          |


## 【逐仓】查询用户可用杠杆倍数

- POST `/linear-swap-api/v1/swap_available_level_rate`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数：

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |	
| contract_code | false | string | 合约代码，不填默认返回所有合约的实际可用杠杆倍数	 | 比如： “BTC-USDT”。。。 |

> 返回示例：

```json

{
    "status": "ok",
    "data": [
        {
            "contract_code": "BTC-USDT",
            "margin_mode": "isolated",
            "available_level_rate": "1,2,3,5,10,20,30,50,75,100,125"
        }
    ],
    "ts": 1603699467348
}

```

### 返回参数：

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| status | true | string | 请求处理结果	 | "ok" , "error" |
| \<data\> | true  | object array |  | 字典数据 |
| contract_code | true  | string |  合约代码 |  比如："BTC-USDT"|
| margin_mode | true | string |  保证金模式  | isolated：逐仓模式 |
| available_level_rate | true  | string |  实际可用杠杆倍数，多个以英文逗号隔开 | 比如："1,5,10" |
| \</data\> |  |  |  |  |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |

## 【全仓】查询用户可用杠杆倍数

 - POST `/linear-swap-api/v1/swap_cross_available_level_rate`

#### 备注
 - 该接口仅支持全仓模式。

###  请求参数

| 参数名              | 参数类型    | 必填    | 描述    | 取值范围 |
| ---------------- | ------- | ----- | ---------------------------------------- | -----------|
| contract_code | false | string | 合约代码，不填默认返回所有支持全仓的合约的实际可用杠杆倍数	 | 比如： “BTC-USDT”。。。 |

> Response

```json

{
    "status": "ok",
    "data": [
        {
            "contract_code": "BTC-USDT",
            "available_level_rate": "1,2,3,5,10,20,30,50,75,100,125",
            "margin_mode": "cross"
        }
    ],
    "ts": 1606965620243
}

```

### 返回参数

| 参数名称          | 是否必须 | 类型      | 描述  | 取值范围 |
| ------------- | ---- | ------- | --------------- | ---------------------------------------- |
| status | true | string | 请求处理结果	 | "ok" , "error" |
| \<data\> | true  | object array |  | 字典数据 |
| contract_code | true  | string |  合约代码 |  比如："BTC-USDT"|
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| available_level_rate | true  | string |  实际可用杠杆倍数，多个以英文逗号隔开 | 比如："1,5,10" |
| \</data\> |  |  |  |  |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |

## 【通用】查询用户当前的下单量限制

- POST `/linear-swap-api/v1/swap_order_limit`

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

  参数名称               |   是否必须   |  类型  |  描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 contract_code <img width=250/> |  false <img width=250/> | string <img width=250/> |  合约代码 <img width=1000/> | "BTC-USDT"... ,如果缺省，默认返回所有合约  |
 order_price_type | true  | string | 订单报价类型 | "limit":限价，"opponent":对手价，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单,opponent_ioc"： 对手价-IOC下单，"lightning_ioc"：闪电平仓-IOC下单，"optimal_5_ioc"：最优5档-IOC下单，"optimal_10_ioc"：最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单,"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |

> Response:

```json

{
    "status": "ok",
    "data": {
        "order_price_type": "limit",
        "list": [
            {
                "symbol": "BTC",
                "contract_code": "BTC-USDT",
                "open_limit": 70000.000000000000000000,
                "close_limit": 140000.000000000000000000
            }
        ]
    },
    "ts": 1603699658996
}

```

### 返回参数

 参数名称                |  是否必须 |  类型  |  描述            |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 status <img width=250/> | true <img width=250/> | string <img width=250/> | 请求处理结果 <img width=1000/>	 | "ok" , "error" |
 ts | true  | long | 响应生成时间点，单位：毫秒 |  |
 \<dict\>(属性名称：data) |  |  |  |  |    
 order_price_type | true  | string | 订单报价类型 | "limit":限价，"opponent":对手价，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单,opponent_ioc"： 对手价-IOC下单，"lightning_ioc"：闪电平仓-IOC下单，"optimal_5_ioc"：最优5档-IOC下单，"optimal_10_ioc"：最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单,"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
 \<list\>(属性名称：list) |  |  |  |  |
 symbol | true  | string | 品种代码 | "BTC","ETH"... |
 contract_code  |  true   |  string   |  合约代码   |  "BTC-USDT" ...  |
 open_limit | true | decimal | 合约开仓单笔下单量最大值 |  |
 close_limit | true | decimal | 合约平仓单笔下单量最大值 |  |
 \</list\>  |  |  |  |  |
 \</dict\> |  |  |  |  |

## 【通用】查询用户当前的手续费费率

- POST `/linear-swap-api/v1/swap_fee`

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围                         |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | false | string | 合约代码 | "BTC-USDT"... ,如果缺省，默认返回所有合约 |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "open_maker_fee": "0.0002",
            "open_taker_fee": "0.0004",
            "close_maker_fee": "0.0002",
            "close_taker_fee": "0.0004",
            "fee_asset": "USDT"
        }
    ],
    "ts": 1603699756575
}

```

### 返回参数

| 参数名称   | 是否必须 | 类型     | 描述     | 取值范围           |
| --------------- | ---- | ------ | --------------- | -------------- |
| status          | true | string | 请求处理结果          | "ok" , "error" |
| ts              | true | long   | 响应生成时间点，单位：毫秒   |                |
| \<data\>        | true     |  object array      |                 |                |
| symbol          | true | string | 品种代码            | "BTC","ETH"... |
| contract_code          | true | string | 合约代码            | "BTC-USDT" ...  |
| open_maker_fee  | true | string | 开仓挂单的手续费费率，小数形式 |                |
| open_taker_fee  | true | string | 开仓吃单的手续费费率，小数形式 |                |
| close_maker_fee | true | string | 平仓挂单的手续费费率，小数形式 |                |
| close_taker_fee | true | string | 平仓吃单的手续费费率，小数形式 |                |
| fee_asset    | true | string | 手续费币种   |    "USDT"...    |
| \</data\>       |      |        |                 |                |

## 【逐仓】查询用户当前的划转限制

- POST `/linear-swap-api/v1/swap_transfer_limit`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围       |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | false | string | 合约代码 |  "BTC-USDT"... ,如果缺省，默认返回所有合约 |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT",
            "transfer_in_max_each": 100000000.000000000000000000,
            "transfer_in_min_each": 1.000000000000000000,
            "transfer_out_max_each": 10000000.000000000000000000,
            "transfer_out_min_each": 0.000001000000000000,
            "transfer_in_max_daily": 1000000000.000000000000000000,
            "transfer_out_max_daily": 200000000.000000000000000000,
            "net_transfer_in_max_daily": 500000000.000000000000000000,
            "net_transfer_out_max_daily": 100000000.000000000000000000
        }
    ],
    "ts": 1603699803580
}

```

### 返回参数

| 参数名称   | 是否必须 | 类型      | 描述       | 取值范围           |
| -------------------------- | ---- | ------- | ------------- | -------------- |
| status                     | true | string  | 请求处理结果        | "ok" , "error" |
| ts                         | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>     |  true    |  object array       |               |                |
| symbol                     | true | string  | 品种代码          | "BTC","ETH"... |
| contract_code                     | true | string  | 合约代码          | "BTC-USDT" ... |
| margin_mode               | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account            | true | string | 保证金账户  | 比如“BTC-USDT” |
| transfer_in_max_each       | true | decimal | 单笔最大转入量       |                |
| transfer_in_min_each       | true | decimal | 单笔最小转入量       |                |
| transfer_out_max_each      | true | decimal | 单笔最大转出量       |                |
| transfer_out_min_each      | true | decimal | 单笔最小转出量       |                |
| transfer_in_max_daily      | true | decimal | 单日累计最大转入量     |                |
| transfer_out_max_daily     | true | decimal | 单日累计最大转出量     |                |
| net_transfer_in_max_daily  | true | decimal | 单日累计最大净转入量    |                |
| net_transfer_out_max_daily | true | decimal | 单日累计最大净转出量    |                |
| \</data\>                  |      |         |               |                |

## 【全仓】查询用户当前的划转限制

 - POST `/linear-swap-api/v1/swap_cross_transfer_limit`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围       |
| ------ | ----- | ------ | ---- | ---------------------------- |
| margin_account | false | string | 保证金账户，不填则返回所有全仓保证金账户  |  "USDT"，目前只有一个全仓账户（USDT）  |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "transfer_in_max_each": 999999999999999999,
            "transfer_in_min_each": 0.0001,
            "transfer_out_max_each": 999999999999999999,
            "transfer_out_min_each": 0.0001,
            "transfer_in_max_daily": 900000000999999999,
            "transfer_out_max_daily": 900000099999999999,
            "net_transfer_in_max_daily": 900000000099999999,
            "net_transfer_out_max_daily": 123456789012345678.12345678,
            "margin_account": "USDT",
            "margin_mode": "cross"
        }
    ],
    "ts": 1606964432217
}

```

### 返回参数

| 参数名称   | 是否必须 | 类型      | 描述       | 取值范围           |
| -------------------------- | ---- | ------- | ------------- | -------------- |
| status                     | true | string  | 请求处理结果        | "ok" , "error" |
| ts                         | true | long    | 响应生成时间点，单位：毫秒 |                |
| \<data\>     |  true    |  object array       |               |                |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| transfer_in_max_each       | true | decimal | 单笔最大转入量       |                |
| transfer_in_min_each       | true | decimal | 单笔最小转入量       |                |
| transfer_out_max_each      | true | decimal | 单笔最大转出量       |                |
| transfer_out_min_each      | true | decimal | 单笔最小转出量       |                |
| transfer_in_max_daily      | true | decimal | 单日累计最大转入量     |                |
| transfer_out_max_daily     | true | decimal | 单日累计最大转出量     |                |
| net_transfer_in_max_daily  | true | decimal | 单日累计最大净转入量    |                |
| net_transfer_out_max_daily | true | decimal | 单日累计最大净转出量    |                |
| \</data\>                  |      |         |               |                |

## 【逐仓】用户持仓量限制的查询

- post `/linear-swap-api/v1/swap_position_limit`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围      |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | false | string | 合约代码 |   "BTC-USDT"... ,如果缺省，默认返回所有合约 |

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "margin_mode": "isolated",
            "buy_limit": 700000.000000000000000000,
            "sell_limit": 700000.000000000000000000
        }
    ],
    "ts": 1603699957489
}

```

### 返回参数

| 参数名称          | 是否必须 | 类型      | 描述   | 取值范围   |
| ------------- | ---- | ------- | --------------- | ---------------------------------------- |
| status        | true | string  | 请求处理结果          | "ok" , "error"                           |
| ts            | true | long    | 响应生成时间点，单位：毫秒   |                                          |
| \<data\>      | true     |  object array       |      |   |
| symbol        | true | string  | 品种代码            | "BTC","ETH"...                           |
| contract_code | true | string  | 合约代码            |   "BTC-USDT" ... |
| margin_mode   | true | string |  保证金模式  | isolated：逐仓模式 |
| buy_limit     | true | decimal | 合约多仓持仓的最大值，单位为张 |                                          |
| sell_limit    | true | decimal | 合约空仓持仓的最大值，单位为张 |                                          |
| \</data\>     |      |         |                 |   |

## 【全仓】用户持仓量限制的查询

 - POST `/linear-swap-api/v1/swap_cross_position_limit`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围      |
| ------ | ----- | ------ | ---- | ---------------------------- |
| contract_code | false | string | 合约代码 |   "BTC-USDT"... ,如果缺省，默认返回所有支持全仓的合约 |

> Response

```json

{
    "status":"ok",
    "data":[
        {
            "symbol":"BSV",
            "contract_code":"BSV-USDT",
            "margin_mode":"cross",
            "buy_limit":50000,
            "sell_limit":50000
        },
        {
            "symbol":"BTC",
            "contract_code":"BTC-USDT",
            "margin_mode":"cross",
            "buy_limit":999999993424398,
            "sell_limit":999943243299997
        }
    ],
    "ts":1606964793311
}

````

### 返回参数

| 参数名称          | 是否必须 | 类型      | 描述   | 取值范围   |
| ------------- | ---- | ------- | --------------- | ---------------------------------------- |
| status        | true | string  | 请求处理结果          | "ok" , "error"                           |
| ts            | true | long    | 响应生成时间点，单位：毫秒   |                                          |
| \<data\>      | true     |  object array       |      |   |
| symbol        | true | string  | 品种代码            | "BTC","ETH"...                           |
| contract_code | true | string  | 合约代码            |   "BTC-USDT" ... |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| buy_limit     | true | decimal | 合约多仓持仓的最大值，单位为张 |                                          |
| sell_limit    | true | decimal | 合约空仓持仓的最大值，单位为张 |                                          |
| \</data\>     |      |         |                 |   |

## 【通用】母子账户划转

- post `/linear-swap-api/v1/swap_master_sub_transfer`

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围    |
| ------ | ----- | ------ | ---- | ---------------------------- |
| sub_uid | true | long | 子账号uid   |  |
| asset | true | string | 币种	 |  "USDT"... |
| from_margin_account | true | string | 转出的保证金账户	 |  "BTC-USDT"，"USDT"... |
| to_margin_account | true | string | 转入的保证金账户	 |  "BTC-USDT"，"USDT"... |
| amount | true | decimal | 划转金额 ||
| type | true | string | 划转类型 | master_to_sub：母账户划转到子账户， sub_to_master：子账户划转到母账户 |

#### 备注：
 - 当from_margin_account或to_margin_account 为USDT时，代表是从全仓保证金中转入或划出。
 - 从转出的保证金账户划转到转入的保证金账户，币种必须为转出的保证金账户的计价币种；
 - 转出的保证金账户与转入的保证金账户的计价币种必须一致（如BTC-USDT可以划转USDT到ETH-USDT，而没办法划转到ETH-HUSD）.
 - 母账户与每个子账户相互划转限频10次/分钟。
  
> Response:

```json

{
    "status": "ok",
    "data": {
        "order_id": "770320047276195840"
    },
    "ts": 1603700211160
}
```

### 返回参数

| 参数名称          | 是否必须 | 类型      | 描述              | 取值范围                                     |
| ------------- | ---- | ------- | --------------- | ---------------------------------------- |
| status        | true | string  | 请求处理结果          | "ok" , "error"                           |
| ts            | true | long    | 响应生成时间点，单位：毫秒   |                                          |
| \<data\>      | true     |  object        |      |   |
| order_id        | true | string  | 划转订单ID            |  |
| \</data\>     |      |         |         |   |

## 【通用】获取母账户下的所有母子账户划转记录

- post `/linear-swap-api/v1/swap_master_sub_transfer_record`

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| 参数名称   | 是否必须  | 类型     | 描述   | 取值范围      |
| ------ | ----- | ------ | ---- | ---------------------------- |
| margin_account | true | string | 保证金账户	 |  "BTC-USDT"，"USDT"... |
| transfer_type | false | string | 划转类型，不填查询全部类型,【查询多类型中间用，隔开】 | 34:转出到子账号合约账户;  35:从子账号合约账户转入; |
| create_date | true | int | 日期 | 可随意输入正整数，如果参数超过90则默认查询90天的数据 |
| page_index | false | int | 页码，不填默认第1页 | 1 |
| page_size | false | int | 不填默认20，不得多于50 | 20 |

> Response:

```json

{
    "status": "ok",
    "data": {
        "total_page": 2,
        "current_page": 1,
        "total_size": 2,
        "transfer_record": [
            {
                "id": 57920,
                "transfer_type": 34,
                "amount": -10.000000000000000000,
                "ts": 1603700211125,
                "sub_uid": "123436789",
                "sub_account_name": "tom",
                "margin_account": "BTC-USDT",
                "asset": "USDT",
                "to_margin_account": "BTC-USDT",
                "from_margin_account": "BTC-USDT"
            }
        ]
    },
    "ts": 1603700414957
} 
```

### 返回参数

| 参数名称          | 是否必须 | 类型      | 描述  | 取值范围 |
| ------------- | ---- | ------- | --------------- | ---------------------------------------- |
| status        | true | string  | 请求处理结果          | "ok" , "error"                           |
| ts            | true | long    | 响应生成时间点，单位：毫秒   |                                          |
| \<data\>      | true     |  object        |      |   |
| \<transfer_record\>      | true     |  object array      |      |   |
| id        | true | long  | 划转订单ID            |  |
| ts        | true | long  | 创建时间            |  |
| asset | true | string | 币种	 |  "USDT"... |
| margin_account | true | string | 保证金账户	 |  "BTC-USDT"... |
| from_margin_account | true | string | 转出的保证金账户	 |  "BTC-USDT"... |
| to_margin_account | true | string | 转入的保证金账户	 |  "BTC-USDT"... |
| sub_uid        | true | string  | 子账户UID            |  |
| sub_account_name        | true | string  | 子账户登录名            |  |
| transfer_type        | true | int  | 划转类型            | 34:转出到子账号合约账户; 35:从子账号合约账户转入; |
| amount        | true | decimal  | 金额            |  |
| \</transfer_record\>     |      |         |         |   |
| total_page        | true | int  | 总页数            |  |
| current_page        | true | int  | 当前页            |  |
| total_size        | true | int  | 总条数            |  |
| \</data\>     |      |         |         |   |

## 【通用】同账号不同保证金账户的划转

- post `/linear-swap-api/v1/swap_transfer_inner`

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| asset | true | string | 币种	 |  "USDT"... |
| from_margin_account | true | string | 转出的保证金账户	 |  "BTC-USDT"，"USDT"... |
| to_margin_account | true | string | 转入的保证金账户	 |  "ETH-USDT"，"USDT"... |
| amount | true | decimal | 划转数额（单位为合约的计价币种）	 |  |

#### **备注：**
- 当from_margin_account或to_margin_account 为USDT时，代表是从全仓保证金中转入或划出。
- 从转出的保证金账户划转到转入的保证金账户，划转的币种必须为转出的保证金账户的计价币种；
- 转出的保证金账户与转入的保证金账户的计价币种必须一致（如BTC-USDT可以划转USDT到ETH-USDT，而没办法划转到ETH-HUSD）。
- 此接口的访问频次的限制为1分钟10次。

> 返回示例：

```json

{
    "status": "ok",
    "data": {
        "order_id": "770321554893758464"
    },
    "ts": 1603700570600
}
```

### 返回参数

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| status | true | string | 请求处理结果	 | "ok" , "error" |
| \<data\> |  |  |  | 字典数据 |
| order_id | true  | string | 划转订单ID |  |
| \</data\> |  |  |  |  |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |

## 【通用】获取用户的API指标禁用信息

- get `/linear-swap-api/v1/swap_api_trading_status`

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 请求参数
 
 无

 > 例子：
 
 ```json

{
  "status": "ok",
  "data":
  [{
      "is_disable": 1,   //是否被禁用
      "order_price_types": "limit,post_only,FOK,IOC",  // 触发禁用的订单价格类型
      "disable_reason":"COR",  // 触发禁用的原因
      "disable_interval": 5,  // 禁用时间间隔
      "recovery_time": 1, // 计划恢复时间
      "COR":  //撤单率的指标（Cancel Order Ratio）
       {
           "orders_threshold": 150,  //委托单笔数的阈值
           "orders": 150,  //用户委托单笔数的实际值
           "invalid_cancel_orders": 150,  //委托单中的无效撤单笔数 
           "cancel_ratio_threshold": 0.98,   //撤单率的阈值
           "cancel_ratio": 0.98,   //用户撤单率的实际值
           "is_trigger": 1,  //用户是否触发该指标
           "is_active": 1   //该指标是否开启
      } ,
      "TDN":  //总禁用次数的指标（Total  Disable Number）
       {
           "disables_threshold": 3,  //总禁用次数的阈值
           "disables": 3,  //总禁用次数的实际值
           "is_trigger": 1,  //用户是否触发该指标
           "is_active": 1   //该指标是否开启
      } 
   }],
 "ts": 158797866555
}

 ``` 

### Response:

| 参数名称          | 是否必须 | 类型      | 描述  | 取值范围 |
| ------------- | ---- | ------- | --------------- | ---------------------------------------- |
| status        | true | string  | 请求处理结果          | "ok" , "error"                           |
| ts            | true | long    | 响应生成时间点，单位：毫秒   |                                          |
| \<data\>      | true     |  object        |      |   |
| is_disable        | true | int  | 是否被禁用            | 1：被禁用中，0：没有被禁用 |
| order_price_types        | true | string  | 触发禁用的订单价格类型，多个订单价格类型以英文逗号分割，例如：“limit,post_only,FOK,IOC”            |  |
| disable_reason        | true | string  | 触发禁用的原因，表示当前的禁用是由哪个指标触发            | "COR":撤单率（Cancel Order Ratio），“TDN”：总禁用次数（Total Disable Number） |
| disable_interval        | true | long  | 禁用时间间隔，单位：毫秒            |  |
| recovery_time        | true | long  | 计划恢复时间，单位：毫秒    ||
| \<COR\>      | true     |  object       |  表示撤单率的指标（Cancel Order Ratio）    |   |
| orders_threshold        | true | long  |  委托单笔数的阈值            |  |
| orders        | true | long  | 用户委托单笔数的实际值            |  |
| invalid_cancel_orders        | true | long  | 用户委托单中的无效撤单笔数  ||
| cancel_ratio_threshold        | true | decimal  | 撤单率的阈值            |  |
| cancel_ratio        | true | decimal  | 用户撤单率的实际值            |  |
| is_trigger        | true | int  | 用户是否触发该指标            |   1：已经触发，0：没有触发 |
| is_active        | true | int  | 该指标是否开启            |  |
| \</COR\>     |      |         |         |   |
| \<TDN\>      | true     |  object       |  表示总禁用次数的指标（Total Disable Number）    |   |
| disables_threshold        | true | long  |  总禁用次数的阈值            |  |
| disables        | true | long  | 总禁用次数的实际值            |  |
| is_trigger        | true | int  | 用户是否触发该指标            |   1：已经触发，0：没有触发 |
| is_active        | true | int  | 该指标是否开启            |  |
| \</TDN\>     |      |         |         |   |
| \</data\>     |      |         |         |   |

# 合约交易接口

## 【逐仓】合约下单 

###  示例

- POST  `/linear-swap-api/v1/swap_order`

#### 备注
 - 该接口仅支持逐仓模式。

> Request

```json
{
    "contract_code": "btc-usdt",
    "direction": "buy",
    "offset":"open",
    "price":"29999",
    "lever_rate": 5,
    "volume": 1,
    "order_price_type":"opponent",
    "tp_trigger_price": 31000,
    "tp_order_price": 31000,
    "tp_order_price_type": "optimal_5",
    "sl_trigger_price": "29100",
    "sl_order_price": "29100",
    "sl_order_price_type": "optimal_5"
}
```

###  请求参数

| 参数名              | 参数类型    | 必填    | 描述    | 取值范围 |
| ---------------- | ------- | ----- | ---------------------------------------- | -----------|
| contract_code     | string <img width=250/>  | true  <img width=250/> | 合约代码 <img width=1000/> | "BTC-USDT"...                           |
| client_order_id  | long    | false | 客户自己填写和维护，必须为数字,请注意必须小于等于9223372036854775807   | |
| price            | decimal | false | 价格                                       | |
| volume           | long    | true  | 委托数量(张)                                  | |
| direction        | string  | true  | 仓位方向 | "buy":买 "sell":卖 |
| offset           | string  | true  | 开平方向    | "open":开 "close":平 |
| lever_rate       | int     | true  | 杠杆倍数[“开仓”若有10倍多单，就不能再下20倍多单;首次使用高倍杠杆(>20倍)，请使用主账号登录web端同意高倍杠杆协议后，才能使用接口下高倍杠杆(>20倍)]             |   |
| order_price_type | string  | true  | 订单报价类型 | "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档，ioc:IOC订单，fok：FOK订单, "opponent_ioc": 对手价-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| tp_trigger_price   | decimal | false  | 止盈触发价格                  |                            |
| tp_order_price   |  decimal | false | 	止盈委托价格（最优N档委托类型时无需填写价格）                  |  |
| tp_order_price_type   | string |  false | 止盈委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |
| sl_trigger_price          | decimal | false | 止损触发价格                  |                            |
| sl_order_price   | decimal |  false | 	止损委托价格（最优N档委托类型时无需填写价格）                  |  |
| sl_order_price_type   |  string | false | 止损委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |

####  备注

 - "limit":限价，"post_only":只做maker单，ioc:IOC订单，fok：FOK订单，这四种报价类型需要传价格，其他都不需要。
 
 - 若存在持仓，那么下单时杠杆倍数必须与持仓杠杆相同，否则下单失败。若需使用新杠杆下单，则必须先使用切换杠杆接口将持仓杠杆切换成功后再下单。

 - 只有开仓订单才支持设置止盈止损。

 - 止盈触发价格为设置止盈单必填字段，止损触发价格为设置止损单必填字段；若缺省触发价格字段则不会设置对应的止盈单或止损单。

###   开平方向

开多：买入开多(direction用buy、offset用open)

平多：卖出平多(direction用sell、offset用close)

开空：卖出开空(direction用sell、offset用open)

平空：买入平空(direction用buy、offset用close)

> Response:

```json

{
    "status": "ok",
    "data": {
        "order_id": 770323133537685504,
        "client_order_id": 57012021022,
        "order_id_str": "770323133537685504"
    },
    "ts": 1603700946949
}

```

###  返回参数

| 参数名称            | 是否必须 | 类型     | 描述                     | 取值范围           |
| --------------- | ---- | ------ | ---------------------- | -------------- |
| status          | true | string | 请求处理结果                 | "ok" , "error" |
| \<data\>      | true     |  object       |      |   |
| order_id        | true | long   | 订单ID                   |                |
| order_id_str        | true | string   | String类型订单ID                   |                |
| client_order_id | false | long   | 用户下单时填写的客户端订单ID，没填则不返回 |                |
| \</data\>     |      |         |                 |    |
| ts    | true | long   | 响应生成时间点，单位：毫秒          |     |

#### 备注
 - order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。

## 【全仓】合约下单

 - POST `/linear-swap-api/v1/swap_cross_order`

#### 备注
 - 该接口仅支持全仓模式。

> Request

```json
{
    "contract_code": "btc-usdt",
    "direction": "buy",
    "offset":"open",
    "price":"29999",
    "lever_rate": 5,
    "volume": 1,
    "order_price_type":"opponent",
    "tp_trigger_price": 31000,
    "tp_order_price": 31000,
    "tp_order_price_type": "optimal_5",
    "sl_trigger_price": "29100",
    "sl_order_price": "29100",
    "sl_order_price_type": "optimal_5"
}
```

###  请求参数

| 参数名           | 必填  | 参数类型 | 描述                                             | 取值范围                                                     |
| ---------------- | ----- | -------- | ------------------------------------------------ | ------------------------------------------------------------ |
| contract_code    | true  | string   | 合约代码                                         | "BTC-USDT"...                    |
| client_order_id  | false | long     | 客户自己填写和维护，必须为数字,请注意必须小于等于9223372036854775807 |                                                              |
| price            | false | decimal  | 价格                                             |                                                              |
| volume           | true  | long     | 委托数量(张)                                     |                                                              |
| direction        | true  | string   | 仓位方向                                         | "buy":买 "sell":卖                                           |
| offset           | true  | string   | 开平方向                                         | "open":开 "close":平                                         |
| lever_rate       | true  | int      | 杠杆倍数,“开仓”若有10倍多单，就不能再下20倍多单;首次使用高倍杠杆(>20倍)，请使用主账号登录web端同意高倍杠杆协议后，才能使用接口下高倍杠杆(>20倍)] |                                                              |
| order_price_type | true  | string   | 订单报价类型                                     | "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档，ioc:IOC订单，fok：FOK订单, "opponent_ioc": 对手价-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| tp_trigger_price   | decimal | false  | 止盈触发价格                  |                            |
| tp_order_price   |  decimal | false | 	止盈委托价格（最优N档委托类型时无需填写价格）                  |  |
| tp_order_price_type   | string |  false | 止盈委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |
| sl_trigger_price          | decimal | false | 止损触发价格                  |                            |
| sl_order_price   | decimal |  false | 	止损委托价格（最优N档委托类型时无需填写价格）                  |  |
| sl_order_price_type   |  string | false | 止损委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |

####  备注

 - "limit":限价，"post_only":只做maker单，ioc:IOC订单，fok：FOK订单，这四种报价类型需要传价格，其他都不需要。

 - 若存在持仓，那么下单时杠杆倍数必须与持仓杠杆相同，否则下单失败。若需使用新杠杆下单，则必须先使用切换杠杆接口将持仓杠杆切换成功后再下单。

 - 只有开仓订单才支持设置止盈止损。

 - 止盈触发价格为设置止盈单必填字段，止损触发价格为设置止损单必填字段；若缺省触发价格字段则不会设置对应的止盈单或止损单。

###   开平方向

开多：买入开多(direction用buy、offset用open)

平多：卖出平多(direction用sell、offset用close)

开空：卖出开空(direction用sell、offset用open)

平空：买入平空(direction用buy、offset用close)

> Response

```json

{
    "status": "ok",
    "data": {
        "order_id": 784017187857760256,
        "order_id_str": "784017187857760256"
    },
    "ts": 1606965863952
}

```

###  返回参数

| 参数名称            | 是否必须 | 类型     | 描述                     | 取值范围           |
| --------------- | ---- | ------ | ---------------------- | -------------- |
| status          | true | string | 请求处理结果                 | "ok" , "error" |
| \<data\>      | true     |  object       |      |   |
| order_id        | true | long   | 订单ID                   |                |
| order_id_str        | true | string   | String类型订单ID                   |                |
| client_order_id | false | long   | 用户下单时填写的客户端订单ID，没填则不返回 |                |
| \</data\>     |      |         |                 |    |
| ts    | true | long   | 响应生成时间点，单位：毫秒          |     |

####备注

order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。

## 【逐仓】合约批量下单 

###  示例

- POST  `/linear-swap-api/v1/swap_batchorder`

#### 备注
 - 该接口仅支持逐仓模式。

> Request

```json
{
    "orders_data": [
        {
            "contract_code": "btc-usdt",
            "direction": "sell",
            "offset": "open",
            "price": "29999",
            "lever_rate": 5,
            "volume": 1,
            "order_price_type": "opponent",
            "tp_trigger_price": 27000,
            "tp_order_price": 27000,
            "tp_order_price_type": "optimal_5",
            "sl_trigger_price": "30100",
            "sl_order_price": "30100",
            "sl_order_price_type": "optimal_5"
        },
        {
            "contract_code": "btc-usdt",
            "direction": "buy",
            "offset": "open",
            "price": "29999",
            "lever_rate": 5,
            "volume": 1,
            "order_price_type": "post_only",
            "tp_trigger_price": 31000,
            "tp_order_price": 31000,
            "tp_order_price_type": "optimal_5",
            "sl_trigger_price": "29100",
            "sl_order_price": "29100",
            "sl_order_price_type": "optimal_5"
        }
    ]
}
```

###  请求参数

参数名  |    参数类型   |  必填   |  描述  |
---------------------------------- | -------------- |  ---------- | -------------------------------------------------------------- |
orders_data  | List\<Object\>   |    |    |  

- orders_data对象参数详情

| 参数名  |    参数类型   |  必填   |  描述  |   取值范围   |
| -------- | -------------- |  ---------- | ---------- | ---------- |
| contract_code        | true <img width=250/> | string <img width=250/>  |  合约代码 <img width=1000/>  |        "BTC-USDT"...          |
| client_order_id       |  false   |  long| 客户自己填写和维护，必须为数字,请注意必须小于等于9223372036854775807  |      |
| price       |false  | decimal | 价格 |      |
| volume   | true    |  long | 委托数量(张)  |      |
| direction   |true   |  string | 仓位方向   |  "buy":买 "sell":卖    |
| offset   | true  |  string |   开平方向    |  "open":开 "close":平    |
| lever_rate     |  true    | int  | 杠杆倍数[“开仓”若有10倍多单，就不能再下20倍多单;首次使用高倍杠杆(>20倍)，请使用主账号登录web端同意高倍杠杆协议后，才能使用接口下高倍杠杆(>20倍)]             |      |
| order_price_type            |  true |  string | 订单报价类型  | "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档，ioc:IOC订单，fok：FOK订单, "opponent_ioc": 对手价-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| tp_trigger_price   | decimal | false  | 止盈触发价格                  |                            |
| tp_order_price   |  decimal | false | 	止盈委托价格（最优N档委托类型时无需填写价格）                  |  |
| tp_order_price_type   | string |  false | 止盈委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |
| sl_trigger_price          | decimal | false | 止损触发价格                  |                            |
| sl_order_price   | decimal |  false | 	止损委托价格（最优N档委托类型时无需填写价格）                  |  |
| sl_order_price_type   |  string | false | 止损委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |

###  备注

 - 对手价下单price价格参数不用传，对手价下单价格是买一和卖一价,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档下单price价格参数不用传，"limit":限价，"post_only":只做maker单 需要传价格。

 - 若存在持仓，那么下单时杠杆倍数必须与持仓杠杆相同，否则下单失败。若需使用新杠杆下单，则必须先使用切换杠杆接口将持仓杠杆切换成功后再下单。

 - 只有开仓订单才支持设置止盈止损。

 - 止盈触发价格为设置止盈单必填字段，止损触发价格为设置止损单必填字段；若缺省触发价格字段则不会设置对应的止盈单或止损单。

一次最多允许10个订单。

> Response:

```json

{
    "status": "ok",
    "data": {
        "errors": [
            {
                "index": 2,
                "err_code": 1050,
                "err_msg": "Customers order number is repeated. Please try again later."
            }
        ],
        "success": [
            {
                "order_id": 770323847022211072,
                "client_order_id": 57012021024,
                "index": 1,
                "order_id_str": "770323847022211072"
            }
        ]
    },
    "ts": 1603701117058
}

```

###  返回参数

| 参数名称                    | 是否必须 | 类型     | 描述                     | 取值范围           |
| ----------------------- | ---- | ------ | ---------------------- | -------------- |
| status                  | true | string | 请求处理结果                 | "ok" , "error" |
| \<data\> |    true  |   object array     |                        |                |
| \<errors\> |    true  |   object array     |                        |                |
| index                   | true | int    | 订单索引                   |                |
| err_code                | true | int    | 错误码                    |                |
| err_msg                 | true | string | 错误信息                   |                |
| \</errors\>               |      |        |                        |                |
| \<success\> |      |        |                        |                |
| index                   | true | int    | 订单索引                   |                |
| order_id                | true | long   | 订单ID                   |                |
| order_id_str                | true | string   | string格式的订单ID                   |                |
| client_order_id         | true | long   | 用户下单时填写的客户端订单ID，没填则不返回 |                |
| \</success\>               |      |        |                        |                |
| \</data\>               |      |        |                        |                |
| ts                      | true | long   | 响应生成时间点，单位：毫秒          |

### 备注
 - order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。



## 【全仓】合约批量下单 

 - POST `/linear-swap-api/v1/swap_cross_batchorder`

#### 备注
 - 该接口仅支持全仓模式。

> Request

```json
{
    "orders_data": [
        {
            "contract_code": "btc-usdt",
            "direction": "sell",
            "offset": "open",
            "price": "29999",
            "lever_rate": 5,
            "volume": 1,
            "order_price_type": "opponent",
            "tp_trigger_price": 27000,
            "tp_order_price": 27000,
            "tp_order_price_type": "optimal_5",
            "sl_trigger_price": "30100",
            "sl_order_price": "30100",
            "sl_order_price_type": "optimal_5"
        },
        {
            "contract_code": "btc-usdt",
            "direction": "buy",
            "offset": "open",
            "price": "29999",
            "lever_rate": 5,
            "volume": 1,
            "order_price_type": "post_only",
            "tp_trigger_price": 31000,
            "tp_order_price": 31000,
            "tp_order_price_type": "optimal_5",
            "sl_trigger_price": "29100",
            "sl_order_price": "29100",
            "sl_order_price_type": "optimal_5"
        }
    ]
}
```

###  请求参数

| 参数名称            | 是否必须 | 类型     | 描述                     | 取值范围           |
| --------------- | ---- | ------ | ---------------------- | -------------- |
| \<orders_data\>   | true | object array |     |  |
| contract_code        | true | string   |  合约代码      |        "BTC-USDT"...          |
| client_order_id       |  false   |  long| 客户自己填写和维护，必须为数字,请注意必须小于等于9223372036854775807  |      |
| price       |false  | decimal | 价格 |      |
| volume   | true    |  long | 委托数量(张)  |      |
| direction   |true   |  string | 仓位方向   |  "buy":买 "sell":卖    |
| offset   | true  |  string |   开平方向    |  "open":开 "close":平    |
| lever_rate     |  true    | int  | 杠杆倍数,“开仓”若有10倍多单，就不能再下20倍多单;首次使用高倍杠杆(>20倍)，请使用主账号登录web端同意高倍杠杆协议后，才能使用接口下高倍杠杆(>20倍)]            |      |
| order_price_type            |  true |  string | 订单报价类型  | "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档，ioc：IOC订单，fok：FOK订单,"opponent_ioc": 对手价-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| tp_trigger_price   | decimal | false  | 止盈触发价格                  |                            |
| tp_order_price   |  decimal | false | 	止盈委托价格（最优N档委托类型时无需填写价格）                  |  |
| tp_order_price_type   | string |  false | 止盈委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |
| sl_trigger_price          | decimal | false | 止损触发价格                  |                            |
| sl_order_price   | decimal |  false | 	止损委托价格（最优N档委托类型时无需填写价格）                  |  |
| sl_order_price_type   |  string | false | 止损委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |
| \</orders_data\>     |         |       |   |      |

####  备注

 - "limit":限价，"post_only":只做maker单，ioc:IOC订单，fok：FOK订单，这四种报价类型需要传价格，其他都不需要。

 - 若存在持仓，那么下单时杠杆倍数必须与持仓杠杆相同，否则下单失败。若需使用新杠杆下单，则必须先使用切换杠杆接口将持仓杠杆切换成功后再下单。

 - 只有开仓订单才支持设置止盈止损。

 - 止盈触发价格为设置止盈单必填字段，止损触发价格为设置止损单必填字段；若缺省触发价格字段则不会设置对应的止盈单或止损单。

 - 一次最多允许10个订单。

> Response:

```json
{
    "status": "ok",
    "data": {
        "errors": [
            {
                "index": 2,
                "err_code": 1045,
                "err_msg": "Unable to switch leverage due to open orders."
            }
        ],
        "success": [
            {
                "order_id": 784022175422087168,
                "index": 1,
                "order_id_str": "784022175422087168"
            }
        ]
    },
    "ts": 1606967053089
}

```

###  返回参数

| 参数名称                    | 是否必须 | 类型     | 描述                     | 取值范围           |
| ----------------------- | ---- | ------ | ---------------------- | -------------- |
| status                  | true | string | 请求处理结果                 | "ok" , "error" |
| \<data\>  |    true  |   object     |                        |                |
| \<errors\> |    true  |   object array     |                        |                |
| index                   | true | int    | 订单索引                   |                |
| err_code                | true | int    | 错误码                    |                |
| err_msg                 | true | string | 错误信息                   |                |
| \</errors\>               |      |        |                        |                |
| \<success\> |      |        |                        |                |
| index                   | true | int    | 订单索引                   |                |
| order_id                | true | long   | 订单ID                   |                |
| order_id_str                | true | string   | string格式的订单ID                   |                |
| client_order_id         | true | long   | 用户下单时填写的客户端订单ID，没填则不返回 |                |
| \</success\>               |      |        |                        |                |
| \</data\>               |      |        |                        |                |
| ts                      | true | long   | 响应生成时间点，单位：毫秒          |

#### 备注

 - order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。

## 【逐仓】撤销订单 

###  示例

- POST `/linear-swap-api/v1/swap_cancel`

#### 备注
 - 该接口仅支持逐仓模式。

###  请求参数

| 参数名称            | 是否必须 | 类型     | 描述                     | 取值范围           |
| --------------- | ---- | ------ | ---------------------- | -------------- |
| order_id        | false | string | 订单ID(多个订单ID中间以","分隔,一次最多允许撤消10个订单)   |      |
| client_order_id | false | string | 客户订单ID(多个订单ID中间以","分隔,一次最多允许撤消10个订单) |      |
| contract_code          | true  | string | 合约代码                       |    "BTC-USDT" ...  |

#### 备注：

 - order_id和client_order_id都可以用来撤单，同时只可以设置其中一种，如果设置了两种，默认以order_id来撤单。

 - 撤单接口返回结果只代表撤单命令发送成功，建议根据订单查询接口查询订单的状态来确定订单是否已真正撤销。
 
 - client_order_id，24小时有效，超过24小时的订单根据client_order_id将查询不到。

> Response:

```json

{
    "status": "ok",
    "data": {
        "errors": [
            {
                "order_id": "770323133537685504",
                "err_code": 1071,
                "err_msg": "Repeated withdraw."
            }
        ],
        "successes": "770323847022211072"
    },
    "ts": 1603701351602
}

```

###  返回参数

参数名称  |  是否必须  |  类型  |  描述  |  取值范围  |
---------------------------- | -------------- | ---------- | -------------------------------------------------- | ---------------- |
status  |  true  |  string  |  请求处理结果  | "ok" , "error"  | 
\<data\>  |    |    |    |    |  
\<errors\>  |    |    |    |    |  
order_id  |    true  |  string  |  订单ID  |    |   
err_code  |   true  |  int  |   错误码  |    |   
err_msg  |  true  |  string  |  错误信息  |    | 
\</errors\>  |    |    |    |    |
successes  |   true  |  string  |  撤销成功的订单的order_id或client_order_id列表  |   |
\</data\>  |    |    |    |    |
ts  |  true  |  long  |  响应生成时间点，单位：毫秒  |   |

## 【全仓】撤销订单

 - POST `/linear-swap-api/v1/swap_cross_cancel`

#### 备注
 - 该接口仅支持全仓模式。

###  请求参数

| 参数名称            | 是否必须 | 类型     | 描述                     | 取值范围           |
| --------------- | ---- | ------ | ---------------------- | -------------- |
| order_id        | false | string | 订单ID(多个订单ID中间以","分隔,一次最多允许撤消10个订单)   |      |
| client_order_id | false | string | 客户订单ID(多个订单ID中间以","分隔,一次最多允许撤消10个订单) |      |
| contract_code          | true  | string | 合约代码                       |    "BTC-USDT" ...  |

### 备注：

 - order_id和client_order_id都可以用来撤单，同时只可以设置其中一种，如果设置了两种，默认以order_id来撤单。

 - 撤单接口返回结果只代表撤单命令发送成功，建议根据订单查询接口查询订单的状态来确定订单是否已真正撤销。
 
 - client_order_id，24小时有效，超过24小时的订单根据client_order_id将查询不到。
 
> Response

```json

{
    "status": "ok",
    "data": {
        "errors": [
            {
                "order_id": "784054331179532288",
                "err_code": 1062,
                "err_msg": "Cancelling. Please be patient."
            }
        ],
        "successes": "784054331179532288"
    },
    "ts": 1606974744952
}
```

###  返回参数

| 参数名称                   | 是否必须 | 类型     | 描述                                 | 取值范围           |
| ---------------------- | ---- | ------ | ---------------------------------- | -------------- |
| status                 | true | string | 请求处理结果                             | "ok" , "error" |
| \<data\> |  true    |   object       |        |    |
| \<errors\>|  true    | object array       |                                    |                |
| order_id               | true | string | 订单ID                               |                |
| err_code               | true | int    | 错误码                                |                |
| err_msg                | true | string | 错误信息                               |                |
| \</errors\>              |      |        |                                    |                |
| successes              | true | string | 撤销成功的订单的order_id或client_order_id列表 |                |
| \</data\>        |      |         |        |         |
| ts                     | true | long   | 响应生成时间点，单位：毫秒                      |                |

## 【逐仓】全部撤单 

###  示例

- POST  `/linear-swap-api/v1/swap_cancelall`

#### 备注
 - 该接口仅支持逐仓模式。

###  请求参数

| 参数名称  | 是否必须 | 类型 | 描述  | 取值范围 |
| ------------- | ------ | ----- | ---------------------------------------- | ---- |
| contract_code | true |  string | 合约代码 |   "BTC-USDT"    |
| direction | false  | string | 买卖方向（不填默认全部）  |  "buy":买 "sell":卖 |
| offset | false  | string | 开平方向（不填默认全部）  | "open":开 "close":平  |

#### 备注：
 - direction与offset可只填其一，只填其一则按对应的条件去撤单。（如用户只传了direction=buy，则撤销所有买单，包括开仓和平仓）

> Response:(多笔订单返回结果(成功订单ID,失败订单ID))

```json

{
    "status": "ok",
    "data": {
        "errors": [],
        "successes": "768883002062282752,770325103371542528,770325103388319744"
    },
    "ts": 1603701437838
}
    
```

###  返回参数

参数名称  |  是否必须   |  类型  |  描述  |  取值范围  |
---------------------------- | -------------- | ---------- | ---------------------------- | ---------------- |
status  |  true  |  string  |  请求处理结果  | "ok" , "error"  | 
\<data\>  |    |    |    |    |
\<errors\>  |    |    |    |    |
order_id  |    true  |  string  |  订单id  |   | 
err_code  |    true  |  int  |   订单失败错误码  |   |   
err_msg  |  true  |  string  |   订单失败信息  |    | 
\</errors\>    |    |    |    |    |
successes  |    true  |  string  |  成功的订单  |    |   
\</data\>    |    |    |    |    |
ts  | true  |  long  |  响应生成时间点，单位：毫秒  |   | 

## 【全仓】全部撤单

 - POST `/linear-swap-api/v1/swap_cross_cancelall`

#### 备注
 - 该接口仅支持全仓模式。

###  请求参数

| 参数名称  | 是否必须 | 类型 | 描述  | 取值范围 |
| ------------- | ------ | ----- | ---------------------------------------- | ---- |
| contract_code | true |  string | 合约代码 |   "BTC-USDT"    |
| direction | false  | string | 买卖方向（不填默认全部）  |  "buy":买 "sell":卖 |
| offset | false  | string | 开平方向（不填默认全部）  | "open":开 "close":平  |

#### 备注：
 - direction与offset可只填其一，只填其一则按对应的条件去撤单。（如用户只传了direction=buy，则撤销所有买单，包括开仓和平仓）

> Response

```json

{
    "status": "ok",
    "data": {
        "errors": [],
        "successes": "784055473531781120,784055473842159616"
    },
    "ts": 1606974998510
}
```

###  返回参数

| 参数名称                   | 是否必须 | 类型     | 描述            | 取值范围           |
| ---------------------- | ---- | ------ | ------------- | -------------- |
| status                 | true | string | 请求处理结果        | "ok" , "error" |
| \<data\> |  true    |   object array      |        |    |
| \<errors\> |  true    | object array       |               |                |
| order_id               | true | String | 订单id          |                |
| err_code               | true | int    | 订单失败错误码       |                |
| err_msg                | true | string    | 订单失败信息        |                |
| \</errors\>              |      |        |               |                |
| successes              | true | string | 成功的订单         |                |
| \</data\>        |      |         |        |         |
| ts                     | true | long   | 响应生成时间点，单位：毫秒 |                |

## 【逐仓】切换杠杆

- POST `/linear-swap-api/v1/swap_switch_lever_rate`

#### 备注
- 该接口仅支持逐仓模式。

- 只有在单个品种下只有持仓，且没有挂单的场景下，才可以切换该品种当前的倍数。

- 接口限制请求次数为每3秒一次。

### 请求参数

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| contract_code | true | string | 合约代码	 | 比如“BTC-USDT” |
| lever_rate | true | int | 要切换的杠杆倍数;首次使用高倍杠杆(>20倍)，请使用主账号登录web端同意高倍杠杆协议后，才能使用接口下高倍杠杆(>20倍) |  |

> ** 响应示例**

```json

正确：
{
    "status": "ok",
    "data": {
        "contract_code": "btc-usdt",
        "margin_mode": "isolated",
        "lever_rate": 10
    },
    "ts": 1603699417036
}
错误：
{
    "status": "error",
    "err_code": 1045,
    "err_msg": "Unable to switch leverage due to current holdings or open orders.",
    "ts": 1603701654205
}
```

### **响应参数**
| 参数名称                   | 是否必须 | 类型      | 描述                 | 取值范围                                     |
| ---------------------- | ---- | ------- | ------------------ | ---------------------------------------- |
| status                 | true | string  | 响应状态: ok,error            |                                          |
| \<data\> | false     |  object      |                    |                                          |
| contract_code               | false | string    | 合约代码      |                                          |
| margin_mode           | false | string |  保证金模式  | isolated：逐仓模式 |
| lever_rate               | false | int    | 切换成功后的杠杆倍数      |                                          |
| \</data\>            |      |         |                    |                                          |
| err_code | false | int | 错误码| |
| err_msg| false| string | 错误信息| |
| ts                     | true | long    | 时间戳                |                                          |

## 【全仓】切换杠杆

 - POST `/linear-swap-api/v1/swap_cross_switch_lever_rate`

#### 备注
 - 该接口仅支持全仓模式。

 - 只有在单个品种下只有持仓，且没有挂单的场景下，才可以切换该品种当前的倍数。

 - 接口限制请求次数为每3秒一次。

###  请求参数

| 参数名称  | 是否必须 | 类型 | 描述  | 取值范围 |
| ------------- | ------ | ----- | ---------------------------------------- | ---- |
| contract_code | true | string | 合约代码	 | "BTC-USDT", |
| lever_rate | true | int | 要切换的杠杆倍数；首次使用高倍杠杆(>20倍)，请使用主账号登录web端同意高倍杠杆协议后，才能使用接口下高倍杠杆(>20倍)	 | |

> Response

```json

{
    "status": "ok",
    "data": {
        "contract_code": "eth-usdt",
        "lever_rate": 30,
        "margin_mode": "cross"
    },
    "ts": 1606975779177
}

```

###  返回参数

| 参数名称                   | 是否必须 | 类型     | 描述            | 取值范围           |
| ---------------------- | ---- | ------ | ------------- | -------------- |
| status                 | true | string  | 响应状态: ok,error            |                                          |
| \<data\> | false     |  object      |                    |                                          |
| contract_code               | false | string    |  合约代码      |                                          |
| margin_mode | false | string | 保证金模式  | cross：全仓模式； |
| lever_rate               | false | int    | 切换成功后的杠杆倍数      |                                          |
| \</data\>            |      |         |                    |                                          |
| err_code | false | int | 错误码| |
| err_msg| false| string | 错误信息| |
| ts                     | true | long    | 时间戳                |                                          |

## 【逐仓】获取合约订单信息

###  示例

- POST  `/linear-swap-api/v1/swap_order_info`

#### 备注
 - 该接口仅支持逐仓模式。

###  请求参数

| 参数名称            | 是否必须  | 类型     | 描述                                   | 取值范围     |
| --------------- | ----- | ------ | ------------------------------------ | ---- |
| order_id        | false（请看备注） | string | 订单ID(多个订单ID中间以","分隔,一次最多允许查询50个订单)   |      |
| client_order_id | false（请看备注） | string | 客户订单ID(多个订单ID中间以","分隔,一次最多允许查询50个订单) |      |
| contract_code          | true  | string | 合约代码 |"BTC-USDT"...                       |

###  备注：

- 最多只能查询4小时内的撤单信息。

- order_id和client_order_id至少要填写一个。

- order_id和client_order_id都可以用来查询，同时只可以设置其中一种，如果设置了两种，默认以order_id来查询。结算后，会把结束状态的订单（5部分成交已撤单 6全部成交 7已撤单）删除掉。

- client_order_id，24小时有效，超过24小时的订单根据client_order_id将查询不到。

> Response:

```json

{
    "status": "ok",
    "data": [
        {
            "symbol": "BTC",
            "contract_code": "BTC-USDT",
            "volume": 1,
            "price": 13059.8,
            "order_price_type": "opponent",
            "order_type": 1,
            "direction": "sell",
            "offset": "open",
            "lever_rate": 10,
            "order_id": 770334322963152896,
            "client_order_id": 57012021045,
            "created_at": 1603703614712,
            "trade_volume": 1,
            "trade_turnover": 13.059800000000000000,
            "fee": -0.005223920000000000,
            "trade_avg_price": 13059.800000000000000000,
            "margin_frozen": 0,
            "profit": 0,
            "status": 6,
            "order_source": "api",
            "order_id_str": "770334322963152896",
            "fee_asset": "USDT",
            "liquidation_type": "0",
            "canceled_at": 0,
            "margin_asset": "USDT",
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT",
            "is_tpsl": 0,
            "real_profit": 0
        }
    ],
    "ts": 1603703631815
}
    
```

###  返回数据

| 参数名称                 | 是否必须 | 类型      | 描述     | 取值范围                                     |
| -------------------- | ---- | ------- | ------ | ---------------------------------------- |
| status               | true <img width=250/> | string  | 请求处理结果 <img width=1000/> | "ok" , "error"                           |
| \<data\> |  true    |   object array      |        |    |
| symbol               | true | string  | 品种代码   |       |
| contract_code        | true | string  | 合约代码   | "BTC-USDT" ...   |
| volume               | true | decimal | 委托数量   |   |
| price                | true | decimal | 委托价格   |            |
| order_price_type     | true | string  | 订单报价类型 |  "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| direction            | true | string  | 买卖方向  | "buy":买 "sell":卖  |
| offset  | true | string  | 开平方向   | "open":开 "close":平    |
| lever_rate           | true | int     | 杠杆倍数   |    |
| order_id             | true | long    | 订单ID   |    |
| order_id_str             | true | string    | String类型订单ID   |    |
| client_order_id      | true | long    | 客户订单ID |    |
| created_at           | true | long    | 创建时间   |     |
| trade_volume         | true | decimal | 成交数量   |   |
| trade_turnover       | true | decimal | 成交总金额 ，即sum（每一笔成交张数 * 合约面值 * 成交价格）  |     |
| fee                  | true | decimal | 手续费    |     |
| trade_avg_price      | true | decimal | 成交均价   |   |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_frozen        | true | decimal | 冻结保证金  |     |
| profit               | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）     |        |
| status               | true | int     | 订单状态   | (1准备提交 2准备提交 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单 11撤单中) |
| order_type           | true | int  | 订单类型   | 1:报单 、 2:撤单 、 3:强平、4:交割                  |
| order_source         | true | string  | 订单来源   | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发 ） |
| fee_asset         | true | string  | 手续费币种   | （"USDT"...）|
| liquidation_type               | true     | string    | 结算类型 0:非强平类型，1：多空轧差， 2:部分接管，3：全部接管           |  |
| canceled_at               | true     | long    |撤单时间           |  |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| margin_mode | true | string | 保证金模式  |isolated：逐仓模式 |
| is_tpsl | true | int | 是否设置止盈止损  | 1：是；0：否 |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \</data\>        |      |         |        |         |
| ts                   | true | long    | 时间戳    |      |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 只有在2021年1月30日0点后创建的订单，真实收益（real_profit）字段才会有值。存量数据均为0。
 
 
## 【全仓】获取合约订单信息

 - POST `/linear-swap-api/v1/swap_cross_order_info`

#### 备注
 - 该接口仅支持全仓模式。

###  请求参数

| 参数名称            | 是否必须  | 类型     | 描述                                   | 取值范围     |
| --------------- | ----- | ------ | ------------------------------------ | ---- |
| order_id        | false（请看备注） | string | 订单ID(多个订单ID中间以","分隔,一次最多允许查询50个订单)   |      |
| client_order_id | false（请看备注） | string | 客户订单ID(多个订单ID中间以","分隔,一次最多允许查询50个订单) |      |
| contract_code          | true  | string | 合约代码 |"BTC-USDT"...                       |

####  备注：
 - 最多只能查询4小时内的撤单信息。

 - order_id和client_order_id至少要填写一个。

 - order_id和client_order_id都可以用来查询，同时只可以设置其中一种，如果设置了两种，默认以order_id来查询。结算后，会把结束状态的订单（5部分成交已撤单 6全部成交 7已撤单）删除掉。

 - client_order_id，24小时有效，超过24小时的订单根据client_order_id将查询不到。

> Response

```json
{
    "status": "ok",
    "data": [
        {
            "symbol": "ETH",
            "contract_code": "ETH-USDT",
            "volume": 1,
            "price": 17,
            "order_price_type": "optimal_10_ioc",
            "order_type": 1,
            "direction": "sell",
            "offset": "open",
            "lever_rate": 5,
            "order_id": 784056956650258432,
            "client_order_id": null,
            "created_at": 1606975345528,
            "trade_volume": 1,
            "trade_turnover": 0.5,
            "fee": -0.0002,
            "trade_avg_price": 50,
            "margin_frozen": 0,
            "profit": 0,
            "status": 6,
            "order_source": "api",
            "order_id_str": "784056956650258432",
            "fee_asset": "USDT",
            "liquidation_type": "0",
            "canceled_at": 0,
            "margin_asset": "USDT",
            "margin_account": "USDT",
            "margin_mode": "cross",
            "is_tpsl":0,
            "real_profit": 0
        }
    ],
    "ts": 1606975356655
}
```

###  返回数据

| 参数名称                 | 是否必须 | 类型      | 描述     | 取值范围                                     |
| -------------------- | ---- | ------- | ------ | ---------------------------------------- |
| status               | true <img width=250/> | string  | 请求处理结果 <img width=1000/> | "ok" , "error"                           |
| \<data\> |  true    |   object array      |        |    |
| symbol               | true | string  | 品种代码   |       |
| contract_code        | true | string  | 合约代码   | "BTC-USDT" ...   |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| volume               | true | decimal | 委托数量   |   |
| price                | true | decimal | 委托价格   |            |
| order_price_type     | true | string  | 订单报价类型 |  "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| direction            | true | string  | 买卖方向  | "buy":买 "sell":卖  |
| offset  | true | string  | 开平方向   | "open":开 "close":平    |
| lever_rate           | true | int     | 杠杆倍数   |    |
| order_id             | true | long    | 订单ID   |    |
| order_id_str             | true | string    | String类型订单ID   |    |
| client_order_id      | true | long    | 客户订单ID |    |
| created_at           | true | long    | 创建时间   |     |
| trade_volume         | true | decimal | 成交数量   |   |
| trade_turnover       | true | decimal | 成交总金额 ，即sum（每一笔成交张数 * 合约面值 * 成交价格）  |     |
| fee                  | true | decimal | 手续费    |     |
| trade_avg_price      | true | decimal | 成交均价   |   |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_frozen        | true | decimal | 冻结保证金  |     |
| profit               | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）     |        |
| status               | true | int     | 订单状态   | (1准备提交 2准备提交 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单 11撤单中) |
| order_type           | true | int  | 订单类型   | 1:报单 、 2:撤单 、 3:强平、4:交割                  |
| order_source         | true | string  | 订单来源   | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发） |
| fee_asset         | true | string  | 手续费币种   | （"USDT"...）|
| liquidation_type               | true     | string    | 结算类型 0:非强平类型，1：多空轧差， 2:部分接管，3：全部接管           |  |
| canceled_at               | true     | long    |撤单时间           |  |
| is_tpsl               | true     | int    | 是否设置止盈止损           | 1：是；0：否  |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \</data\>        |      |         |        |         |
| ts                   | true | long    | 时间戳    |      |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 只有在2021年1月30日0点后创建的订单，真实收益（real_profit）字段才会有值。存量数据均为0。

## 【逐仓】获取订单明细信息

###  示例

- POST `/linear-swap-api/v1/swap_order_detail`

#### 备注
 - 该接口仅支持逐仓模式。

###  请求参数

| 参数名称       | 是否必须  | 类型     | 描述                           |    取值范围  |
| ---------- | ----- | ------ | ---------------------------- | ---- |
| contract_code     | true  | string | 合约代码| "BTC-USDT"...     |
| order_id   | true  | long   | 订单id                         |      |
| created_at | false  | long   | 下单时间戳                        |      |
| order_type | false  | int    | 订单类型|  1:报单 、 2:撤单 、 3:强平、4:交割     |
| page_index | false | int    | 第几页,不填第一页                    |      |
| page_size  | false | int    | 不填默认20，不得多于50                |      |

### 备注

获取订单明细接口查询撤单数据时，如果传“created_at”和“order_type”参数则能查询最近24小时数据，如果不传“created_at”和“order_type”参数只能查询到最近2小时数据。

order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。

created_at使用13位long类型时间戳（包含毫秒时间），如果输入准确的时间戳，查询性能将会提升。例如:"2019/10/18 10:26:22"转换为时间戳为：1571365582123。也可以直接从swap_order下单接口返回的ts中获取时间戳查询对应的订单。

created_at禁止传0。


> Response:

```json

{
    "status": "ok",
    "data": {
        "symbol": "BTC",
        "contract_code": "BTC-USDT",
        "instrument_price": 0,
        "final_interest": 0,
        "adjust_value": 0,
        "lever_rate": 10,
        "direction": "sell",
        "offset": "open",
        "volume": 1.000000000000000000,
        "price": 13059.800000000000000000,
        "created_at": 1603703614712,
        "canceled_at": 0,
        "order_source": "api",
        "order_price_type": "opponent",
        "margin_frozen": 0,
        "profit": 0,
        "trades": [
            {
                "trade_id": 131560927,
                "trade_price": 13059.800000000000000000,
                "trade_volume": 1.000000000000000000,
                "trade_turnover": 13.059800000000000000,
                "trade_fee": -0.005223920000000000,
                "created_at": 1603703614715,
                "role": "taker",
                "fee_asset": "USDT",
                "real_profit": 0,
                "profit": 0,
                "id": "131560927-770334322963152896-1"
            }
        ],
        "total_page": 1,
        "current_page": 1,
        "total_size": 1,
        "liquidation_type": "0",
        "fee_asset": "USDT",
        "fee": -0.005223920000000000,
        "order_id": 770334322963152896,
        "order_id_str": "770334322963152896",
        "client_order_id": 57012021045,
        "order_type": "1",
        "status": 6,
        "trade_avg_price": 13059.800000000000000000,
        "trade_turnover": 13.059800000000000000,
        "trade_volume": 1.000000000000000000,
        "margin_asset": "USDT",
        "margin_mode": "isolated",
        "margin_account": "BTC-USDT",
        "is_tpsl": 0,
        "real_profit": 0
    },
    "ts": 1603703678477
}
    
```

###  返回数据

| 参数名称                    | 是否必须 | 类型      | 描述          | 取值范围                                     |
| ----------------------- | ---- | ------- | ----------- | ---------------------------------------- |
| status                  | true <img width=250/> | string  <img width=250/> | 请求处理结果 <img width=1000/>     | "ok" , "error"                           |
| \<data\> |  true    |  object       |             |    |
| symbol                  | true | string  | 品种代码        |      |
| contract_code           | true | string  | 合约代码     | "BTC-USDT"  |
| lever_rate              | true | int     | 杠杆倍数        | |
| direction               | true | string  | 买卖方向        | "buy":买 "sell":卖         |
| offset                  | true | string  | 开平方向        | "open":开 "close":平     |
| volume                  | true | decimal | 委托数量        | |
| price                   | true | decimal | 委托价格        |  |
| created_at              | true | long    | 创建时间        |  |
| canceled_at              | true | long     | 撤单时间        |        |
| order_source            | true | string  | 订单来源        | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发）   |
| order_price_type        | true | string  | 订单报价类型      | "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_frozen           | true | decimal | 冻结保证金       |    |
| profit                  | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）          |     |
| instrument_price        | true | decimal | 爆仓单合约价格     |     |
| final_interest          | true | decimal | 爆仓时合约权益     |     |
| adjust_value            | true | decimal | 爆仓时调整系数     |      |
| fee              | true | decimal     | 总手续费        |     |
| fee_asset              | true | string     | 手续费币种        |   （"USDT"...）                                       |
| liquidation_type              | true | string     | 强平类型    |      |
| order_id               | true     | long    | 订单id            |  |
| order_id_str               | true     | string    | string格式的订单id             |  |
| client_order_id               | true     | long    | 客户订单id             |  |
| order_type               | true     | string    | 订单类型             | 1:报单 、 2:撤单 、 3:强平、4:交割 |
| status               | true     | int    | 订单状态            | (1准备提交 2准备提交 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单 11撤单中)  |
| trade_avg_price               | true     | decimal    | 成交均价             |  |
| trade_turnover               | true     | decimal    | 成交总金额，即sum（每一笔成交张数 * 合约面值*成交价格）        |  |
| trade_volume               | true     | decimal    | 成交总数量           |  |
| total_page              | true | int     | 总共页数        |  |
| current_page            | true | int     | 当前页数        |    |
| total_size              | true | int     | 总条数         |      |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| is_tpsl | true | int | 是否设置止盈止损  | 1：是；0：否 |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \<trades\>  |  true    |   object array      |        |   |      |
| id                | true | string    | 全局唯一的交易标识       |   |
| trade_id                | true | long    | 与linear-swap-api/v1/swap_matchresults返回结果中的match_id一样，是撮合结果id， 非唯一，可重复，注意：一个撮合结果代表一个taker单和N个maker单的成交记录的集合，如果一个taker单吃了N个maker单，那这N笔trade都是一样的撮合结果id   |  |
| trade_price             | true | decimal | 成交价格        |   |
| trade_volume            | true | decimal | 成交量（张）         |   |
| trade_turnover          | true | decimal | 成交金额（成交数量*合约面值*成交价格）        |     |
| trade_fee               | true | decimal | 成交手续费       |      |
| role                    | true | string  | taker或maker |   |
| created_at              | true | long    | 创建时间        |      |
| real_profit             | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| profit                  | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）          |     |
| \</trades\>               |      |         |             |     |
| \</data\>            |      |         |             |         |
| ts                      | true | long    | 时间戳         |      |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 只有在2021年1月30日0点后创建的订单，订单级别的真实收益（real_profit）字段才会有值。而成交级别的真实收益（real_profit）在2020年12月10日后就会有值。

## 【全仓】获取订单明细信息

 - POST `/linear-swap-api/v1/swap_cross_order_detail`

#### 备注
 - 该接口仅支持全仓模式。

###  请求参数

| 参数名称       | 是否必须  | 类型     | 描述                           |    取值范围  |
| ---------- | ----- | ------ | ---------------------------- | ---- |
| contract_code     | true  | string | 合约代码| "BTC-USDT"...     |
| order_id   | true  | long   | 订单id                         |      |
| created_at | false  | long   | 下单时间戳                        |      |
| order_type | false  | int    | 订单类型|  1:报单 、 2:撤单 、 3:强平、4:交割     |
| page_index | false | int    | 第几页,不填第一页                    |      |
| page_size  | false | int    | 不填默认20，不得多于50                |      |

### 备注

获取订单明细接口查询撤单数据时，如果传“created_at”和“order_type”参数则能查询最近24小时数据，如果不传“created_at”和“order_type”参数只能查询到最近2小时数据。

order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。

created_at使用13位long类型时间戳（包含毫秒时间），如果输入准确的时间戳，查询性能将会提升。例如:"2019/10/18 10:26:22"转换为时间戳为：1571365582123。也可以直接从swap_order下单接口返回的ts中获取时间戳查询对应的订单。

created_at禁止传0。

> Response

```json
{
    "status": "ok",
    "data": {
        "symbol": "ETH",
        "contract_code": "ETH-USDT",
        "instrument_price": 0,
        "final_interest": 0,
        "adjust_value": 0,
        "lever_rate": 5,
        "direction": "sell",
        "offset": "open",
        "volume": 1,
        "price": 17,
        "created_at": 1606975345528,
        "canceled_at": 0,
        "order_source": "api",
        "order_price_type": "optimal_10_ioc",
        "margin_frozen": 0,
        "profit": 0,
        "trades": [
            {
                "trade_id": 33142,
                "trade_price": 50,
                "trade_volume": 1,
                "trade_turnover": 0.5,
                "trade_fee": -0.0002,
                "created_at": 1606975346393,
                "role": "taker",
                "fee_asset": "USDT",
                "real_profit": 0,
                "profit": 0,
                "id": "33142-784056956650258432-1"
            }
        ],
        "total_page": 1,
        "current_page": 1,
        "total_size": 1,
        "liquidation_type": "0",
        "fee_asset": "USDT",
        "fee": -0.0002,
        "order_id": 784056956650258432,
        "order_id_str": "784056956650258432",
        "client_order_id": null,
        "order_type": "1",
        "status": 6,
        "trade_avg_price": 50,
        "trade_turnover": 0.5,
        "trade_volume": 1,
        "margin_asset": "USDT",
        "margin_account": "USDT",
        "margin_mode": "cross",
        "is_tpsl": 0,
        "real_profit": 0
    },
    "ts": 1606975532569
}
```

###  返回数据

| 参数名称                    | 是否必须 | 类型      | 描述          | 取值范围                                     |
| ----------------------- | ---- | ------- | ----------- | ---------------------------------------- |
| status                  | true | string  | 请求处理结果      | "ok" , "error"                           |
| \<data\> |  true    |  object       |             |    |
| symbol                  | true | string  | 品种代码        |      |
| contract_code           | true | string  | 合约代码     | "BTC-USDT"  |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| lever_rate              | true | int     | 杠杆倍数        | |
| direction               | true | string  | 买卖方向        | "buy":买 "sell":卖         |
| offset                  | true | string  | 开平方向        | "open":开 "close":平     |
| volume                  | true | decimal | 委托数量        | |
| price                   | true | decimal | 委托价格        |  |
| created_at              | true | long    | 创建时间        |  |
| order_source            | true | string  | 订单来源        | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发） |
| order_price_type        | true | string  | 订单报价类型      |  "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_frozen           | true | decimal | 冻结保证金       |    |
| profit                  | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）          |     |
| instrument_price        | true | decimal | 爆仓单合约价格     |     |
| final_interest          | true | decimal | 爆仓时合约权益     |     |
| adjust_value            | true | decimal | 爆仓时调整系数     |      |
| fee              | true | decimal     | 总手续费        |     |
| fee_asset              | true | string     | 手续费币种        |   （"USDT"...）                                       |
| liquidation_type              | true | string     | 强平类型    |      |
| canceled_at              | true | long     | 撤单时间        |        |
| order_id               | true     | long    | 订单id            |  |
| order_id_str               | true     | string    | string格式的订单id             |  |
| client_order_id               | true     | long    | 客户订单id             |  |
| order_type               | true     | string    | 订单类型             | 1:报单 、 2:撤单 、 3:强平、4:交割 |
| status               | true     | int    | 订单状态            | (1准备提交 2准备提交 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单 11撤单中)  |
| trade_avg_price               | true     | decimal    | 成交均价             |  |
| trade_turnover               | true     | decimal    | 成交总金额，即sum（每一笔成交张数 * 合约面值*成交价格）        |  |
| trade_volume               | true     | decimal    | 成交总数量           |  |
| is_tpsl               | true     | int    | 是否设置止盈止损           | 1：是；0：否 |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| total_page              | true | int     | 总共页数        |  |
| current_page            | true | int     | 当前页数        |    |
| total_size              | true | int     | 总条数         |      |
| \<trades\>  |  true    |   object array      |        |   |      |
| id                | true | string    | 全局唯一的交易标识      |   |
| trade_id                | true | long    | 与linear-swap-api/v1/swap_cross_matchresults返回结果中的match_id一样，是撮合结果id， 非唯一，可重复，注意：一个撮合结果代表一个taker单和N个maker单的成交记录的集合，如果一个taker单吃了N个maker单，那这N笔trade都是一样的撮合结果id  |  |
| trade_price             | true | decimal | 成交价格        |   |
| trade_volume            | true | decimal | 成交量（张）         |   |
| trade_turnover          | true | decimal | 成交金额（成交数量*合约面值*成交价格）        |     |
| trade_fee               | true | decimal | 成交手续费       |      |
| role                    | true | string  | taker或maker |   |
| created_at              | true | long    | 创建时间        |      |
| profit                  | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）          |     |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \</trades\>               |      |         |             |     |
| \</data\>            |      |         |             |         |
| ts                      | true | long    | 时间戳         |      |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 只有在2021年1月30日0点后创建的订单，订单级别的真实收益（real_profit）字段才会有值。而成交级别的真实收益（real_profit）在2020年12月10日后就会有值。
 

## 【逐仓】获取合约当前未成交委托 

###  示例

- POST `/linear-swap-api/v1/swap_openorders`  

#### 备注
 - 该接口仅支持逐仓模式。

###  请求参数

| 参数名称       | 是否必须  | 类型     | 描述       | 取值范围           |
| ---------- | ----- | ------ | ---------- | -------------- |
| contract_code     | true  | string | 合约代码       |   "BTC-USDT" ...  |
| page_index | false | int    | 页码，不填默认第1页 |               |
| page_size  | false | int    |  页长，不填默认20，不得多于50          |    |
| sort_by  | false | string    |  排序字段，不填默认按创建时间倒序         | “created_at”(按照创建时间倒序)，“update_time”(按照更新时间倒序)   |
| trade_type  | false | int    |  交易类型，不填默认查询全部         | 0:全部,1:买入 开多,2: 卖出开空,3: 买入平空,4: 卖出平多。   |

> Response:

```json

{
    "status": "ok",
    "data": {
        "orders": [
            {
                "symbol": "BTC",
                "contract_code": "BTC-USDT",
                "volume": 1,
                "price": 13329,
                "order_price_type": "limit",
                "order_type": 1,
                "direction": "sell",
                "offset": "open",
                "lever_rate": 10,
                "order_id": 770326042832437248,
                "client_order_id": 57012021028,
                "created_at": 1603701640576,
                "trade_volume": 0,
                "trade_turnover": 0,
                "fee": 0,
                "trade_avg_price": null,
                "margin_frozen": 1.332900000000000000,
                "profit": 0,
                "status": 3,
                "order_source": "api",
                "order_id_str": "770326042832437248",
                "fee_asset": "USDT",
                "liquidation_type": null,
                "canceled_at": null,
                "margin_asset": "USDT",
                "margin_mode": "isolated",
                "margin_account": "BTC-USDT",
                "is_tpsl": 0,
                "update_time": 1606975980467,
                "real_profit": 0
            }
        ],
        "total_page": 2,
        "current_page": 1,
        "total_size": 2
    },
    "ts": 1603703993952
}
```

###  返回参数

参数名称  |   是否必须  |  类型   |  描述  |   取值范围  |
-------------------------- | -------------- | ---------- | --------------------------------------------------------------- | ------------------------------------------------------ |
status  |  true <img width=250/> |  string  |  请求处理结果 <img width=1000/>  | <img width=1100/>   |
\<data\>  |    |    |    |    |   
\<orders\>              |    |    |    |    |   
symbol  |  true  |  string  |  品种代码  |    |  
contract_code  |  true  |  string  |  合约代码  |  "BTC-USDT" ...  |
volume  |  true  |  decimal    |  委托数量  |    |
price   |  true  |  decimal    |  委托价格  |    |   
order_price_type  |    true  |  string  | 订单报价类型 |  "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单   |
order_type  |    true  |  int  |  订单类型 |  1:报单 、 2:撤单 、 3:强平、4:交割  |
direction  |  true  |  string  |  "buy":买 "sell":卖  |    |   
offset  |  true  |  string  |  "open":开 "close":平  |    |  
lever_rate  |  true  |  int  |   杠杆倍数  |    |
order_id  |  true  |  long  |  订单ID  |    |
order_id_str  |  true  |  string  |  订单ID，字符串类型  |    | 
client_order_id  |  true  |  long  |  客户订单ID  |    |
created_at  |  true  |  long  |  订单创建时间  |    |
trade_volume  |   true  |  decimal    |  成交数量  |    |  
trade_turnover  | true  |  decimal    |  成交总金额  |     | 
fee  |   true  |  decimal    |  手续费  |    |
fee_asset | true  | string | 手续费币种 | "BTC","ETH"... |
trade_avg_price  |  true |  decimal    |  成交均价  |    |  
margin_frozen  |  true  |  decimal    |  冻结保证金  |    | 
margin_asset   | true   | string | 保证金币种（计价币种）                 |                |
profit  |  true  |  decimal   | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）  |    |  
status  |  true  |  int  |   订单状态  |  (3未成交 4部分成交 5部分成交已撤单 6全部成交 7已撤单)  |  
order_source|   true  |  string  |  订单来源| （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发） |
liquidation_type|   true  |  string  | 强平类型	 |    |
canceled_at|   true  |  long  |  撤单时间 |    |
margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
is_tpsl | true | int | 是否设置止盈止损  | 1：是；0：否 |
update_time | true | Long | 订单更新时间，单位：毫秒  | |
real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
\</orders\>  |    |    |    |    |
total_page  |  true  |  int  |   总页数  |    |
current_page  |   true  |  int  |   当前页  |    |
total_size  |  true  |  int  |   总条数  |    |
\</data\>  |    |    |    |    |
ts  |    true  |  long  |  时间戳  |    |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 只有在2021年1月30日0点后创建的订单，真实收益（real_profit）字段才会有值。存量数据均为0。

## 【全仓】获取合约当前未成交委托

 - POST `/linear-swap-api/v1/swap_cross_openorders`

#### 备注
 - 该接口仅支持全仓模式。

###  请求参数

| 参数名称       | 是否必须  | 类型     | 描述       | 取值范围           |
| ---------- | ----- | ------ | ---------- | -------------- |
| contract_code     | true  | string | 合约代码       |   "BTC-USDT" ...  |
| page_index | false | int    | 页码，不填默认第1页 |               |
| page_size  | false | int    |  页长，不填默认20，不得多于50          |    |
| sort_by  | false | string    |  排序字段，不填默认按创建时间倒序         | “created_at”(按照创建时间倒序)，“update_time”(按照更新时间倒序)   |
| trade_type  | false | int    |  交易类型，不填默认查询全部         | 0:全部,1:买入 开多,2: 卖出开空,3: 买入平空,4: 卖出平多。   |


> Response

```json
{
    "status": "ok",
    "data": {
        "orders": [
            {
                "symbol": "ETH",
                "contract_code": "ETH-USDT",
                "volume": 1,
                "price": 80,
                "order_price_type": "limit",
                "order_type": 1,
                "direction": "sell",
                "offset": "open",
                "lever_rate": 30,
                "order_id": 784059619752280064,
                "client_order_id": null,
                "created_at": 1606975980467,
                "trade_volume": 0,
                "trade_turnover": 0,
                "fee": 0,
                "trade_avg_price": null,
                "margin_frozen": 0.026666666666666666,
                "profit": 0,
                "status": 3,
                "order_source": "api",
                "order_id_str": "784059619752280064",
                "fee_asset": "USDT",
                "liquidation_type": null,
                "canceled_at": null,
                "margin_asset": "USDT",
                "margin_account": "USDT",
                "margin_mode": "cross",
                "is_tpsl": 0,
                "update_time": 1606975980467,
                "real_profit": 0
            }
        ],
        "total_page": 1,
        "current_page": 1,
        "total_size": 2
    },
    "ts": 1606975988388
}
```

###  返回参数

| 参数名称                 | 是否必须 | 类型      | 描述                                       | 取值范围                                     |
| -------------------- | ---- | ------- | ---------------------------------------- | ---------------------------------------- |
| status               | true <img width=250/> | string  | 请求处理结果   <img width=1000/>      |                                          |
| \<data\> | true     |    object     |                   |                                          |
| symbol               | true | string  | 品种代码                                     |                                          |
| contract_code        | true | string  | 合约代码                                     | "BTC-USDT" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| volume               | true | decimal | 委托数量                                     |                                          |
| price                | true | decimal | 委托价格                                     |                                          |
| order_price_type     | true | string  | 订单报价类型 |   "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单  |
| order_type         | true | int  | 订单类型        |   1:报单 、 2:撤单 、 3:强平、4:交割      |
| direction            | true | string  |买卖方向   | "buy":买 "sell":卖                         |                                        
| offset               | true | string  | 开平方向   |  "open":开 "close":平                       |                                 
| lever_rate           | true | int     | 杠杆倍数                                     |                       |
| order_id             | true | long    | 订单ID    | |
| order_id_str             | true | string    | string格式的订单ID                                     |      |
| client_order_id      | true | long    | 客户订单ID                                   |                                          |
| order_source         | true | string  | 订单来源                                     | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发）  |
| created_at           | true | long    | 订单创建时间                                   |                                          |
| trade_volume         | true | decimal | 成交总数量                                     |                                          |
| trade_turnover       | true | decimal | 成交总金额，即sum（每一笔成交张数*合约面值*成交价格）                                    |                                          |
| fee                  | true | decimal | 手续费                                      |
| fee_asset         | true | string  | 手续费币种       |  （"USDT"...）      ||
| trade_avg_price      | true | decimal | 成交均价                                     |                                          |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_frozen        | true | decimal | 冻结保证金                                    |                                          |
| profit               | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）                                       |                                          |
| status               | true | int     | 订单状态                                     | (3未成交 4部分成交 5部分成交已撤单 6全部成交 7已撤单)         |
| liquidation_type              | true | string     | 强平类型    |      |
| canceled_at              | true | long     | 撤单时间        |        |
| is_tpsl              | true | int     | 是否设置止盈止损        |  1：是；0：否      |
| update_time | true | Long | 订单更新时间，单位：毫秒  | |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \</data\>            |      |         |                     |      |
| total_page           | true | int     | 总页数                                      |                                          |
| current_page         | true | int     | 当前页                                      |                                          |
| total_size           | true | int     | 总条数                                      |                                          |
| ts                   | true | long    | 时间戳                                      |                                          |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 只有在2021年1月30日0点后创建的订单，真实收益（real_profit）字段才会有值。存量数据均为0。

## 【逐仓】获取合约历史委托

- POST `/linear-swap-api/v1/swap_hisorders` 

#### 备注
 - 该接口仅支持逐仓模式。

###  请求参数

参数名称   |  是否必须   |  类型    |  描述  |  默认值    |  取值范围  |
-------------- | -------------- | ---------- |------------------------ | ------------ | ------------------------------------------------------------------------------------------------------ |
contract_code  |  true   |  string   |  合约代码   |  支持大小写,"BTC-USDT" ...  |
trade_type  |   true  |  int  |   交易类型  |    0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多,5: 卖出强平,6: 买入强平,7:交割平多,8: 交割平空, 11:减仓平多，12:减仓平空  |
type  |  true  |  int  |   类型  |  1:所有订单,2:结束状态的订单  |
status  |    true  |  string  |   订单状态  |  可查询多个状态，"3,4,5" , 0:全部,3:未成交, 4: 部分成交,5: 部分成交已撤单,6: 全部成交,7:已撤单 |
create_date |  true  |  int  |   日期  |   可随意输入正整数，如果参数超过90则默认查询90天的数据 |
page_index  |  false  |  int  |   |  页码，不填默认第1页  |  1  | 
page_size  |  false  |  int   |  每页条数，不填默认20  |  20  | 不得多于50  |
sort_by | false  | string | 排序字段（降序），不填默认按照create_date降序 | create_date |  "create_date"：按订单创建时间进行降序，"update_time"：按订单更新时间进行降序|
 
### 备注：

- 所有已撤销且无成交的API限价订单记录只保留最近2小时。

> Response:

```json

{
    "status": "ok",
    "data": {
        "orders": [
            {
                "order_id": 770336866451992576,
                "contract_code": "BTC-USDT",
                "symbol": "BTC",
                "lever_rate": 10,
                "direction": "sell",
                "offset": "close",
                "volume": 1.000000000000000000,
                "price": 13100.000000000000000000,
                "create_date": 1603704221118,
                "update_time": 1603704221118,
                "order_source": "web",
                "order_price_type": 6,
                "order_type": 1,
                "margin_frozen": 0,
                "profit": 0,
                "trade_volume": 0,
                "trade_turnover": 0,
                "fee": 0,
                "trade_avg_price": 0,
                "status": 3,
                "order_id_str": "770336866451992576",
                "fee_asset": "USDT",
                "liquidation_type": "0",
                "margin_asset": "USDT",
                "margin_mode": "isolated",
                "margin_account": "BTC-USDT",
                "is_tpsl": 0,
                "real_profit": 0
            }
        ],
        "total_page": 10,
        "current_page": 1,
        "total_size": 10
    },
    "ts": 1603704312847
}
```

###  返回参数

| 参数名称                   | 是否必须 | 类型      | 描述     | 取值范围                                     |
| ---------------------- | ---- | ------- | ------ | ---------------------------------------- |
| status     <img width=250/>    | true <img width=250/> | string <img width=250/>  | 请求处理结果 <img width=1000/> |   |
| \<data\> | true     |   object      |        |     |
| \<orders\> |  true    |  object array       |        |     |
| order_id               | true | long    | 订单ID   |       |
| order_id_str   | true | string    | string格式的订单ID    |      |
| symbol                 | true | string  | 品种代码   |   |
| contract_code          | true | string  | 合约代码   | "BTC-USDT" ... |
| lever_rate             | true | int     | 杠杆倍数   |    |
| direction              | true | string  | 买卖方向 | "buy":买 "sell":卖  |
| offset                 | true | string  | 开平方向   | "open":开 "close":平   |
| volume                 | true | decimal | 委托数量   |   |
| price                  | true | decimal | 委托价格   |    |
| create_date            | true | long    | 创建时间   |     |
| update_time            | true | long    | 订单更新时间，单位：毫秒	   |     |
| order_source           | true | string  | 订单来源   | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发） |
| order_price_type       | true | int  | 订单报价类型 | 	1：限价单（limit），2：市价单（market），3：对手价（opponent），4：闪电平仓（lightning），5：计划委托（trigger），6：post_only ，7：最优5档（optimal_5） ，8：最优10档（optimal_10） ，9：最优20档（optimal_20），10：FOK ，11：IOC ，12：对手价_IOC（opponent_ioc），13：闪电平仓_IOC（lightning_ioc），14：最优5档_IOC（optimal_5_ioc），15：最优10档_IOC（optimal_10_ioc），16：最优20档_IOC（optimal_20_ioc），17：对手价_FOK（opponent_fok），18：闪电平仓_FOK（lightning_fok），19：最优5档_FOK（optimal_5_fok），40：最优10档_FOK（optimal_10_fok），41：最优20档_FOK（optimal_20_fok）。    |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_frozen          | true | decimal | 冻结保证金  |   |
| profit                 | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）     |    |
| trade_volume           | true | decimal | 成交数量   |     |
| trade_turnover         | true | decimal | 成交总金额，即sum（每一笔成交张数*合约面值*成交价格）  |         |
| fee                    | true | decimal | 手续费    |      |
| trade_avg_price        | true | decimal | 成交均价   |    |
| status                 | true | int     | 订单状态   |     |
| order_type             | true | int     | 订单类型   | 1:报单 、 2:撤单 、 3:强平、4:交割                  |
| fee_asset         | true | string  | 手续费币种       |  （"USDT"...）      |
| liquidation_type              | true | string     | 强平类型        |  0:非强平类型，1：多空轧差， 2:部分接管，3：全部接管 |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| is_tpsl | true | int | 是否设置止盈止损  | 1：是；0：否 |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \</orders\>     |      |         |        |                          |
| current_page           | true | int     | 当前页    |      |
| total_page             | true | int     | 总页数    |    |
| total_size             | true | int     | 总条数    |     |
| \</data\>            |      |         |        |      |
| ts                     | true | long    | 时间戳    |      |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 只有在2021年1月30日0点后创建的订单，真实收益（real_profit）字段才会有值。存量数据均为0。

## 【全仓】获取合约历史委托

 - POST `/linear-swap-api/v1/swap_cross_hisorders`

#### 备注
 - 该接口仅支持全仓模式。

###  请求参数

| 参数名称        | 是否必须  | 类型     | 描述              | 取值范围   |
| ----------- | ----- | ----------- | ---------------------------------------- | ------ |
| contract_code      | true  | string | 合约代码        |  "BTC-USDT" ...                          |
| trade_type  | true  | int    | 交易类型        | 0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多,5: 卖出强平,6: 买入强平,7:交割平多,8: 交割平空, 11:减仓平多，12:减仓平空 |        |
| type        | true  | int    | 类型          | 1:所有订单,2:结束状态的订单                         |
| status      | true  | string    | 订单状态        | 可查询多个状态，"3,4,5" , 0:全部,3:未成交, 4: 部分成交,5: 部分成交已撤单,6: 全部成交,7:已撤单 |
| create_date | true  | int    | 日期，可随意输入正整数，如果参数超过90则默认查询90天的数据          |                          |
| page_index  | false | int    |   页码，不填默认第1页           |                               |
| page_size   | false | int    | 每页条数，不填默认20       | 不得多于50 |
| sort_by | false  | string | 排序字段（降序），不填默认按照create_date降序 |  "create_date"：按订单创建时间进行降序，"update_time"：按订单更新时间进行降序|

###备注：
 所有已撤销且无成交的API限价订单记录只保留最近2小时。

> Response

```json
{
    "status": "ok",
    "data": {
        "orders": [
            {
                "order_id": 784059619752280064,
                "contract_code": "ETH-USDT",
                "symbol": "ETH",
                "lever_rate": 30,
                "direction": "sell",
                "offset": "open",
                "volume": 1,
                "price": 80,
                "create_date": 1606975980467,
                "update_time": 1606975980467,
                "order_source": "api",
                "order_price_type": 1,
                "order_type": 1,
                "margin_frozen": 0.026666666666666666,
                "profit": 0,
                "trade_volume": 0,
                "trade_turnover": 0,
                "fee": 0,
                "trade_avg_price": 0,
                "status": 3,
                "order_id_str": "784059619752280064",
                "fee_asset": "USDT",
                "liquidation_type": "0",
                "margin_asset": "USDT",
                "margin_mode": "cross",
                "margin_account": "USDT",
                "is_tpsl": 0,
                "real_profit": 0
            }
        ],
        "total_page": 6,
        "current_page": 1,
        "total_size": 12
    },
    "ts": 1606976252777
}
```

###  返回参数

| 参数名称                   | 是否必须 | 类型      | 描述     | 取值范围                                     |
| ---------------------- | ---- | ------- | ------ | ---------------------------------------- |
| status                 | true <img width=250/> | string <img width=250/>  | 请求处理结果 <img width=1000/> |   |
| \<data\> | true     |   object      |        |     |
| \<orders\> |  true    |  object array       |        |     |
| order_id               | true | long    | 订单ID   |       |
| order_id_str   | true | string    | string格式的订单ID    |      |
| symbol                 | true | string  | 品种代码   |   |
| contract_code          | true | string  | 合约代码   | "BTC-USDT" ... |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| lever_rate             | true | int     | 杠杆倍数   |    |
| direction              | true | string  | 买卖方向 | "buy":买 "sell":卖  |
| offset                 | true | string  | 开平方向   | "open":开 "close":平   |
| volume                 | true | decimal | 委托数量   |   |
| price                  | true | decimal | 委托价格   |    |
| create_date            | true | long    | 创建时间   |     |
| update_time            | true | long    | 订单更新时间，单位：毫秒   |     |
| order_source           | true | string  | 订单来源   | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发）   |
| order_price_type       | true | int  | 订单报价类型 | 1：限价单（limit），2：市价单（market），3：对手价（opponent），4：闪电平仓（lightning），5：计划委托（trigger），6：post_only ，7：最优5档（optimal_5） ，8：最优10档（optimal_10） ，9：最优20档（optimal_20），10：FOK ，11：IOC ，12：对手价_IOC（opponent_ioc），13：闪电平仓_IOC（lightning_ioc），14：最优5档_IOC（optimal_5_ioc），15：最优10档_IOC（optimal_10_ioc），16：最优20档_IOC（optimal_20_ioc），17：对手价_FOK（opponent_fok），18：闪电平仓_FOK（lightning_fok），19：最优5档_FOK（optimal_5_fok），40：最优10档_FOK（optimal_10_fok），41：最优20档_FOK（optimal_20_fok）。       |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_frozen          | true | decimal | 冻结保证金  |   |
| profit                 | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）     |    |
| trade_volume           | true | decimal | 成交数量   |     |
| trade_turnover         | true | decimal | 成交总金额，即sum（每一笔成交张数*合约面值*成交价格）  |         |
| fee                    | true | decimal | 手续费    |      |
| trade_avg_price        | true | decimal | 成交均价   |    |
| status                 | true | int     | 订单状态   |     |
| order_type             | true | int     | 订单类型   | 1:报单 、 2:撤单 、 3:强平、4:交割                  |
| fee_asset         | true | string  | 手续费币种       |  （"USDT"...）      |
| liquidation_type              | true | string     | 强平类型        |  0:非强平类型，1：多空轧差， 2:部分接管，3：全部接管 |
| is_tpls              | true | int     | 是否设置止盈止损        |  1：是；0：否 |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \</orders\>     |      |         |        |                          |
| current_page           | true | int     | 当前页    |      |
| total_page             | true | int     | 总页数    |    |
| total_size             | true | int     | 总条数    |     |
| \</data\>            |      |         |        |      |
| ts                     | true | long    | 时间戳    |      |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 只有在2021年1月30日0点后创建的订单，真实收益（real_profit）字段才会有值。存量数据均为0。

## 【逐仓】获取历史成交记录

- POST `/linear-swap-api/v1/swap_matchresults`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code        | true  | string | 合约代码          | "BTC-USDT"...                           |
| trade_type    | true  | int    | 交易类型        | 0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多,5: 卖出强平,6: 买入强平 |
| create_date   | true  | int    | 日期        | 可随意输入正整数，如果参数超过90则默认查询90天的数据    |
| page_index    | false | int    | 页码，不填默认第1页     |                                          |
| page_size     | false | int    | 不填默认20，不得多于50    |                                          |

> Response: 

```json

{
    "status": "ok",
    "data": {
        "trades": [
            {
                "match_id": 131560927,
                "order_id": 770334322963152896,
                "symbol": "BTC",
                "contract_code": "BTC-USDT",
                "direction": "sell",
                "offset": "open",
                "trade_volume": 1.000000000000000000,
                "trade_price": 13059.800000000000000000,
                "trade_turnover": 13.059800000000000000,
                "trade_fee": -0.005223920000000000,
                "offset_profitloss": 0,
                "create_date": 1603703614715,
                "role": "Taker",
                "order_source": "api",
                "order_id_str": "770334322963152896",
                "id": "131560927-770334322963152896-1",
                "fee_asset": "USDT",
                "margin_mode": "isolated",
                "margin_account": "BTC-USDT",
                "real_profit": 0
            }
        ],
        "total_page": 2,
        "current_page": 1,
        "total_size": 2
    },
    "ts": 1603704407235
}            
                               
```

### 返回参数

| 参数名称                   | 是否必须 | 类型      | 描述                 | 取值范围                                     |
| ---------------------- | ---- | ------- | ------------------ | ---------------------------------------- |
| status                 | true <img width=250/> | string  | 请求处理结果             | <img width=1000/>  |
| \<data\> | true     |  object       |                    |     |
| \<trades\> | true     |  object array       |                    |    |
| id               | true | string    | 全局唯一的交易标识       |   |
| match_id               | true | long    | 撮合结果id, 与订单ws推送orders.$contract_code推送结果中的trade_id是相同的，非唯一，可重复，注意：一个撮合结果代表一个taker单和N个maker单的成交记录的集合，如果一个taker单吃了N个maker单，那这N笔trade都是一样的撮合结果   |   |
| order_id               | true | long    | 订单ID               |   |
| order_id_str      | true | string    | string格式的订单ID   |       |
| symbol                 | true | string  | 品种代码               | |
| order_source           | true | string  | 订单来源   | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发）  |
| contract_code          | true | string  | 合约代码               | "BTC-USDT" ...                          |
| direction              | true | string  | 买卖方向  |       "buy":买 "sell":卖                                   |
| offset                 | true | string  | 开平方向 |    "open":开 "close":平          |
| trade_volume           | true | decimal | 成交数量               |     |
| trade_price            | true | decimal | 成交价格               |  |
| trade_turnover         | true | decimal | 成交金额（成交数量*合约面值*成交价格）       |       |
| create_date            | true | long    | 成交时间               |  |
| offset_profitloss      | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）   |    |
| trade_fee             | true | decimal | 成交手续费              |    |
| role                   | true | string  | taker或maker        |    |
| fee_asset         | true | string  | 手续费币种   | （"USDT"...）  |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \</trades\>              |      |         |                    |   |
| current_page           | true | int     | 当前页                |  |
| total_page             | true | int     | 总页数                |    |
| total_size             | true | int     | 总条数                |      |
| \</data\>           |      |         |                    |     |
| ts                     | true | long    | 时间戳                |    |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 真实收益（real_profit）字段在2020年12月10日后才有值。该时间点之前的存量数据均为0。

## 【全仓】获取历史成交记录

 - POST `/linear-swap-api/v1/swap_cross_matchresults`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code        | true  | string | 合约代码          | "BTC-USDT"...                           |
| trade_type    | true  | int    | 交易类型        | 0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多,5: 卖出强平,6: 买入强平 |
| create_date   | true  | int    | 日期        | 可随意输入正整数，如果参数超过90则默认查询90天的数据    |
| page_index    | false | int    | 页码，不填默认第1页     |                                          |
| page_size     | false | int    | 不填默认20，不得多于50    |                                          |

> Response

```json

{
    "status": "ok",
    "data": {
        "trades": [
            {
                "match_id": 33161,
                "order_id": 784059498905993216,
                "symbol": "ETH",
                "contract_code": "ETH-USDT",
                "direction": "sell",
                "offset": "open",
                "trade_volume": 1,
                "trade_price": 50,
                "trade_turnover": 0.5,
                "trade_fee": -0.0002,
                "offset_profitloss": 0,
                "create_date": 1606975951808,
                "role": "Taker",
                "order_source": "api",
                "order_id_str": "784059498905993216",
                "id": "33161-784059498905993216-1",
                "fee_asset": "USDT",
                "margin_mode": "cross",
                "margin_account": "USDT",
                "real_profit": 0
            }
        ],
        "total_page": 6,
        "current_page": 1,
        "total_size": 6
    },
    "ts": 1606976521624
}
```

### 返回参数

| 参数名称                   | 是否必须 | 类型      | 描述                 | 取值范围                                     |
| ---------------------- | ---- | ------- | ------------------ | ---------------------------------------- |
| status                 | true <img width=250/> | string  | 请求处理结果    |   <img width=1000/>  |
| \<data\> | true     |  object       |                    |     |
| \<trades\> | true     |  object array       |                    |    |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| id               | true | string    | 全局唯一的交易标识      |   |
| match_id               | true | long    | 撮合结果id, 与订单ws推送orders_cross.$contract_code推送结果中的trade_id是相同的，非唯一，可重复，注意：一个撮合结果代表一个taker单和N个maker单的成交记录的集合，如果一个taker单吃了N个maker单，那这N笔trade都是一样的撮合结果   |   |
| order_id               | true | long    | 订单ID               |   |
| order_id_str      | true | string    | string格式的订单ID   |       |
| symbol                 | true | string  | 品种代码               | |
| order_source           | true | string  | 订单来源   |  （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发） |
| contract_code          | true | string  | 合约代码               | "BTC-USDT" ...                          |
| direction              | true | string  |  买卖方向  |       "buy":买 "sell":卖                                   |
| offset                 | true | string  | 开平方向 |    "open":开 "close":平          |
| trade_volume           | true | decimal | 成交数量               |     |
| trade_price            | true | decimal | 成交价格               |  |
| trade_turnover         | true | decimal | 成交金额（成交数量*合约面值*成交价格）       |       |
| create_date            | true | long    | 成交时间               |  |
| offset_profitloss      | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）    |    |
| trade_fee             | true | decimal | 成交手续费              |    |
| role                   | true | string  | taker或maker        |    |
| fee_asset         | true | string  | 手续费币种   | （"USDT"...）  |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \</trades\>              |      |         |                    |   |
| current_page           | true | int     | 当前页                |  |
| total_page             | true | int     | 总页数                |    |
| total_size             | true | int     | 总条数                |      |
| \</data\>            |      |         |                    |     |
| ts                     | true | long    | 时间戳                |    |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 真实收益（real_profit）字段在2020年12月10日后才有值。该时间点之前的存量数据均为0。

## 【逐仓】闪电平仓下单

- POST `/linear-swap-api/v1/swap_lightning_close_position`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述                    | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- | ---------------------------------------- |
| contract_code          | true | string | 合约代码                  | "BTC-USDT"...                           |
| volume          | true  | long | 委托数量（张）               |                                          |
| direction       | true  | string | 买卖方向      |        “buy”:买，“sell”:卖       |
| client_order_id | false | long | （API）客户自己填写和维护，必须保持唯一,请注意必须小于等于9223372036854775807 | |
| order_price_type | false | string | 订单报价类型 |不填，默认为“闪电平仓”，"lightning"：闪电平仓，"lightning_ioc"：闪电平仓-IOC，"lightning_fok"：闪电平仓-FOK |

#### 备注
 - 闪电平仓，是指在对手价平仓的基础上，实行'最优30档'成交，即用户发出的平仓订单能够迅速以30档范围内对手方价格进行成交，未成交部分自动转为限价委托单。

 - client_order_id，24小时有效，超过24小时的订单根据client_order_id将查询不到。

> Response:

```json

{
  "status": "ok",
  "data": {
    "order_id": 9861634,
    "order_id_str": "9861634",
    "client_order_id": 9086
  },
  "ts": 158797866555
}

```


### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |                      |
| \<data\>        |   true    |   object     |                               | 字典                   |
| order_id        | true  | long | 订单ID[全局唯一] |                      |
| order_id_str        | true  | string | String类型订单ID |                      |
| client_order_id | false | Long | 用户自己的订单id                     |                      |
| \</data\>       |       |        |     |  |


> 错误信息：

```json

{
    "status": "error",
    "err_code": 1048,
    "err_msg": "Insufficient close amount available.",
    "ts": 1603704587846
}

```

## 【全仓】闪电平仓下单

 - POST `/linear-swap-api/v1/swap_cross_lightning_close_position`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述                    | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- | ---------------------------------------- |
| contract_code          | true | String | 合约代码                  | "BTC-USDT"...                           |
| volume          | true  | decimal | 委托数量（张）               |                                          |
| direction       | true  | String | 买卖方向      |        “buy”:买，“sell”:卖       |
| client_order_id | false | long | （API）客户自己填写和维护，必须保持唯一,请注意必须小于等于9223372036854775807 | |
| order_price_type | false | string | 订单报价类型 |不填，默认为“闪电平仓”，"lightning"：闪电平仓，"lightning_ioc"：闪电平仓-IOC，"lightning_fok"：闪电平仓-FOK |

#### 备注
 - 闪电平仓，是指在对手价平仓的基础上，实行'最优30档'成交，即用户发出的平仓订单能够迅速以30档范围内对手方价格进行成交，未成交部分自动转为限价委托单。

 - client_order_id，24小时有效，超过24小时的订单根据client_order_id将查询不到。

> Response

```json

{
    "status": "ok",
    "data": {
        "order_id": 784063527799226368,
        "order_id_str": "784063527799226368"
    },
    "ts": 1606976912267
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |                      |
| \<data\>        |   true    |   object     |                               | 字典                   |
| order_id        | true  | long | 订单ID[全局唯一] |                      |
| order_id_str        | true  | string | String类型订单ID |                      |
| client_order_id | false | int | 用户自己的订单id                     |                      |
| \</data\>       |       |        |     |  |


# 合约策略订单接口

## 【逐仓】合约计划委托下单

- POST `/linear-swap-api/v1/swap_trigger_order`

#### 备注
 - 该接口仅支持逐仓模式。

> 请求示例

```json

{
    "contract_code": "BTC-USDT",
    "trigger_type": "ge",
    "trigger_price": 1111,
    "order_price": 1000,
    "order_price_type":"limit",
    "volume": 111,
    "direction": "buy",
    "offset": "open",
    "lever_rate": 10
}
```

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述                    | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码 |BTC-USDT <img width=1000/> |
| trigger_type | true | string | 触发类型： ge大于等于(触发价比最新价大)；le小于(触发价比最新价小) |  |
| trigger_price | true | decimal | 触发价，精度超过最小变动单位会报错 |  |
| order_price | false | decimal | 委托价，精度超过最小变动单位会报错 |  |
| order_price_type | false | string | 委托类型： 不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20 |  |
| volume | true | long | 委托数量(张) |  |
| direction | true | string | buy:买 sell:卖 |  |
| offset | true | string | open:开 close:平 |  |
| lever_rate | false | int | 开仓必须填写，平仓可以不填。杠杆倍数[开仓若有10倍多单，就不能再下20倍多单;首次使用高倍杠杆(>20倍)，请使用主账号登录web端同意高倍杠杆协议后，才能使用接口下高倍杠杆(>20倍)] |  |

#### 备注：

- optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档下单order_price价格参数不用传，"limit":限价需要传价格。

- 若存在持仓，那么下单时杠杆倍数必须与持仓杠杆相同，否则下单失败。若需使用新杠杆下单，则必须先使用切换杠杆接口将持仓杠杆切换成功后再下单。

> Response:

```json

{
    "status": "ok",
    "data": {
        "order_id": 35,
        "order_id_str": "35"
    },
    "ts": 1547521135713
}

```


### 返回参数

| 参数名称              | 是否必须 | 类型 | 描述                  | 取值范围   |
| -------------------------- | ------------ | -------- | -------------------------- | -------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| ts |  true  | long | 时间戳 | |
| \<data\> |  true  | object | 成功处理返回的数据  | |
| order_id  |  true  | int | 订单ID : 全局唯一  | |
| order_id_str |  true  | string | 字符串类型的订单ID   | |
| \</data\> |   | |  | |


> 错误示例：

```json

{
    "status": "error",
    "err_code": 1014,
    "err_msg": "This contract doesnt exist.",
    "ts": 1603704820880
}

```

## 【全仓】合约计划委托下单

 - POST `/linear-swap-api/v1/swap_cross_trigger_order`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述                    | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- | ---------------------------------------- |
| contract_code | true | String | 合约代码 |BTC-USDT  <img width=1000/> |
| trigger_type | true | String | 触发类型： ge大于等于(触发价比最新价大)；le小于(触发价比最新价小) |  |
| trigger_price | true | decimal | 触发价，精度超过最小变动单位会报错 |  |
| order_price | false | decimal | 委托价，精度超过最小变动单位会报错 |  |
| order_price_type | false | string | 委托类型： 不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20 |  |
| volume | true | decimal | 委托数量(张) |  |
| direction | true | String | buy:买 sell:卖 |  |
| offset | true | String | open:开 close:平 |  |
| lever_rate | false | int | 开仓必须填写，平仓可以不填。杠杆倍数[开仓若有10倍多单，就不能再下20倍多单;首次使用高倍杠杆(>20倍)，请使用主账号登录web端同意高倍杠杆协议后，才能使用接口下高倍杠杆(>20倍)] |  |

> Response

```json

正确的返回：
{
    "status": "ok",
    "data": {
        "order_id": 1880,
        "order_id_str": "1880"
    },
    "ts": 1606977456766
}

错误的返回：
{
    "status": "error",
    "err_code": 1085,
    "err_msg": "Trigger order failed, please modify the price and place the order again or contact the customer service.",
    "ts": 1606977396756
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| ts |  true  | long | 时间戳 | |
| \<data\> |  true  | object | 成功处理返回的数据  | |
| order_id  |  true  | int | 订单ID : 全局唯一  | |
| order_id_str |  true  | string | 字符串类型的订单ID   | |
| \</data\> |   | |  | |

## 【逐仓】合约计划委托撤单

- POST `/linear-swap-api/v1/swap_trigger_cancel`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| contract_code | true | string | 合约代码 |BTC-USDT |
| order_id | true | string | 用户订单ID（多个订单ID中间以","分隔,一次最多允许撤消20个订单 ） |  |


> Response:

```json

{
    "status": "ok",
    "data": {
        "errors": [
            {
                "order_id": "34",
                "err_code": 1061,
                "err_msg": "This order doesnt exist."
            }
        ],
        "successes": "1"
    },
    "ts": 1603704887184
}

```


### 返回参数

| 参数名称              | 是否必须 | 类型 | 描述                  | 取值范围   |
| -------------------------- | ------------ | -------- | -------------------------- | -------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| \<data\> |  true  | object | 成功处理返回的数据  | |
| \<errors\>|   true          |    object array      |     订单失败信息                       |                |
| order_id                   | false         | string   | 订单id                     |                |
| err_code                   | false         | int      | 订单失败错误码             |                |
| err_msg                    | false         | string      | 订单失败信息               |                |
| \</errors\>                  |              |          |                            |                |
| successes                  | true        | string   | 成功的订单，多个订单号以“,”相连                 |                |
| \</data\> |   | |  | |
| ts                         | true         | long     | 响应生成时间点，单位：毫秒 |  |

## 【全仓】合约计划委托撤单

 - POST `/linear-swap-api/v1/swap_cross_trigger_cancel`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述                    | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- | ---------------------------------------- |
| contract_code | true | String | 合约代码 |BTC-USDT |
| order_id | true | String | 用户订单ID（多个订单ID中间以","分隔,一次最多允许撤消10个订单 ） |  |

> Response

```json
{
    "status": "ok",
    "data": {
        "errors": [
            {
                "order_id": "1888",
                "err_code": 1061,
                "err_msg": "This order doesnt exist."
            }
        ],
        "successes": "1880"
    },
    "ts": 1606977508308
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| \<data\> |  true  | object | 成功处理返回的数据  | |
| \<errors\>|   true          |    object array      |     订单失败信息                       |                |
| order_id                   | false         | string   | 订单id                     |                |
| err_code                   | false         | int      | 订单失败错误码             |                |
| err_msg                    | false         | string      | 订单失败信息               |                |
| \</errors\>                  |              |          |                            |                |
| successes                  | true        | string   | 成功的订单，多个订单号以“,”相连                 |                |
| \</data\> |   | |  | |
| ts                         | true         | long     | 响应生成时间点，单位：毫秒 |  |

## 【逐仓】合约计划委托全部撤单

- POST `/linear-swap-api/v1/swap_trigger_cancelall`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述                    | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码 |BTC-USDT |
| direction | false  | string | 买卖方向（不填默认全部）  |  "buy":买 "sell":卖 |
| offset | false  | string | 开平方向（不填默认全部）  | "open":开 "close":平  |

#### 备注：
 - direction与offset可只填其一，只填其一则按对应的条件去撤单。（如用户只传了direction=buy，则撤销所有买单，包括开仓和平仓）

> Response:

```json

{
    "status": "ok",
    "data": {
        "errors": [],
        "successes": "2"
    },
    "ts": 1603704998960
}

```

### 返回参数

| 参数名称              | 是否必须 | 类型 | 描述                  | 取值范围   |
| -------------------------- | ------------ | -------- | -------------------------- | -------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| \<data\> |  true  | object | 成功处理返回的数据  | |
| \<errors\>|   true          |    object array      |     订单失败信息                       |                |
| order_id                   | false         | string   | 订单id                     |                |
| err_code                   | false         | int      | 订单失败错误码             |                |
| err_msg                    | false         | string      | 订单失败信息               |                |
| \</errors\>                  |              |          |                            |                |
| successes                  | true        | string   | 成功的订单，多个订单号以“,”相连                 |                |
| \</data\> |   | |  | |
| ts                         | true         | long     | 响应生成时间点，单位：毫秒 |  |

> 错误示例：

```json

{
    "status": "error",
    "err_code": 1051,
    "err_msg": "No orders to cancel.",
    "ts": 1603705063592
}

```

## 【全仓】合约计划委托全部撤单

 - POST `/linear-swap-api/v1/swap_cross_trigger_cancelall`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述                    | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- | ---------------------------------------- |
| contract_code | true | String | 合约代码 |BTC-USDT |
| direction | false  | string | 买卖方向（不填默认全部）  |  "buy":买 "sell":卖 |
| offset | false  | string | 开平方向（不填默认全部）  | "open":开 "close":平  |

#### 备注：
 - direction与offset可只填其一，只填其一则按对应的条件去撤单。（如用户只传了direction=buy，则撤销所有买单，包括开仓和平仓）

> Response

```json
{
    "status": "ok",
    "data": {
        "errors": [],
        "successes": "1879,1878"
    },
    "ts": 1606977712328
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| \<data\> |  true  | object | 成功处理返回的数据  | |
| \<errors\>|   true          |    object array      |     订单失败信息                       |                |
| order_id                   | false         | string   | 订单id                     |                |
| err_code                   | false         | int      | 订单失败错误码             |                |
| err_msg                    | false         | string      | 订单失败信息               |                |
| \</errors\>                  |              |          |                            |                |
| successes                  | true        | string   | 成功的订单，多个订单号以“,”相连                 |                |
| \</data\> |   | |  | |
| ts                         | true         | long     | 响应生成时间点，单位：毫秒 |  |

## 【逐仓】获取计划委托当前委托

- POST `/linear-swap-api/v1/swap_trigger_openorders`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| contract_code | true | string | 合约代码 |BTC-USDT |
| page_index | false | int | 第几页，不填默认第一页 | |
| page_size | false | int | 不填默认20，不得多于50 | |
| trade_type  | false | int    |  交易类型，不填默认查询全部         | 0:全部,1:买入 开多,2: 卖出开空,3: 买入平空,4: 卖出平多。   |

> Response:

```json

{
    "status": "ok",
    "data": {
        "orders": [
            {
                "symbol": "BTC",
                "contract_code": "BTC-USDT",
                "trigger_type": "ge",
                "volume": 1.000000000000000000,
                "order_type": 1,
                "direction": "sell",
                "offset": "open",
                "lever_rate": 10,
                "order_id": 4,
                "order_id_str": "4",
                "order_source": "api",
                "trigger_price": 13900.000000000000000000,
                "order_price": 13900.000000000000000000,
                "created_at": 1603705215654,
                "order_price_type": "limit",
                "status": 2,
                "margin_mode": "isolated",
                "margin_account": "BTC-USDT"
            }
        ],
        "total_page": 1,
        "current_page": 1,
        "total_size": 1
    },
    "ts": 1603705219567
}

```


### 返回参数

| 参数名称              | 是否必须 | 类型 | 描述                  | 取值范围   |
| -------------------------- | ------------ | -------- | -------------------------- | -------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| \<data\> |  true  | object | 成功处理返回的数据  | |
| total_page |true | int |  总页数 | |
| current_page | true |int |  当前页 | |
| total_size | true |int |  总条数 | |
| \<orders\>|   true          |    object array      |     订单信息                       |                |
| symbol |true |string |合约品种 | |
| contract_code |true | string  | 合约代码 | |
| trigger_type | true |string  | 触发类型  | `ge`大于等于；`le`小于等于 |
| volume | true |decimal  | 委托数量 | |
| order_type | true |int  | 订单类型  |  1、报单  2、撤单 |
| direction | true |string  | 订单方向  | [买(buy),卖(sell)] |
| offset | true |string  | 开平标志 |  [开(open),平(close)] |
| lever_rate | true |int | 杠杆倍数  | |
| order_id | true |long  | 计划委托单订单ID | |
| order_id_str | true |string  | 字符串类型的订单ID  | |
| order_source | true |string | 来源  |（system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发） |
| trigger_price | true |decimal |  触发价 | |
| order_price | true |decimal | 委托价 | |
| created_at | true |long | 订单创建时间 | |
| order_price_type | true |string | 订单报价类型 |  限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20 |
| status | true |int | 订单状态  | 1:准备提交、2:已提交、3:报单中、8：撤单未找到、9：撤单中、10：失败' |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| \</orders\>                  |              |          |                            |                |
| \</data\> |   | |  | |
| ts                         | true         | long     | 响应生成时间点，单位：毫秒 |  |

## 【全仓】获取计划委托当前委托

 - POST `/linear-swap-api/v1/swap_cross_trigger_openorders`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述                    | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- | ---------------------------------------- |
| contract_code | true | String | 合约代码 |BTC-USDT |
| page_index | false | int | 第几页，不填默认第一页 | |
| page_size | false | int | 不填默认20，不得多于50 | |
| trade_type  | false | int    |  交易类型，不填默认查询全部         | 0:全部,1:买入 开多,2: 卖出开空,3: 买入平空,4: 卖出平多。   |

> Response

```json
{
    "status": "ok",
    "data": {
        "orders": [
            {
                "symbol": "ETH",
                "contract_code": "ETH-USDT",
                "trigger_type": "ge",
                "volume": 1,
                "order_type": 1,
                "direction": "sell",
                "offset": "open",
                "lever_rate": 30,
                "order_id": 1881,
                "order_id_str": "1881",
                "order_source": "api",
                "trigger_price": 90,
                "order_price": 90,
                "created_at": 1606978152937,
                "order_price_type": "limit",
                "status": 2,
                "margin_mode": "cross",
                "margin_account": "USDT"
            }
        ],
        "total_page": 1,
        "current_page": 1,
        "total_size": 1
    },
    "ts": 1606978195074
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| \<data\> |  true  | object | 成功处理返回的数据  | |
| total_page |true | int |  总页数 | |
| current_page | true |int |  当前页 | |
| total_size | true |int |  总条数 | |
| \<orders\>|   true          |    object array      |     订单信息                       |                |
| symbol |true |string |合约品种 | |
| contract_code |true | string  | 合约代码 | |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| trigger_type | true |string  | 触发类型   | `ge`大于等于；`le`小于等于 |
| volume | true |decimal  | 委托数量 | |
| order_type | true |int  | 订单类型  |1、报单  2、撤单 |
| direction | true |string  | 订单方向  |[买(buy),卖(sell)] |
| offset | true |string  | 开平标志  | [开(open),平(close)] |
| lever_rate | true |int | 杠杆倍数  | |
| order_id | true |long  | 计划委托单订单ID | |
| order_id_str | true |string  | 字符串类型的订单ID  | |
| order_source | true |string | 来源 |（system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发） |
| trigger_price | true |decimal |  触发价 | |
| order_price | true |decimal | 委托价 | |
| created_at | true |long | 订单创建时间 | |
| order_price_type | true |string | 订单报价类型 |  限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20 |
| status | true |int | 订单状态 |  1:准备提交、2:已提交、3:报单中、8：撤单未找到、9：撤单中、10：失败' |
| \</orders\>                  |              |          |                            |                |
| \</data\> |   | |  | |
| ts                         | true         | long     | 响应生成时间点，单位：毫秒 |  |

## 【逐仓】获取计划委托历史委托

- POST `/linear-swap-api/v1/swap_trigger_hisorders`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| **参数名称**  | **是否必须** | **类型** | **描述**               | **默认值** | **取值范围**|
| ------- | ------- | ------- | -------- | ------- | -------- |
| contract_code | true        | string   | 合约代码 |   | BTC-USDT |
| trade_type        | true         | int      | 交易类型               |            | 0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多；后台是根据该值转换为offset和direction，然后去查询的； 其他值无法查询出结果 |
| status        | true         | string      | 订单状态               |            | 多个以英文逗号隔开，计划委托单状态：0:全部（表示全部结束状态的订单）、4:已委托、5:委托失败、6:已撤单 |
| create_date   | true         | int      | 日期                   |            | 可随意输入正整数，如果参数超过90则默认查询90天的数据      |
| page_index    | false        | int      | 页码，不填默认第1页    | 1          | 第几页，不填默认第一页 |
| page_size     | false        | int      | 不填默认20，不得多于50 | 20         | 不填默认20，不得多于50 |
| sort_by | false  | string | 排序字段（降序），不填默认按照created_at降序 | created_at  | "created_at"：按订单创建时间进行降序，"update_time"：按订单更新时间进行降序|

#### 备注：

- 默认查询 已完成订单（status对应状态范围 4、5、6）；

> Response:

```json

{
    "status": "ok",
    "data": {
        "orders": [
            {
                "symbol": "BTC",
                "contract_code": "BTC-USDT",
                "trigger_type": "ge",
                "volume": 1.000000000000000000,
                "order_type": 1,
                "direction": "sell",
                "offset": "open",
                "lever_rate": 10,
                "order_id": 3,
                "order_id_str": "3",
                "relation_order_id": "-1",
                "order_price_type": "limit",
                "status": 6,
                "order_source": "api",
                "trigger_price": 13900.000000000000000000,
                "triggered_price": null,
                "order_price": 13900.000000000000000000,
                "created_at": 1603705155231,
                "triggered_at": null,
                "order_insert_at": 0,
                "canceled_at": 1603705159520,
                "update_time": 1603705159520,
                "fail_code": null,
                "fail_reason": null,
                "margin_mode": "isolated",
                "margin_account": "BTC-USDT"
            }
        ],
        "total_page": 3,
        "current_page": 1,
        "total_size": 3
    },
    "ts": 1603705603369
}

```


### 返回参数

| 参数名称              | 是否必须 | 类型 | 描述                  | 取值范围   |
| -------------------------- | ------------ | -------- | -------------------------- | -------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| \<data\> |  true  | object | 成功处理返回的数据  | |
| total_page |true | int |  总页数 | |
| current_page | true |int |  当前页 | |
| total_size | true |int |  总条数 | |
| \<orders\>|   true          |    object array      |     订单信息                       |                |
| symbol |true |string |合约品种 | |
| contract_code |true | string  | 合约代码 | |
| trigger_type | true |string  | 触发类型   |`ge`大于等于；`le`小于等于 |
| volume | true |decimal  | 委托数量 | |
| order_type | true |int  | 订单类型  | 1、报单  2、撤单 |
| direction | true |string  | 订单方向  | [买(buy),卖(sell)] |
| offset | true |string  | 开平标志  | [开(open),平(close)] |
| lever_rate | true |int | 杠杆倍数  | |
| order_id | true |long  | 计划委托单订单ID | |
| order_id_str | true |string  | 字符串类型的订单ID  | |
| relation_order_id | true | string  | 该字段为关联限价单的订单id，未触发前数值为-1 | |
| order_price_type | true |string | 订单报价类型 |  限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20 |
| status | true |int  | 订单状态 | (4:报单成功、5:报单失败、6:已撤单 ) |
| order_source | true |string | 来源 | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发） |
| trigger_price | true |decimal | 触发价| |
| triggered_price | true |decimal  | 被触发时的价格| |
| order_price | true |decimal  | 委托价| |
| created_at | true |long  | 订单创建时间| |
| update_time | true |long  | 订单更新时间，单位：毫秒	| |
| triggered_at | true |long  | 触发时间| |
| order_insert_at | true |long  | 下order单时间| |
| canceled_at | true |long | 撤单时间| |
| fail_code | true |int | 被触发时下order单失败错误码| |
| fail_reason | true |string | 被触发时下order单失败原因| |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| \</orders\>                  |              |          |                            |                |
| \</data\> |   | |  | |
| ts                         | true         | long     | 响应生成时间点，单位：毫秒 |  |

## 【全仓】获取计划委托历史委托

 - POST `/linear-swap-api/v1/swap_cross_trigger_hisorders`

#### 备注
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述              |  默认值        | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- |----- | ---------------------------------------- |
| contract_code | true        | string   | 合约代码 |   | BTC-USDT|
| trade_type        | true         | int      | 交易类型               |            | 0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多；后台是根据该值转换为offset和direction，然后去查询的； 其他值无法查询出结果 |
| status        | true         | string      | 订单状态               |            | 多个以英文逗号隔开，计划委托单状态：0:全部（表示全部结束状态的订单）、4:已委托、5:委托失败、6:已撤单 |
| create_date   | true         | int      | 日期                   |            | 可随意输入正整数，如果参数超过90则默认查询90天的数据      |
| page_index    | false        | int      | 页码，不填默认第1页    | 1          | 第几页，不填默认第一页 |
| page_size     | false        | int      | 不填默认20，不得多于50 | 20         | 不填默认20，不得多于50 |
| sort_by | false  | string | 排序字段（降序），不填默认按照created_at降序 | created_at  | "created_at"：按订单创建时间进行降序，"update_time"：按订单更新时间进行降序|

#### 备注：
  - 只查询 已完成订单（status对应状态范围 4、5、6）;

> Response

```json

{
    "status": "ok",
    "data": {
        "orders": [
            {
                "symbol": "ETH",
                "contract_code": "ETH-USDT",
                "trigger_type": "ge",
                "volume": 1,
                "order_type": 1,
                "direction": "sell",
                "offset": "open",
                "lever_rate": 30,
                "order_id": 1880,
                "order_id_str": "1880",
                "relation_order_id": "-1",
                "order_price_type": "limit",
                "status": 6,
                "order_source": "api",
                "trigger_price": 90,
                "triggered_price": null,
                "order_price": 90,
                "created_at": 1606977456761,
                "triggered_at": null,
                "order_insert_at": 0,
                "canceled_at": 1606977508571,
                "update_time": 1606977508571,
                "fail_code": null,
                "fail_reason": null,
                "margin_mode": "cross",
                "margin_account": "USDT"
            }
        ],
        "total_page": 2,
        "current_page": 1,
        "total_size": 2
    },
    "ts": 1606978565722
}

```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| \<data\> |  true  | object | 成功处理返回的数据  | |
| total_page |true | int |  总页数 | |
| current_page | true |int |  当前页 | |
| total_size | true |int |  总条数 | |
| \<orders\>|   true          |    object array      |     订单信息                       |                |
| symbol |true |string |合约品种 | |
| contract_code |true | string  | 合约代码 | |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| trigger_type | true |string  | 触发类型   | `ge`大于等于；`le`小于等于 |
| volume | true |decimal  | 委托数量 | |
| order_type | true |int  | 订单类型  | 1、报单  2、撤单 |
| direction | true |string  | 订单方向  | [买(buy),卖(sell)] |
| offset | true |string  | 开平标志 | [开(open),平(close)]  |
| lever_rate | true |int | 杠杆倍数  | |
| order_id | true |long  | 计划委托单订单ID | |
| order_id_str | true |string  | 字符串类型的订单ID  | |
| relation_order_id | true | string  | 该字段为关联限价单的关联字段，未触发前数值为-1 | |
| order_price_type | true |string | 订单报价类型 |  限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20 |
| status | true |int  | 订单状态 | (4:报单成功、5:报单失败、6:已撤单 ) |
| order_source | true |string | 来源 | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发） |
| trigger_price | true |decimal | 触发价| |
| triggered_price | true |decimal  | 被触发时的价格| |
| order_price | true |decimal  | 委托价| |
| created_at | true |long  | 订单创建时间| |
| update_time	 | true |long  | 订单更新时间，单位：毫秒	| |
| triggered_at | true |long  | 触发时间| |
| order_insert_at | true |long  | 下order单时间| |
| canceled_at | true |long | 撤单时间| |
| fail_code | true |int | 被触发时下order单失败错误码| |
| fail_reason | true |string | 被触发时下order单失败原因| |
| \</orders\>                  |              |          |                            |                |
| \</data\> |   | |  | |
| ts                         | true         | long     | 响应生成时间点，单位：毫秒 |  |


## 【逐仓】对仓位设置止盈止损订单

 - POST `/linear-swap-api/v1/swap_tpsl_order`

#### 备注
 - 止盈触发价格和止损触发价格至少填写一个，当触发价格未填写时则不会下该类型止盈止损单。
 - 止盈止损订单都为平仓单。
 - 该接口仅支持逐仓模式。
 - 该接口的限频次数为1秒5次。

> Request

```json
{
    "contract_code": "btc-usdt",
    "direction": "sell",
    "volume": 1,
    "tp_trigger_price": 32000,
    "tp_order_price": 32000,
    "tp_order_price_type": "optimal_5",
    "sl_trigger_price": "29000",
    "sl_order_price": "29000",
    "sl_order_price_type": "optimal_5"
}
```

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述                    | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- | ---------------------------------------- |
| contract_code   | true | String | 合约代码    | BTC-USDT                                |
| direction | true | string | 买卖方向| buy:买入平空 sell:卖出平多  |
| volume | true | decimal |委托数量(张)|  |
| tp_trigger_price          | false | decimal | 止盈触发价格                  |                            |
| tp_order_price   | false | decimal | 	止盈委托价格（最优N档委托类型时无需填写价格）                  |  |
| tp_order_price_type   | false | string | 止盈委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |
| sl_trigger_price          | false | decimal | 止损触发价格                  |                            |
| sl_order_price   | false | decimal | 	止损委托价格（最优N档委托类型时无需填写价格）                  |  |
| sl_order_price_type   | false | string | 止损委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |


> Response

```json
{
    "status": "ok",
    "data": {
        "tp_order": {
            "order_id": 795713650661638144,
            "order_id_str": "795713650661638144"
        },
        "sl_order": {
            "order_id": 795713650665832448,
            "order_id_str": "795713650665832448"
        }
    },
    "ts": 1609754517975
}
```

> Error Response

```json
{
    "status": "error",
    "err_code": 1066,
    "err_msg": "contract_code cannot be empty.",
    "ts": 1604369954194
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| ts |  true  | long | 时间戳 | |
| \<data\> |  false  | object | 成功处理返回的数据，下单失败时不返回  | |
| \<tp_order\>  |  true  | object |   止盈单下单结果   | |
| order_id  |  true  | long | 止盈订单ID   | |
| order_id_str |  true  | string | 止盈订单ID（字符串格式）   | |
| \</tp_order\>  |   | |      | |
| \<sl_order\>  |  true  | object |   止损单下单结果   | |
| order_id  |  true  | long | 止损订单ID   | |
| order_id_str |  true  | string | 止损订单ID（字符串格式）   | |
| \</sl_order\>  |   | |      | |
| \</data\> |   | |  | |
| err_code  |  false  | int | 错误码（下单失败才出现）  | |
| err_msg |  false  | string | 错误信息（下单失败才出现）   | |

#### 备注
 - 当用户只设置了止盈或止损时，则对应返回的sl_order/tp_order则为空。


## 【全仓】对仓位设置止盈止损订单

  - POST `/linear-swap-api/v1/swap_cross_tpsl_order`

#### 备注：
 - 止盈触发价格和止损触发价格至少填写一个，当触发价格未填写时则不会下该类型止盈止损单。
 - 该接口仅支持全仓模式。
 - 止盈止损订单都为平仓单。
 - 该接口的限频次数为1秒5次。

> Request

```json
{
    "contract_code": "btc-usdt",
    "direction": "sell",
    "volume": 1,
    "tp_trigger_price": 32000,
    "tp_order_price": 32000,
    "tp_order_price_type": "optimal_5",
    "sl_trigger_price": "29000",
    "sl_order_price": "29000",
    "sl_order_price_type": "optimal_5"
}
```

### 请求参数

| 参数名称            | 是否必须  | 类型     | 描述                    | 取值范围                                     |
| --------------- | ----- | ------ | --------------------- | ---------------------------------------- |
| contract_code   | true | String | 合约代码    | BTC-USDT                                |
| direction | true | string | 买卖方向| buy:买入平空 sell:卖出平多  |
| volume | true | decimal |委托数量(张)|  |
| tp_trigger_price          | false | decimal | 止盈触发价格                  |                            |
| tp_order_price   | false | decimal | 	止盈委托价格（最优N档委托类型时无需填写价格）                  |  |
| tp_order_price_type   | false | string | 止盈委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |
| sl_trigger_price          | false | decimal | 止损触发价格                  |                            |
| sl_order_price   | false | decimal | 	止损委托价格（最优N档委托类型时无需填写价格）                  |  |
| sl_order_price_type   | false | string | 止损委托类型    |    不填默认为limit; 限价：limit ，最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20            |

> Response

```json
{
    "status": "ok",
    "data": {
        "tp_order": {
            "order_id": 795714078698749952,
            "order_id_str": "795714078698749952"
        },
        "sl_order": {
            "order_id": 795714078698749953,
            "order_id_str": "795714078698749953"
        }
    },
    "ts": 1609754620038
}
```

> Error Response

```json
{
    "status": "error",
    "err_code": 1066,
    "err_msg": "contract_code cannot be empty.",
    "ts": 1604369954194
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status                     | true         | string   | 请求处理结果               | "ok" , "error" |
| ts |  true  | long | 时间戳 | |
| \<data\> |  false  | object | 成功处理返回的数据，下单失败时不返回  | |
| \<tp_order\>  |  true  | object |   止盈单下单结果   | |
| order_id  |  true  | long | 止盈订单ID   | |
| order_id_str |  true  | string | 止盈订单ID（字符串格式）   | |
| \</tp_order\>  |   | |      | |
| \<sl_order\>  |  true  | object |   止损单下单结果   | |
| order_id  |  true  | long | 止损订单ID   | |
| order_id_str |  true  | string | 止损订单ID（字符串格式）   | |
| \</sl_order\>  |   | |      | |
| \</data\> |   | |  | |
| err_code  |  false  | int | 错误码（下单失败才出现）  | |
| err_msg |  false  | string | 错误信息（下单失败才出现）   | |

#### 备注

  - 只设置了止盈或止损时，则对应返回的sl_order/tp_order则为空。

## 【逐仓】止盈止损订单撤单

 - POST `/linear-swap-api/v1/swap_tpsl_cancel`

#### 备注
 - 该接口仅支持逐仓模式。
 - 该接口的限频次数为1秒5次。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码|  "BTC-USDT" ...  |
| order_id | true | string | 止盈止损订单ID（多个订单ID中间以","分隔,一次最多允许撤消10个订单 ）|    |

> Response

```json
{
    "status": "ok",
    "data": {
        "errors": [
            {
                "order_id": "795713650661638145",
                "err_code": 1061,
                "err_msg": "This order doesnt exist."
            }
        ],
        "successes": "795713650661638144"
    },
    "ts": 1609754722004
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| \<data\>        |   true    |   object     |                               | 字典                   |
| \<errors\>        |   true    |   object     |                               | 字典                   |
| order_id        | true  | string | 止盈止损订单ID[全局唯一] |                      |
| err_code              | false  | long   | 错误码                |                      |
| err_msg              | false  | string   | 错误信息               |                      |
| \</errors\>       |       |        |     |  |
| successes              | true  | string   | 成功的订单                 |     |
| \</data\>       |       |        |     |  |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |     |


## 【全仓】止盈止损订单撤单

 - POST `/linear-swap-api/v1/swap_cross_tpsl_cancel`

#### 备注：
 - 该接口仅支持全仓模式。
 - 该接口的限频次数为1秒5次。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码|  "BTC-USDT" ...  |
| order_id | true | string | 止盈止损订单ID（多个订单ID中间以","分隔,一次最多允许撤消10个订单 ）|    |

> Response

```json
{
    "status": "ok",
    "data": {
        "errors": [
            {
                "order_id": "795714078698749956",
                "err_code": 1061,
                "err_msg": "This order doesnt exist."
            }
        ],
        "successes": "795714078698749952"
    },
    "ts": 1609754775942
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| \<data\>        |   true    |   object     |                               | 字典                   |
| \<errors\>        |   true    |   object     |                               | 字典                   |
| order_id        | true  | string | 止盈止损订单ID[全局唯一] |                      |
| err_code              | false  | long   | 错误码                |                      |
| err_msg              | false  | string   | 错误信息               |                      |
| \</errors\>       |       |        |     |  |
| successes              | true  | string   | 成功的订单                 |     |
| \</data\>       |       |        |     |  |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |     |


## 【逐仓】止盈止损订单全部撤单

 - POST `/linear-swap-api/v1/swap_tpsl_cancelall`

#### 备注
 - 该接口仅支持逐仓模式。
 - 该接口的限频次数为1秒5次。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码|  "BTC-USDT" ...  |
| direction | false  | string | 买卖方向（不填默认全部）  |  "buy":买 "sell":卖 |

> Response

```json
{
    "status": "ok",
    "data": {
        "errors": [],
        "successes": "795713650665832448,795714964661583872,795714964661583873"
    },
    "ts": 1609754843671
}
```

### 返回参数

| 参数名称                   | 是否必须 | 类型      | 描述                 | 取值范围                                     |
| ---------------------- | ---- | ------- | ------------------ | ---------------------------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| \<data\>        |   true    |   object     |                               | 字典                   |
| \<errors\>        |   true    |   object     |                               | 字典                   |
| order_id        | true  | string | 止盈止损订单ID[全局唯一] |                      |
| err_code              | false  | long   | 错误码                |                      |
| err_msg              | false  | string   | 错误信息               |                      |
| \</errors\>       |       |        |     |  |
| successes              | true  | string   | 成功的订单                 |     |
| \</data\>       |       |        |     |  |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |     |


## 【全仓】止盈止损订单全部撤单

 - POST `/linear-swap-api/v1/swap_cross_tpsl_cancelall`

#### 备注：
 - 该接口仅支持全仓模式。
 - 该接口的限频次数为1秒5次。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码|  "BTC-USDT" ...  |
| direction | false  | string | 买卖方向（不填默认全部）  |  "buy":买 "sell":卖 |

> Response

```json
{
    "status": "ok",
    "data": {
        "errors": [],
        "successes": "795714078698749953,795715192882053120,795715192886247424"
    },
    "ts": 1609754894463
}
```

### 返回参数

| 参数名称                   | 是否必须 | 类型      | 描述                 | 取值范围                                     |
| ---------------------- | ---- | ------- | ------------------ | ---------------------------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| \<data\>        |   true    |   object     |                               | 字典                   |
| \<errors\>        |   true    |   object     |                               | 字典                   |
| order_id        | true  | string | 止盈止损订单ID[全局唯一] |                      |
| err_code              | false  | long   | 错误码                |                      |
| err_msg              | false  | string   | 错误信息               |                      |
| \</errors\>       |       |        |     |  |
| successes              | true  | string   | 成功的订单                 |     |
| \</data\>       |       |        |     |  |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |     |


## 【逐仓】查询止盈止损订单当前委托

 - POST `/linear-swap-api/v1/swap_tpsl_openorders`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码|  "BTC-USDT" ...  |
| page_index | false | int | 第几页，不填默认第一页|    |
| page_size | false | int | 不填默认20，不得多于50|    |
| trade_type  | false | int    |  交易类型，不填默认查询全部         | 0:全部,3: 买入平空,4: 卖出平多。   |
> Response

```json
{
    "status": "ok",
    "data": {
        "orders": [
            {
                "symbol": "BTC",
                "contract_code": "BTC-USDT",
                "margin_mode": "isolated",
                "margin_account": "BTC-USDT",
                "volume": 1,
                "order_type": 1,
                "direction": "buy",
                "order_id": 795715396674895872,
                "order_id_str": "795715396674895872",
                "order_source": "api",
                "trigger_type": "le",
                "trigger_price": 27000,
                "order_price": 0,
                "created_at": 1609754934244,
                "order_price_type": "optimal_5",
                "status": 2,
                "tpsl_order_type": "tp",
                "source_order_id": "795715396666507264",
                "relation_tpsl_order_id": "795715396674895873"
            }
        ],
        "total_page": 4,
        "current_page": 1,
        "total_size": 4
    },
    "ts": 1609755183516
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| \<data\>        |   true    |   object     |                               | 字典                   |
| total_page        | true | int | 总页数   |                |
| total_size        | true | int | 总条数   |                |
| current_page        | true | int | 当前页   |                |
| \<orders\>        |   true    |   object array    |                               |     |
| symbol                 | true | string  | 品种代码               |                                          |
| contract_code          | true | string  | 合约代码               | "BTC-USDT" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式；isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“USDT”，“BTC-USDT” |
| volume                 | true | decimal  | 委托数量 |      |
| order_type           | true | int | 订单类型：1、报单 2、撤单               |                                          |
| tpsl_order_type            | true | string | 止盈止损类型                |           “tp”:止盈单；"sl"：止损单        |
| direction            | true | string | 买卖方向                |           买入平空："buy",卖出平多："sell"         |
| order_id      | true | long | 止盈止损订单ID                |                                          |
| order_id_str             | true | string | 字符串类型的止盈止损订单ID              |                                          |
| order_source      | true | string  | 来源        |                                          |
| trigger_type              | true | string  | 触发类型： ge大于等于；le小于等于  |              |
| trigger_price         | true | decimal | 触发价              |                      |
| created_at        | true  | long | 订单创建时间 |                      |
| order_price_type        | true  | string | 订单报价类型  |  限价："limit"， 最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20        |
| order_price	      | true | decimal  |  委托价	       |                                          |
| status        | true  | int | 订单状态： |     1:未生效、2:等待委托、3:委托中、4:委托成功、5:委托失败、6:已撤单、8：撤单未找到、9：撤单中、10：失败 、11：已失效     |
| source_order_id        | true  | string |  源限价单的订单id（下单设置的止盈止损订单该字段才有值，表示当前止盈止损单由哪个限价单触发的） |       |
| relation_tpsl_order_id        | true  | string |  关联的止盈止损单id（用户同时设置止盈止损单时，该字段才有值，否则数值为-1） |       |
| \</orders\>       |       |        |     |  |
| \</data\>       |       |        |     |  |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |     |


## 【全仓】查询止盈止损订单当前委托

 - POST `/linear-swap-api/v1/swap_cross_tpsl_openorders`

#### 备注：
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码|  "BTC-USDT" ...  |
| page_index | false | int | 第几页，不填默认第一页|    |
| page_size | false | int | 不填默认20，不得多于50|    |
| trade_type  | false | int    |  交易类型，不填默认查询全部         | 0:全部,3: 买入平空,4: 卖出平多。   |

> Response

```json
{
    "status": "ok",
    "data": {
        "orders": [
            {
                "symbol": "BTC",
                "contract_code": "BTC-USDT",
                "margin_mode": "cross",
                "margin_account": "USDT",
                "volume": 1,
                "order_type": 1,
                "direction": "buy",
                "order_id": 795708162867838976,
                "order_id_str": "795708162867838976",
                "order_source": "api",
                "trigger_type": "le",
                "trigger_price": 27000,
                "order_price": 0,
                "created_at": 1609753209570,
                "order_price_type": "optimal_5",
                "status": 2,
                "tpsl_order_type": "tp",
                "source_order_id": "795708162863644672",
                "relation_tpsl_order_id": "795708162867838977"
            }
        ],
        "total_page": 2,
        "current_page": 1,
        "total_size": 2
    },
    "ts": 1609756633067
}
```
### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| \<data\>        |   true    |   object     |                               | 字典                   |
| total_page        | true | int | 总页数   |                |
| total_size        | true | int | 总条数   |                |
| current_page        | true | int | 当前页   |                |
| \<orders\>        |   true    |   object array    |                               |     |
| symbol                 | true | string  | 品种代码               |                                          |
| contract_code          | true | string  | 合约代码               | "BTC-USDT" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式；isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“USDT”，“BTC-USDT” |
| volume                 | true | decimal  | 委托数量 |      |
| order_type           | true | int | 订单类型：1、报单 2、撤单               |                                          |
| tpsl_order_type            | true | string | 止盈止损类型                |           “tp”:止盈单；"sl"：止损单        |
| direction            | true | string | 买卖方向                |           买入平空："buy",卖出平多："sell"         |
| order_id      | true | long | 止盈止损订单ID                |                                          |
| order_id_str             | true | string | 字符串类型的止盈止损订单ID              |                                          |
| order_source      | true | string  | 来源        |                                          |
| trigger_type              | true | string  | 触发类型： ge大于等于；le小于等于  |              |
| trigger_price         | true | decimal | 触发价              |                      |
| created_at        | true  | long | 订单创建时间 |                      |
| order_price_type        | true  | string | 订单报价类型  |  限价："limit"， 最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20        |
| order_price	      | true | decimal  |  委托价	       |                                          |
| status        | true  | int | 订单状态： |     1:未生效、2:等待委托、3:委托中、4:委托成功、5:委托失败、6:已撤单、8：撤单未找到、9：撤单中、10：失败 、11：已失效    |
| source_order_id        | true  | string |  源限价单的订单id（下单设置的止盈止损订单该字段才有值，表示当前止盈止损单由哪个限价单触发的） |       |
| relation_tpsl_order_id        | true  | string |  关联的止盈止损单id（用户同时设置止盈止损单时，该字段才有值，否则数值为-1） |       |
| \</orders\>       |       |        |     |  |
| \</data\>       |       |        |     |  |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |     |


## 【逐仓】查询止盈止损订单历史委托

 - POST `/linear-swap-api/v1/swap_tpsl_hisorders`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码,"BTC-USDT" ...|    |
| status | true | string | 订单状态| 多个以英文逗号隔开，止盈止损订单状态： 0:全部（表示全部结束状态的订单）、4:委托成功、5:委托失败、6:已撤单、11：已失效   |
| create_date | true | long | 日期| 可随意输入正整数，如果参数超过90则默认查询90天的数据   |
| page_index | false | int | 第几页，不填默认第一页|    |
| page_size | false | int | 不填默认20，不得多于50|    |
| sort_by | false  | string | 排序字段（降序），不填默认按照created_at降序 |  "created_at"：按订单创建时间进行降序，"update_time"：按订单更新时间进行降序|

> Response

```json
{
    "status": "ok",
    "data": {
        "orders": [
            {
                "symbol": "BTC",
                "contract_code": "BTC-USDT",
                "margin_mode": "isolated",
                "margin_account": "BTC-USDT",
                "volume": 1,
                "order_type": 1,
                "tpsl_order_type": "sl",
                "direction": "sell",
                "order_id": 795714964661583873,
                "order_id_str": "795714964661583873",
                "order_source": "api",
                "trigger_type": "le",
                "trigger_price": 29000,
                "created_at": 1609754831244,
                "order_price_type": "optimal_5",
                "status": 6,
                "source_order_id": null,
                "relation_tpsl_order_id": "795714964661583872",
                "canceled_at": 1609754844420,
                "fail_code": null,
                "fail_reason": null,
                "triggered_price": null,
                "relation_order_id": "-1",
                "update_time": 1609754850018,
                "order_price": 0
            }
        ],
        "total_page": 17,
        "current_page": 1,
        "total_size": 17
    },
    "ts": 1609756931689
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| \<data\>        |   true    |   object     |                               | 字典                   |
| total_page        | true | int | 总页数   |                |
| total_size        | true | int | 总条数   |                |
| current_page        | true | int | 当前页   |                |
| \<orders\>        |   true    |   object array    |                               |     |
| symbol                 | true | string  | 品种代码               |                                          |
| contract_code          | true | string  | 合约代码               | "BTC-USDT" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式；isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“USDT”，“BTC-USDT” |
| volume                 | true | decimal  | 委托数量 |      |
| order_type           | true | int | 订单类型：1、报单 2、撤单               |                                          |
| tpsl_order_type            | true | string | 止盈止损类型                |           “tp”:止盈单；"sl"：止损单        |
| direction            | true | string | 买卖方向                |           买入平空："buy",卖出平多："sell"         |
| order_id      | true | long | 止盈止损订单ID                |                                          |
| order_id_str             | true | string | 字符串类型的止盈止损订单ID              |                                          |
| order_source      | true | string  | 来源        |                                          |
| trigger_type              | true | string  | 触发类型： ge大于等于；le小于等于  |              |
| trigger_price         | true | decimal | 触发价              |                      |
| created_at        | true  | long | 订单创建时间 |                      |
| order_price_type        | true  | string | 订单报价类型  |  限价："limit"， 最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20        |
| order_price	      | true | decimal  |  委托价	       |                                          |
| status        | true  | int | 订单状态： |    1:未生效、2:等待委托、3:委托中、4:委托成功、5:委托失败、6:已撤单、8：撤单未找到、9：撤单中、10：失败 、11：已失效    |
| source_order_id        | true  | string |  源限价单的订单id（下单设置的止盈止损订单该字段才有值，表示当前止盈止损单由哪个限价单触发的） |       |
| relation_tpsl_order_id        | true  | string |  关联的止盈止损单id（用户同时设置止盈止损单时，该字段才有值，否则数值为-1） |       |
| canceled_at        | true  | long | 撤单时间 |                      |
| fail_code        | true  | int | 被触发时下order单失败错误码 |                      |
| fail_reason        | true  | string | 被触发时下order单失败原因 |                      |
| triggered_price   | true | decimal | 被触发时的价格                |  |
| relation_order_id          | true | string |  该字段为关联限价单的关联字段，未触发前数值为-1	           |                       |
| update_time | true  | long | 订单更新时间，单位：毫秒 |  |
| \</orders\>       |       |        |     |  |
| \</data\>       |       |        |     |  |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |     |


## 【全仓】查询止盈止损订单历史委托

 - POST `linear-swap-api/v1/swap_cross_tpsl_hisorders`

#### 备注：
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码,"BTC-USDT" ...|    |
| status | true | string | 订单状态| 多个以英文逗号隔开，止盈止损订单状态： 0:全部（表示全部结束状态的订单）、4:委托成功、5:委托失败、6:已撤单、11：已失效   |
| create_date | true | long | 日期| 可随意输入正整数，如果参数超过90则默认查询90天的数据   |
| page_index | false | int | 第几页，不填默认第一页|    |
| page_size | false | int | 不填默认20，不得多于50|    |
| sort_by | false  | string | 排序字段（降序），不填默认按照created_at降序 |  "created_at"：按订单创建时间进行降序，"update_time"：按订单更新时间进行降序|

> Response

```json
{
    "status": "ok",
    "data": {
        "orders": [
            {
                "symbol": "BTC",
                "contract_code": "BTC-USDT",
                "margin_mode": "cross",
                "margin_account": "USDT",
                "volume": 1,
                "order_type": 1,
                "tpsl_order_type": "sl",
                "direction": "sell",
                "order_id": 795715192886247424,
                "order_id_str": "795715192886247424",
                "order_source": "api",
                "trigger_type": "le",
                "trigger_price": 29000,
                "created_at": 1609754885657,
                "order_price_type": "optimal_5",
                "status": 6,
                "source_order_id": null,
                "relation_tpsl_order_id": "795715192882053120",
                "canceled_at": 1609754894877,
                "fail_code": null,
                "fail_reason": null,
                "triggered_price": null,
                "relation_order_id": "-1",
                "update_time": 1609754910025,
                "order_price": 0
            }
        ],
        "total_page": 4,
        "current_page": 1,
        "total_size": 4
    },
    "ts": 1609759934758
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| \<data\>        |   true    |   object     |                               | 字典                   |
| total_page        | true | int | 总页数   |                |
| total_size        | true | int | 总条数   |                |
| current_page        | true | int | 当前页   |                |
| \<orders\>        |   true    |   object array    |                               |     |
| symbol                 | true | string  | 品种代码               |                                          |
| contract_code          | true | string  | 合约代码               | "BTC-USDT" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式；isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“USDT”，“BTC-USDT” |
| volume                 | true | decimal  | 委托数量 |      |
| order_type           | true | int | 订单类型：1、报单 2、撤单               |                                          |
| tpsl_order_type            | true | string | 止盈止损类型                |           “tp”:止盈单；"sl"：止损单        |
| direction            | true | string | 买卖方向                |           买入平空："buy",卖出平多："sell"         |
| order_id      | true | long | 止盈止损订单ID                |                                          |
| order_id_str             | true | string | 字符串类型的止盈止损订单ID              |                                          |
| order_source      | true | string  | 来源        |                                          |
| trigger_type              | true | string  | 触发类型： ge大于等于；le小于等于  |              |
| trigger_price         | true | decimal | 触发价              |                      |
| created_at        | true  | long | 订单创建时间 |                      |
| order_price_type        | true  | string | 订单报价类型  |  限价："limit"， 最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20        |
| order_price	      | true | decimal  |  委托价	       |                                          |
| status        | true  | int | 订单状态： |    1:未生效、2:等待委托、3:委托中、4:委托成功、5:委托失败、6:已撤单、8：撤单未找到、9：撤单中、10：失败 、11：已失效    |
| source_order_id        | true  | string |  源限价单的订单id（下单设置的止盈止损订单该字段才有值，表示当前止盈止损单由哪个限价单触发的） |       |
| relation_tpsl_order_id        | true  | string |  关联的止盈止损单id（用户同时设置止盈止损单时，该字段才有值，否则数值为-1） |       |
| canceled_at        | true  | long | 撤单时间 |                      |
| fail_code        | true  | int | 被触发时下order单失败错误码 |                      |
| fail_reason        | true  | string | 被触发时下order单失败原因 |                      |
| triggered_price   | true | decimal | 被触发时的价格                |  |
| relation_order_id          | true | string |  该字段为关联限价单的关联字段，未触发前数值为-1	           |                       |
| update_time | true  | long | 订单更新时间，单位：毫秒 |  |
| \</orders\>       |       |        |     |  |
| \</data\>       |       |        |     |  |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |     |


## 【逐仓】查询开仓单关联的止盈止损订单详情

 - POST `/linear-swap-api/v1/swap_relation_tpsl_order`

#### 备注
 - 该接口仅支持逐仓模式。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码|  "BTC-USDT" ...  |
| order_id | true | long | 开仓订单id  |    |

> Response

```json
{
    "status": "ok",
    "data": {
        "symbol": "BTC",
        "contract_code": "BTC-USDT",
        "margin_mode": "isolated",
        "margin_account": "BTC-USDT",
        "volume": 1,
        "price": 29999,
        "order_price_type": "opponent",
        "direction": "buy",
        "offset": "open",
        "lever_rate": 75,
        "order_id": 795947785812557824,
        "order_id_str": "795947785812557824",
        "client_order_id": null,
        "created_at": 1609810340126,
        "trade_volume": 1,
        "trade_turnover": 29.999,
        "fee": -0.01619946,
        "trade_avg_price": 29999,
        "margin_frozen": 0,
        "profit": 0,
        "status": 6,
        "order_type": 1,
        "order_source": "api",
        "fee_asset": "USDT",
        "canceled_at": 0,
        "tpsl_order_info": [
            {
                "volume": 1,
                "direction": "sell",
                "tpsl_order_type": "tp",
                "order_id": 795947785820946432,
                "order_id_str": "795947785820946432",
                "trigger_type": "ge",
                "trigger_price": 31000,
                "order_price": 0,
                "created_at": 1609810340134,
                "order_price_type": "optimal_5",
                "relation_tpsl_order_id": "795947785820946433",
                "status": 1,
                "canceled_at": 0,
                "fail_code": null,
                "fail_reason": null,
                "triggered_price": null,
                "relation_order_id": "-1"
            },
            {
                "volume": 1,
                "direction": "sell",
                "tpsl_order_type": "sl",
                "order_id": 795947785820946433,
                "order_id_str": "795947785820946433",
                "trigger_type": "le",
                "trigger_price": 29100,
                "order_price": 0,
                "created_at": 1609810340134,
                "order_price_type": "optimal_5",
                "relation_tpsl_order_id": "795947785820946432",
                "status": 1,
                "canceled_at": 0,
                "fail_code": null,
                "fail_reason": null,
                "triggered_price": null,
                "relation_order_id": "-1"
            }
        ]
    },
    "ts": 1609810352828
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| \<data\>        |   true    |   object     |                               | 字典                   |
| symbol               | true | string  | 品种代码   |                                          |
| contract_code        | true | string  | 合约代码   | "BTC-USDT" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式；isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“USDT”，“BTC-USDT” |
| volume               | true | decimal | 委托数量   |                                          |
| price                | true | decimal | 委托价格   |                                          |
| order_price_type     | true | string  | 订单报价类型 | "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| direction            | true | string  | 买卖方向   | "buy":买 "sell":卖                         |
| offset               | true | string  | 开平方向   | "open":开 "close":平                       |
| lever_rate           | true | int     | 杠杆倍数   |                         |
| order_id             | true | long    | 订单ID   |                                          |
| order_id_str             | true | string    | String类型订单ID   |                                          |
| client_order_id      | true | long    | 客户订单ID |                                          |
| created_at           | true | long    | 创建时间   |                                          |
| trade_volume         | true | decimal | 成交数量   |                                          |
| trade_turnover       | true | decimal | 成交总金额  |                                          |
| fee                  | true | decimal | 手续费    |                                          |
| trade_avg_price      | true | decimal | 成交均价   |                                          |
| margin_frozen        | true | decimal | 冻结保证金  |                                          |
| profit               | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）   |                                          |
| status               | true | int     | 订单状态   | (1准备提交 2准备提交 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单 11撤单中) |
| order_type           | true | int  | 订单类型   | 1:报单 、 2:撤单 、 3:强平、4:交割                  |
| order_source         | true | string  | 订单来源   | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发） |
| fee_asset         | true | string  | 手续费币种   | （"BTC","ETH"...）|
| canceled_at               | true     | long    |撤单时间           |  |
| \<tpsl_order_info\>  |  true  | object array |  关联的止盈止损单信息    | |
| volume                 | true | decimal  | 委托数量  |      |
| tpsl_order_type            | true | string | 止盈止损类型                |           “tp”:止盈单；"sl"：止损单        |
| direction            | true | string | 买卖方向                |           买入平空："buy",卖出平多："sell"         |
| order_id      | true | long | 止盈止损订单ID              |                                          |
| order_id_str             | true | string | 字符串类型的止盈止损订单ID             |                                          |
| trigger_type              | true | string  | 触发类型： ge大于等于；le小于等于  |              |
| trigger_price         | true | decimal | 触发价              |                      |
| order_price         | true | decimal | 委托价              |                      |
| created_at        | true  | long | 订单创建时间 |                      |
| order_price_type        | true  | string | 订单报价类型  |  限价："limit"， 最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20        |
| status        | true  | int | 订单状态 |     1:未生效、2:等待委托、3:委托中、4:委托成功、5:委托失败、6:已撤单、8：撤单未找到、9：撤单中、10：失败' 、11：已失效、12、未生效-已结束        |
| relation_tpsl_order_id        | true  | string |  关联的止盈止损单id（用户同时设置止盈止损单时，该字段才有值，否则数值为-1） |       |
| canceled_at        | true  | long | 撤单时间 |                      |
| fail_code        | true  | int | 被触发时下order单失败错误码 |                      |
| fail_reason        | true  | string | 被触发时下order单失败原因 |                      |
| triggered_price   | true | decimal | 被触发时的价格                |  |
| relation_order_id          | true | string |  该字段为关联限价单的关联字段，未触发前数值为-1	           |                       |
| \</tpsl_order_info\>  |   | |      | |
| \</data\>       |       |        |     |  |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |     |


## 【全仓】查询开仓单关联的止盈止损订单详情

 - POST `/linear-swap-api/v1/swap_cross_relation_tpsl_order`

#### 备注：
 - 该接口仅支持全仓模式。

### 请求参数

| 参数名称          | 是否必须  | 类型     | 描述   | 取值范围                                     |
| ------------- | ----- | ------ | ------------- | ---------------------------------------- |
| contract_code | true | string | 合约代码|  "BTC-USDT" ...  |
| order_id | true | long | 开仓订单id  |    |

> Response

```json
{
    "status": "ok",
    "data": {
        "symbol": "BTC",
        "contract_code": "BTC-USDT",
        "margin_mode": "cross",
        "margin_account": "USDT",
        "volume": 1,
        "price": 29860.8,
        "order_price_type": "opponent",
        "direction": "sell",
        "offset": "open",
        "lever_rate": 75,
        "order_id": 795947312485351424,
        "order_id_str": "795947312485351424",
        "client_order_id": null,
        "created_at": 1609810227268,
        "trade_volume": 1,
        "trade_turnover": 29.8608,
        "fee": -0.016124832,
        "trade_avg_price": 29860.8,
        "margin_frozen": 0,
        "profit": 0,
        "status": 6,
        "order_type": 1,
        "order_source": "api",
        "fee_asset": "USDT",
        "canceled_at": 0,
        "tpsl_order_info": [
            {
                "volume": 1,
                "direction": "buy",
                "tpsl_order_type": "tp",
                "order_id": 795947312493740032,
                "order_id_str": "795947312493740032",
                "trigger_type": "le",
                "trigger_price": 27000,
                "order_price": 0,
                "created_at": 1609810227284,
                "order_price_type": "optimal_5",
                "relation_tpsl_order_id": "795947312493740033",
                "status": 1,
                "canceled_at": 0,
                "fail_code": null,
                "fail_reason": null,
                "triggered_price": null,
                "relation_order_id": "-1"
            },
            {
                "volume": 1,
                "direction": "buy",
                "tpsl_order_type": "sl",
                "order_id": 795947312493740033,
                "order_id_str": "795947312493740033",
                "trigger_type": "ge",
                "trigger_price": 30100,
                "order_price": 0,
                "created_at": 1609810227284,
                "order_price_type": "optimal_5",
                "relation_tpsl_order_id": "795947312493740032",
                "status": 1,
                "canceled_at": 0,
                "fail_code": null,
                "fail_reason": null,
                "triggered_price": null,
                "relation_order_id": "-1"
            }
        ]
    },
    "ts": 1609810242146
}
```

### 返回参数

| 参数名称            | 是否必须  | 类型     | 描述                            | 取值范围                 |
| --------------- | ----- | ------ | ----------------------------- | -------------------- |
| status          | true  | string | 请求处理结果                        | "ok" :成功, "error"：失败 |
| \<data\>        |   true    |   object     |                               | 字典                   |
| symbol               | true | string  | 品种代码   |                                          |
| contract_code        | true | string  | 合约代码   | "BTC-UDST" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式；isolated：逐仓模式 |
| margin_account | true | string | 保证金账户  | 比如“USDT”，“BTC-USDT” |
| volume               | true | decimal | 委托数量   |                                          |
| price                | true | decimal | 委托价格   |                                          |
| order_price_type     | true | string  | 订单报价类型 | "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| direction            | true | string  | 买卖方向   | "buy":买 "sell":卖                         |
| offset               | true | string  | 开平方向   | "open":开 "close":平                       |
| lever_rate           | true | int     | 杠杆倍数   |                         |
| order_id             | true | long    | 订单ID   |                                          |
| order_id_str             | true | string    | String类型订单ID   |                                          |
| client_order_id      | true | long    | 客户订单ID |                                          |
| created_at           | true | long    | 创建时间   |                                          |
| trade_volume         | true | decimal | 成交数量   |                                          |
| trade_turnover       | true | decimal | 成交总金额  |                                          |
| fee                  | true | decimal | 手续费    |                                          |
| trade_avg_price      | true | decimal | 成交均价   |                                          |
| margin_frozen        | true | decimal | 冻结保证金  |                                          |
| profit               | true | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）   |                                          |
| status               | true | int     | 订单状态   | (1准备提交 2准备提交 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单 11撤单中) |
| order_type           | true | int  | 订单类型   | 1:报单 、 2:撤单 、 3:强平、4:交割                  |
| order_source         | true | string  | 订单来源   | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发） |
| fee_asset         | true | string  | 手续费币种   | （"BTC","ETH"...）|
| canceled_at               | true     | long    |撤单时间           |  |
| \<tpsl_order_info\>  |  true  | object array |  关联的止盈止损单信息    | |
| volume                 | true | decimal  | 委托数量  |      |
| tpsl_order_type            | true | string | 止盈止损类型                |           “tp”:止盈单；"sl"：止损单        |
| direction            | true | string | 买卖方向                |           买入平空："buy",卖出平多："sell"         |
| order_id      | true | long | 止盈止损订单ID              |                                          |
| order_id_str             | true | string | 字符串类型的止盈止损订单ID          |                                          |
| trigger_type              | true | string  | 触发类型： ge大于等于；le小于等于  |              |
| trigger_price         | true | decimal | 触发价              |                      |
| order_price         | true | decimal | 委托价              |                      |
| created_at        | true  | long | 订单创建时间 |                      |
| order_price_type        | true  | string | 订单报价类型  |  限价："limit"， 最优5档：optimal_5，最优10档：optimal_10，最优20档：optimal_20        |
| status        | true  | int | 订单状态 |    1:未生效、2:等待委托、3:委托中、4:委托成功、5:委托失败、6:已撤单、8：撤单未找到、9：撤单中、10：失败' 、11：已失效、12、未生效-已结束       |
| relation_tpsl_order_id        | true  | string |  关联的止盈止损单id（用户同时设置止盈止损单时，该字段才有值，否则数值为-1） |       |
| canceled_at        | true  | long | 撤单时间 |                      |
| fail_code        | true  | int | 被触发时下order单失败错误码 |                      |
| fail_reason        | true  | string | 被触发时下order单失败原因 |                      |
| triggered_price   | true | decimal | 被触发时的价格                |  |
| relation_order_id          | true | string |  该字段为关联限价单的关联字段，未触发前数值为-1	           |                       |
| \</tpsl_order_info\>  |   | |      | |
| \</data\>       |       |        |     |  |
| ts              | true  | long   | 响应生成时间点，单位：毫秒                 |     |


# USDT本位永续合约划转接口

## 【通用】现货-USDT本位永续账户间进行资金的划转

### 实例

- POST `https://api.huobi.pro/v2/account/transfer`

### 备注

该接口支持全仓模式和逐仓模式

此接口用户币币现货账户与USDT本位永续合约账户之间的资金划转。

该接口的访问频次的限制为1秒/1次。

注意：请求地址为火币Global地址

现货与USDT本位永续合约划转接口，所有划转的币的精度是8位小数。

### 请求参数

  参数名称   |  是否必须    |  类型   |  描述      |  取值范围  |
--------------  | --------------  | ---------- |  ------------------------  |  ------------------------------------------------------------------------------------------------------  |
from  |    true  |  string  |  来源业务线账户，取值：spot(币币)、linear-swap(USDT本位永续合约)  |   e.g. spot  |
to  |    true  |  string  |  目标业务线账户，取值：spot(币币)、linear-swap(USDT本位永续合约)  | e.g. linear-swap  |
currency  |    true  |  string  |  币种,支持大小写  |   e.g. usdt  |
amount  |   true  |  decimal  |   划转金额  |      |
margin-account  |   true  |  string  |   保证金账户	  | e.g. btc-usdt、eth-usdt、USDT     |

#### 备注
- 当"margin-account"为USDT时，表示从全仓账户划出或转入。

> Response:

```json

 正确的返回：
{
    "code": 200,
    "data": 176104252,
    "message": "Succeed",
    "success": true
}
错误的返回：
 {
   "code":1303,
   "data":null,
   "message":"The single transfer-out amount must be no less than 0.0008BTC",
   "success":false
}

```

###  返回参数

参数名称  |  是否必须     |  类型    |  描述  |  取值范围  |
------------------ |  -------------- |  ---------- |  ---------------------  |  -----------------------------  |
success  |  true  |   string  |  状态  | true/false   |  
data  |    true  |   long    |    生成的划转订单id  |  |
code |    true  |   long    |     响应码	  |  |
message |    true  |   string    |   响应信息	 |   |


## 响应码列表

响应码 | 中文说明 |  英文说明  | 
------------------------------------  |  --------------------------------  |  ------------------------- |
|200 | 成功 | Succeed |
|403| 拒绝访问 | Access denied |
|404|访问的资源不存在 | The resource being accessed does not exist|
|429|太多的请求 | too many requests|
|500|系统错误 | System error |
|501|无效请求 |Invalid request|
|502|无效参数 | Invalid parameter | 
|504|缺少参数 | Lack of parameter |
|512|拒绝匿名请求 | Reject anonymous requests |
|513|无效的签名 | Invalid signature | 
|10000|币种不存在 | Currency does not exist |
|10001|不支持同业务划转 | Does not support  transfer within single business|
|10002|不支持此划转业务 | This transfer is not supported| 
|10003|from方check校验不通过 | check rejected by the from party|
|10004|to方check校验不通过 |to check rejected by the to party|
|10005|个人账户平账检查不通过  | Personal account balance check failed |
|10006|系统账户检查失败 | System account check failed|
|10008|黑名单校验不通过 | Blacklist check failed|
|10009|用户有未安全上账资产，禁止划转 | No transfer is allowed if the user has any asset that has not been charged to the account safely |
|10010|用户被锁定 | User locked
|10011|24小时内修改过安全策略 | Security policy has been modified within 24 hours
|20001|OTC 人脸识别   | OTC Face Recognition 
|1030 | 服务异常，请稍后再试 | Abnormal service. Please try again later.
|1010 | 用户不存在 | Abnormal service. Please try again later.
| 1012 | 账户不存在 | Abnormal service. Please contact customer service.
| 1013 | 合约品种不存在 | This contract type doesn't exist.
| 1018 | 主账号不存在 | Main account doesn't exist.
| 1089 | {0}合约暂时限制划转,请联系客服  | {0} contract is restricted of transfer.  Please contact customer service.
| 1102 | 您没有转入权限,请联系客服 |  Unable to transfer in currently. Please contact customer service.
| 1103 | 您没有转出权限,请联系客服 | Unable to transfer out currently. Please contact customer service.
| 1106 | 合约状态异常,暂时无法划转 | Abnormal contracts status. Can’t transfer.
| 1111 | 子账号没有转入权限,请联系客服 | Sub-account doesn't own the permissions to transfer in. Please contact customer service.
| 1112 | 子账号没有转出权限,请联系客服 |  sub-account doesn't own the permissions to transfer out. Please contact customer service.
| 1114 | 子账号没有划转权限,请登录主账号授权 | The sub-account does not have transfer permissions. Please login main account to authorize.
| 1300 | 划转失败 | Transfer failed.
| 1301 | 可划转余额不足 | Insufficient amount available.
| 1302 | 系统划转错误 | Transfer failed.
| 1303 | 单笔转出的数量不能低于{0}{1} | The single transfer-out amount must be no less than {0}{1}.
| 1304 | 单笔转出的数量不能高于{0}{1} | The single transfer-out amount must be no more than {0}{1}.
| 1305 | 单笔转入的数量不能低于{0}{1} | The single transfer-in amount must be no less than {0}{1}.
| 1306 | 单笔转入的数量不能高于{0}{1}  | The single transfer-in amount must be no more than {0}{1}.
| 1307 | 您当日累计转出量超过{0}{1}, 暂无法转出 | Your accumulative transfer-out amount is over the daily maximum, {0}{1}. You can't transfer out for the time being.
| 1308 | 您当日累计转入量超过{0}{1}, 暂无法转入 | Your accumulative transfer-in amount is over the daily maximum, {0}{1}. You can't transfer in for the time being.
| 1309 | 您当日累计净转出量超过{0}{1}, 暂无法转出  | Your accumulative net transfer-out amount is over the daily maximum, {0}{1}. You can't transfer out for the time being.
| 1310 | 您当日累计净转入量超过{0}{1}, 暂无法转入 | Your accumulative net transfer-in amount is over the daily maximum, {0}{1}. You can't transfer in for the time being.
| 1311 | 超过平台当日累计最大转出量限制, 暂无法转出 | The platform's accumulative transfer-out amount is over the daily maximum. You can't transfer out for the time being.
| 1312 | 超过平台当日累计最大转入量限制, 暂无法转入 | The platform's accumulative transfer-in amount is over the daily maximum. You can't transfer in for the time being.
| 1313 | 超过平台当日累计最大净转出量限制, 暂无法转出 | The platform's accumulative net transfer-out amount is over the daily maximum. You can't transfer out for the time being.
| 1314 | 超过平台当日累计最大净转入量限制, 暂无法转入 | The platform's accumulative net transfer-in amount is over the daily maximum. You can't transfer in for the time being.
| 1315 | 划转类型错误 | Wrong transfer type.
| 1316 | 划转冻结失败 | Failed to freeze the transfer.
| 1317 | 划转解冻失败 | Failed to unfreeze the transfer.
| 1318 | 划转确认失败 | Failed to confirm the transfer.
| 1319 | 查询可划转金额失败 | Failed to acquire the available transfer amount.
| 1320 | 此合约在非交易状态中, 无法进行系统划 | The contract status is abnormal. Transfer is unavailable temporarily.
| 1321 | 划转失败, 请稍后重试或联系客服 | Transfer failed. Please try again later or contact customer service.
| 1322 | 划转金额必须大于0 | Invalid amount. Must be more than 0.
| 1323 | 服务异常, 划转失败, 请稍后再试 | Abnormal service, transfer failed. Please try again later.
| 1327 | 无划转权限, 划转失败, 请联系客服 | No transfer permission, transfer failed, please contact customer service.
| 1328 | 无划转权限, 划转失败, 请联系客服 | No transfer permission, transfer failed, please contact customer service.
| 1329 | 无划转权限, 划转失败, 请联系客服 | No transfer permission, transfer failed, please contact customer service.
| 1330 | 无划转权限, 划转失败, 请联系客服 | No transfer permission, transfer failed, please contact customer service.
| 1331 | 超出划转精度限制(8位), 请修改后操作 | Exceeds limit of transfer accuracy (8 digits). Please modify it.




# 合约Websocket简介

## 接口列表

| 权限类型  |   接口数据类型    | 接口模式 |  请求方法   |  类型    |  描述                     |  需要验签       |    
----------- | ----------- | ----- | ------------------ |---------- |---------------------------- |--------------|
| 读取    |  市场行情接口 | 通用 |  market.$contract_code.kline.$period                    | sub  | 【通用】订阅 KLine 数据               |       否      |
| 读取    |  市场行情接口 | 通用 |  market.$contract_code.kline.$period                    | req  | 【通用】请求 KLine 数据               |       否      |
| 读取    |  市场行情接口 | 通用 |  market.$contract_code.depth.$type                      | sub  | 【通用】订阅 Market Depth 数据        |       否      |
| 读取    |  市场行情接口 | 通用 |  market.$contract_code.depth.size_${size}.high_freq     | sub  | 【通用】订阅 Market Depth增量推送数据 |       否      |
| 读取    |  市场行情接口 | 通用 |  market.$contract_code.bbo                              | sub  | 【通用】买一卖一逐笔行情推送         |       否      |
| 读取    |  市场行情接口 | 通用 |  market.$contract_code.detail                           | sub  | 【通用】订阅 Market detail 数据       |       否      |
| 读取    |  市场行情接口 | 通用 |  market.$contract_code.trade.detail                     | req  | 【通用】请求 Trade detail 数据        |       否      |
| 读取    |  市场行情接口 | 通用 |  market.$contract_code.trade.detail                     | sub  | 【通用】订阅 Trade Detail 数据        |       否      |
| 读取    |  指数与基差接口 |  通用  | market.$contract_code.index.$period                    | sub  | 【通用】订阅指数K线数据                  |       否      |
| 读取    |  指数与基差接口 |  通用  | market.$contract_code.index.$period                    | req  | 【通用】请求指数K线数据                  |       否      |
| 读取    |  指数与基差接口 |  通用  | market.$contract_code.basis.$period.$basis_price_type  | sub  | 【通用】订阅基差数据                  |       否      |
| 读取    |  指数与基差接口 |  通用  | market.$contract_code.basis.$period.$basis_price_type  | req  | 【通用】请求基差数据                  |       否      |
| 读取    |  指数与基差接口 |  通用  | market.$contract_code.premium_index.$period            | sub  | 【通用】订阅溢价指数K线数据           |       否      |
| 读取    |  指数与基差接口 |  通用  | market.$contract_code.premium_index.$period            | req  | 【通用】请求溢价指数K线数据           |       否      |
| 读取    |  指数与基差接口 |  通用  | market.$contract_code.estimated_rate.$period           | sub  | 【通用】订阅预测资金费率K线数据       |       否      |
| 读取    |  指数与基差接口 |  通用  | market.$contract_code.estimated_rate.$period           | req  | 【通用】请求预测资金费率K线数据       |       否      |
| 读取    |  指数与基差接口 | 通用 |  market.$contract_code.mark_price.$period                    | sub  | 【通用】订阅标记价格 K 线数据              |       否      |
| 读取    |  指数与基差接口 | 通用 |  market.$contract_code.mark_price.$period                    | req  | 【通用】请求标记价格 K 线数据              |       否      |
| 读取    |  交易接口 |  通用 | public.$contract_code.liquidation_orders               | sub  | 【通用】订阅强平订单数据（免鉴权）    |       否      |
| 读取    |  交易接口 |  通用 | public.$contract_code.funding_rate                     | sub  | 【通用】订阅资金费率变动数据（免鉴权）|       否      |
| 读取    |  交易接口 |  通用 | public.$contract_code.contract_info                    | sub  | 【通用】订阅合约信息变动数据（免鉴权）|       否      |
| 读取    |  交易接口 |  逐仓 | orders.$contract_code                                  | sub  | 【逐仓】订阅订单成交数据              |    是       |
| 读取    |  资产接口 |  逐仓 | accounts.$contract_code                                | sub  | 【逐仓】订阅资产变动数据              |    是       |
| 读取    |  资产接口 |  逐仓 | positions.$contract_code                               | sub  | 【逐仓】订阅持仓变动更新数据          |    是       |
| 读取    |  交易接口 |  逐仓 | matchOrders.$contract_code                             | sub  | 【逐仓】订阅撮合订单成交数据          |    是       |
| 读取    |  交易接口 |  逐仓 | trigger_order.$contract_code                             | sub  | 【逐仓】订阅计划委托订单更新ws推送   |    是       |
| 读取    |  资产接口 | 全仓 | orders_cross.$contract_code                               | sub    |  【全仓】订阅订单成交数据         |       是          |
| 读取    |  资产接口 | 全仓 | accounts_cross.$margin_account                            | sub    |  【全仓】订阅资产变动数据         |       是          |
| 读取    |  交易接口 | 全仓 | positions_cross.$contract_code                            | sub    |  【全仓】订阅持仓变动更新数据     |       是          |
| 读取    |  交易接口 | 全仓 | matchOrders_cross.$contract_code                          | sub    |  【全仓】订阅撮合订单成交数据     |       是          |
| 读取    |  交易接口 | 全仓 | trigger_order_cross.$contract_code                        | sub    |  【全仓】订阅计划委托订单变动     |       是          |
| 读取    |  系统状态接口 | 通用  |  public.$service.heartbeat                            | sub    | 【通用】订阅系统状态更新         |       否          | 

## 合约订阅地址

合约站行情请求以及订阅地址为：wss://api.hbdm.com/linear-swap-ws

合约站订单推送订阅地址：wss://api.hbdm.com/linear-swap-notification

合约站指数K线及基差数据订阅地址：wss://api.hbdm.com/ws_index

合约站系统状态更新订阅地址：wss://api.hbdm.com/center-notification

如果api.hbdm.com域名访问不了，可使用：

合约站行情请求以及订阅地址为：wss://api.btcgateway.pro/linear-swap-ws

合约站订单推送订阅地址：wss://api.btcgateway.pro/linear-swap-notification

合约站指数K线及基差数据订阅地址：wss://api.btcgateway.pro/ws_index

合约站系统状态更新订阅地址：wss://api.btcgateway.pro/center-notification

如果对合约订单推送订阅有疑问，可以参考 <a href='https://docs.huobigroup.com/docs/usdt_swap/v1/cn/#2cff7db524'> Demo </a>
 
### 备注

 如果api.hbdm.com无法访问，可以使用api.btcgateway.pro来做调试，AWS服务器用户推荐使用api.hbdm.vn； 
 
## 访问次数限制

公开行情接口和用户私有接口都有访问次数限制

- 普通用户，需要密钥的私有接口，每个UID 3秒最多 72 次请求(交易接口3秒最多 36 次请求，查询接口3秒最多 36 次请求) (该UID的所有币种和不同到期日的合约的所有私有接口共享该限制) 

- 其他非行情类的公开接口，比如获取指数信息，限价信息，交割结算、平台持仓信息等，所有用户都是每个IP3秒最多120次请求（所有该IP的非行情类的公开接口请求共享3秒120次的额度）

- 行情类的公开接口，比如：获取K线数据、获取聚合行情、市场行情、获取行情深度数据、获取溢价指数K线、获取实时预测资金费率k线，获取基差数据、获取市场最近成交记录：

    （1） restful接口：同一个IP, 所有业务（交割合约、币本位永续合约、期权合约和USDT本位永续合约）总共1秒最多800个请求

    （2） websocket：req请求，同一时刻最多请求50次；sub请求，无限制，服务器主动推送数据

- WebSocket私有订单成交推送接口(需要API KEY验签)

    一个UID最多同时建立30个私有订单推送WS链接。该用户在一个品种(包含该品种的所有周期的合约)上，仅需要维持一个订单推送WS链接即可。

    注意: 订单推送WS的限频，跟用户RESTFUL私有接口的限频是分开的，相互不影响。
    
- websocket 1秒同时最多发40个sub请求。

api接口response中的header返回以下字段

- ratelimit-limit： 单轮请求数上限，单位：次数

- ratelimit-interval：请求数重置的时间间隔，单位：毫秒

- ratelimit-remaining：本轮剩余可用请求数，单位：次数

- ratelimit-reset：请求数上限重置时间，单位：毫秒 
 
# WebSocket心跳以及鉴权接口

## 市场行情心跳

- WebSocket Server 发送心跳：

`{"ping": 18212558000}`

- WebSocket Client 应该返回：

`{"pong": 18212558000}`

注：WebSocket Client 和 WebSocket Server 建立连接之后，WebSocket Server 每隔 `5s`（这个频率可能会变化） 会向 WebSocket Client 发起一次心跳，WebSocket Client 忽略心跳 5 次后，WebSocket Server 将会主动断开连接；WebSocket Client发送最近 2 次心跳message中的其中一个`ping`的值，WebSocket Server都会保持WebSocket连接。

## 订单推送心跳

- WebSocket API 支持单向心跳，Server 发起 ping message，Client 返回 pong message。 WebSocket Server 发送心跳:

`{`

   `"op": "ping",`
    
   `"ts": "1492420473058"`
    
`}`

- WebSocket Client 应该返回:

`{`

   `"op": "pong"`
    
   `"ts": "1492420473058"`
    
`}`

### 备注：

- "pong"操作返回数据里面的"ts"的值为"ping"推送收到的"ts"值

- WebSocket Client 和 WebSocket Server 建⽴立连接之后，WebSocket Server 每隔 5s(这个频率可能会变化) 会向 WebSocket Client 发起⼀一次⼼心跳，WebSocket Client 忽略心跳 5 次后，WebSocket Server 将会主动断开连接。

- 异常情况WebSocket Server 会返回错误信息，比如：

`{`

   `"op": "pong"`
    
   `"ts": "1492420473027",`
    
   `"err-code": 2011`
    
   `"err-msg": “详细出错信息”`
    
`}`

## 订单推送访问地址

- 统一服务地址

  合约站订单推送订阅地址：wss://api.hbdm.com/linear-swap-notification

### 备注

 如果api.hbdm.com无法访问，可以使用api.btcgateway.pro来做调试，AWS服务器用户推荐使用api.hbdm.vn； 
 
 正常ws请求连接不能同时超过30个

### 数据压缩

WebSocket API 返回的所有数据都进⾏了 GZIP 压缩，需要 client 在收到数据之后解压

### 请求与响应数据说明

- 字符编码：UTF-8

- 大小写敏感，包含所有参数名和返回值

- 数据类型：使用JSON传输数据

- 所有请求数据都有固定格式，具体接口说明文档中只会重点介绍非通用部分，

> 请求数据结构如下:

```

   {
  "op": string, // 必填;Client 请求的操作类型(Server 会原样返回)，详细操作
  类型列列表请参考附录
  "cid": string, // 选填;当前请求唯一 ID(Client 自⽣成并保证本地唯一性，
  Server 会原样返回) 
  // 其余必填/可选字段
  }

```

> 所有响应/推送数据都会以固定的结构返回，具体接口说明文档中只会重点介绍data部分，请求响应数据结构如下:

```
   
  {
  "op": string, // 必填;本次响应 Client 请求的操作类型
  "cid": string, // 选填;Client 请求唯一 ID
  "ts": long, // 必填;Server 应答时本地时间戳
  "err-code": integer, // 必填;响应码，0 代表成功;非0 代表出错，详细响应码列表请参考错误码表。
  "err-msg": string, 只在出错情况下有此信息，表明详细的出错信息 
  "data": object // 选填;返回数据对象，请求处理成功时有效
  }
  
 ```

>  推送数据结构如下:

```

  {
  "op": "string", // 必填;Server 推送的操作类型，详细操作类型列表请参考附录
  "ts": long, // 必填;Server 推送时本地时间戳
  "data": object // 必填;返回数据对象
  }
  
```

## 服务方主动断开连接

在建连和鉴权期间，如果出错，服务方会主动断开连接，在关闭之前推送数据结构如下,

`{`

  `"op": "close", // 表明是服务⽅方主动断开连接`
   
  `"ts": long   // Server 推送时本地时间戳`
  
`}`


## 服务方返回错误，但不断开连接

鉴权成功后，在客户方提供非法Op或者某些内部错误的情况下，服务方会返回错误，但并不断开连接

`{`

  `"op": "error", // 表明是收到非法op或者内部错误 `
  
  `"ts": long// Server 推送时本地时间戳`
  
`}`

## 鉴权-Authentication

用户自⼰在火币网⽣成Access Key和Secret Key，Secret Key由用户自⼰保存，⽤户需提供Access Key。目前关于 apikey 申请和修改，请在“账户 - API 管理 ” 创建新API Key 填写备注(可选择绑定 ip)点击创建。其中 Access Key 为 API 访问密钥，Secret Key 为用户对请求进⾏签名的密钥(仅申请时可见)。用户按规则生成签名(Signature)。 

交易功能 websocket 版本接⼝建立连接时首先要做鉴权操作，具体格式如下，

重要提示：这两个密钥与账号安全紧密相关，无论何时都请勿向其它人透露。 

### 鉴权请求数据格式

`{`

  `"op": "auth",`
  
  `"type": "api",`
  
  `"AccessKeyId": "e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx",`
  
  `"SignatureMethod": "HmacSHA256",`
  
  `"SignatureVersion": "2",`
  
  `"Timestamp": "2017-05-11T15:19:30",`
  
  `"Signature": "4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o=",`
  
`}`


### 鉴权请求数据格式说明

| 字段名称         | 类型   | 说明                                                         |
| --------------- | ----- | ----------------------------------------------------------- |
| op               | string | 必填；操作名称，鉴权固定值为auth                             |
| type             | string | 必填；认证方式 api表示接口认证，ticket 表示终端认证          |
| cid              | string | 选填；Client请求唯一ID                                       |
| AccessKeyId      | string | type的值为api时必填；API 访问密钥, 您申请的 APIKEY 中的 AccessKey |
| SignatureMethod  | string | type的值为api时必填；签名方法, 用户计算签名的基于哈希的协议，此处使用 HmacSHA256 |
| SignatureVersion | string | type的值为api时必填；签名协议的版本，此处使用 2              |
| Timestamp        | string | type的值为api时必填；时间戳, 您发出请求的时间 (UTC 时区) 。在查询请求中包含此值有助于防止第三方截取您的请求。如:2017-05-11T16:22:06。再次强调是 (UTC 时区) |
| Signature        | string | type的值为api时必填；签名, 计算得出的值，用于确保签名有效和未被篡改 |
| ticket           | string | type的值为ticket时必填；登陆时返回                           |

#### 注意：

- 为了减少已有用户的接入工作量，此处使用了与REST接口同样的签名算法进行鉴权。

- 请注意大小写

- 当type为api时，参数op，type，cid，Signature不参加签名计算

- 此处签名计算中请求方法固定值为`GET`,其余值请参考REST接口签名算法文档

#### 步骤：

示例例参数签名(Signature)计算过程如下，

- 规范要计算签名的请求 因为使用 HMAC 进⾏签名计算时，使⽤不同内容计算得到的结果会完全
  不同。所以在进⾏签名计算前，请先对请求进⾏规范化处理。

- 请求方法(GET 或 POST)，后面添加换行符 `\n` 。

  `GET\n`

- 添加小写的访问地址，后面添加换行符`\n`。

  `api.hbdm.com\n`

- 访问方法的路径，后面添加换行符`\n`。

  `/linear-swap-notification\n`

- 按照ASCII码的顺序对参数名进行排序(使⽤ UTF-8 编码，且进⾏了 URI 编码，十六进制字符必须
  大写，如‘:’会被编码为'%3A'，空格被编码为'%20')。例如，下面是请求参数的原始顺序，进⾏过
  编码后。

  `AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30`
  

- 按照以上顺序，将各参数使用字符’&’连接。 
 
- 组成最终的要进行签名计算的字符串如下:
  
  计算签名，将以下两个参数传入加密哈希函数: 要进行签名计算的字符串，进行签名的密钥(SecretKey) 
  
  得到签名计算结果并进行 Base64编码
  
  将上述值作为参数Signature的取值添加到 API 请求中。 将此参数添加到请求时，必须将该值进⾏URI编码。

### 鉴权应答数据格式说明

| 名称     | 类型    | 说明                                                 |
| ------- | ------ | --------------------------------------------------- |
| op       | string  | 必填；操作名称，鉴权固定值为 auth                    |
| type     | string  | 必填；根据请求的参数进行返回。                       |
| cid      | string  | 选填；请求时携带则会返回。                           |
| err-code | int | 成功返回 0, 失败为其他值，详细响应码列列表请参考附录 |
| err-msg  | string  | 可选，若出错表示详细错误信息                         |
| ts       | long    | 服务端应答时间戳                                     |
| user-id  | long    | ⽤户 id                                              |

> 鉴权成功应答数据示例

```json
 
{
  "op": "auth",
  "type":"api",
  "ts": 1489474081631,
  "err-code": 0,
  "data": {
    "user-id": 12345678
  }
}

```

> 鉴权失败应答返回数据示例

```

{
"op": "auth",
"type":"api",
"ts": 1489474081631, 
"err-code": xxxx， 
"err-msg": ”详细的错误信息“
}

```

# WebSocket市场行情接口

## 【通用】订阅 KLine 数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

  `{`
  
  `"sub": "market.$contract_code.kline.$period",`
  
  `"id": "id generate by client"`
  
  `}`
  
> 正确订阅请求参数的例子：

```json

 {
    "sub": "market.BTC-USDT.kline.1min",
    "id": "id1"
 }
```

> 订阅成功返回数据的例子:

```json

  {
      "id": "id1",
      "status": "ok",
      "subbed": "market.BTC-USDT.kline.1min",
      "ts": 1489474081631
  }

```
### 请求参数
| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| sub | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.kline.$period，详细参数见sub订阅参数说明	 |  |
| id | false | string | 选填;Client 请求唯一 ID  |  |

### sub订阅参数说明

| 参数名称 | 是否必须   | 类型  | 描述 | 默认值 | 取值范围      |
| ------- | ----- | ------ |------ |------ |------ |
| contract_code  | true |  string   | 合约代码    |    | 支持大小写，比如:BTC-USDT    |
| period         | true | string   |  K线周期   |    |  仅支持小写：1min, 5min, 15min, 30min, 1hour,4hour,1day, 1mon  |


### 返回参数

 参数名称  |    是否必须   |   类型  |   描述   |
-------------- | -----------------  | ---------- |  -------------- |
  ch  |       true         |  string  |   请求参数   | 
  ts    |     true          | long   |  响应生成时间点，单位：毫秒     |           
 \<tick\>   |               |    |      |            | 
  id    |     true          | long   |  K线ID,也就是K线时间戳，K线起始时间    |            
  mrid    |     true          | long   |  订单ID     |            
  vol    |     true          | decimal   |  成交量张数。 值是买卖双边之和 |            
  count    |     true          | decimal   |   成交笔数。 值是买卖双边之和 |            
  open    |     true          | decimal   |  开盘价    |            
  close    |     true          | decimal   |  收盘价,当K线为最晚的一根时，是最新成交价     |            
  low    |     true          | decimal   |  最低价    |            
  high    |     true          | decimal   |  最高价    |            
  amount    |     true          | decimal   |  成交量(币), 即 sum(每一笔成交量(张)*单张合约面值/该笔成交价)。 值是买卖双边之和 |  
  trade_turnover   | true | decimal  | 成交额, 即sum（每一笔成交张数 * 合约面值 * 成交价格）。 值是买卖双边之和 |    |          
  \</tick\>    |               |     |      |          

> 之后每当 KLine 有更新时，client 会收到数据:

```json

{
    "ch":"market.BTC-USDT.kline.1min",
    "ts":1603707124366,
    "tick":{
        "id":1603707120,
        "mrid":131592424,
        "open":13067.7,
        "close":13067.7,
        "high":13067.7,
        "low":13067.7,
        "amount":0.004,
        "vol":4,
        "trade_turnover":52.2708,
        "count":1
    }
}

```

## 【通用】请求 KLine 数据 

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向Server发送如下格式的数据来请求数据：

  `{`
  
  `"req": "market.$contract_code.kline.$period",`
  
  `"id": "id generated by client",`
  
  `"from": " type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒",`
  
  `"to": "type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒，必须比 from 大"`
  
  `}`

> 请求 KLine 数据请求参数的例子：

```json

    {
    "req": "market.BTC-USDT.kline.1min",
    "id": "id4",
    "from": 1579247342,
    "to": 1579247342
    }

```
### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| req | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.kline.$period，详细参数见req请求参数说明	 |  |
| id | false | string | 选填;Client 请求唯一 ID  |  |
| from   | true | long  |  开始时间 | | 
| to     | true | long | 结束时间 | | 

### req请求参数说明

  参数名称  |    是否必须   |   类型  |   描述   |    默认值    |   取值范围
-------- | -------- | ------ | ------ | ------- |---------------------------------------- 
contract_code  |  true   |  string   |  合约代码   |           | 支持大小写，"BTC-USDT"  |
 period | true | string | K线周期 | | 1min, 5min, 15min, 30min, 60min,4hour,1day,1week, 1mon|

  
#### 备注

[t1, t5] 假设有 t1  ~ t5 的K线：

from: t1, to: t5, return [t1, t5].

from: t5, to: t1, which t5  > t1, return [].

from: t5, return [t5].

from: t3, return [t3, t5].

to: t5, return [t1, t5].

from: t which t3  < t  <t4, return [t4, t5].

to: t which t3  < t  <t4, return [t1, t3].

from: t1 and to: t2, should satisfy 1325347200  < t1  < t2  < 2524579200.

一次最多2000条。

> 之后每当 KLine 有更新时，client 会收到数据：

```json
    
{
    "id":"id4",
    "rep":"market.BTC-USDT.kline.60min",
    "wsid":467277265,
    "status":"ok",
    "data":[
        {
            "id":1603270800,
            "open":12198,
            "close":12196.7,
            "low":11715.8,
            "high":12300,
            "amount":0.276,
            "vol":276,
            "trade_turnover":3315.9104,
            "count":39
        },
        {
            "id":1603274400,
            "open":12196.7,
            "close":12277.9,
            "low":12111,
            "high":12289.9,
            "amount":0.198,
            "vol":198,
            "trade_turnover":2420.7728,
            "count":21
        }
    ]
}

```

### 返回参数  

  参数名称  |    是否必须   |   类型  |   描述   |
-------------- | -----------------  | ---------- |  -------------- |
  rep  |       true         |  string  |   请求参数   | 
  status  |       true         |  string  |   状态   | 
  id  |       true         |  string  |   请求id   | 
  wsid    |     true          | long   |  wsid     |           
 \<data\>    |               |    |      |            | 
  id    |     true          | long   | K线ID,也就是K线时间戳，K线起始时间 |            
  vol    |     true          | decimal   |  成交量张数。 值是买卖双边之和 |            
  count    |     true          | decimal   |  成交笔数。 值是买卖双边之和 |            
  open    |     true          | decimal   |    开盘价   |            
  close    |     true          | decimal   |  收盘价,当K线为最晚的一根时，是最新成交价     |            
  low    |     true          | decimal   |  最低价    |            
  high    |     true          | decimal   |  最高价    |            
  amount    |     true          | decimal   |  成交量(币), 即 sum(每一笔成交量(张)*单张合约面值/该笔成交价)。 值是买卖双边之和 |   
  trade_turnover   | true | decimal  | 成交额, 即sum（每一笔成交张数 * 合约面值 * 成交价格）。 值是买卖双边之和 |    |         
  \</data\>    |               |     |      |          

## 【通用】订阅 Market Depth 数据 

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

  `{`
  
  `"sub": "market.$contract_code.depth.$type",`
  
  `"id": "id generated by client"`
  
  `}`

> 正确订阅请求参数的例子：                                   

```json

    {                                          
    "sub": "market.BTC-USDT.depth.step0",       
    "id": "id5"                                
    } 
                                             
``` 
### 请求参数
| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| sub | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.depth.$type，详细参数见sub订阅参数说明	 |  |
| id | false | string | 选填;Client 请求唯一 ID  |  |

### sub订阅参数说明

  参数名称    |  是否必须    |  类型    |  描述      |   默认值    |  取值范围  |
-------------- |-------------- |---------- |------------ |------------ |---------------------------------------------------------------------------------|
 contract_code  |  true   |  string   |  合约代码   |           | 支持大小写，"BTC-USDT" ...  |
 type           |  true   | string     | Depth 类型        |        | (150档数据)  step0, step1, step2, step3, step4, step5, step14, step15（合并深度1-5,14-15）,step0时，不合并深度;(20档数据)  step6, step7, step8, step9, step10, step11, step12, step13（合并深度7-13）；step6时，不合并深度；step12（表示合并精度1的20档深度数据，表示整数位的个位）、step13（表示合并精度10的20档深度数据，表示整数位的十位）、step14（表示合并精度1的150档深度数据，表示整数位的个位）、step15（表示合并精度10的150档深度数据，表示整数位的十位） |

#### 备注

- 合并深度仅改变显示方式，不改变实际成交价格。

- step1至step5, step14, step15是进行了深度合并后的150档深度数据，step7至step13是进行了深度合并后的20档深度数据，对应精度如下：

| 档位 | Depth 类型 | 精度 |
|----|----|----|
|150档 |step0 | 不合并 |
|150档 |step1|0.00001|
|150档 |step2|0.0001|
|150档 |step3|0.001|
|150档 |step4|0.01|
|150档 |step5|0.1|
|150档 |step14|1|
|150档 |step15|10|
|20档 |step6 | 不合并 |
|20档 |step7|0.00001|
|20档 |step8|0.0001|
|20档 |step9|0.001|
|20档 |step10|0.01|
|20档 |step11|0.1|
|20档 |step12|1|
|20档 |step13|10|

> 之后每当 depth 有更新时，client 会收到数据，例子：

```json
 
{
    "ch":"market.BTC-USDT.depth.step6",
    "ts":1603707576468,
    "tick":{
        "mrid":131596447,
        "id":1603707576,
        "bids":[
            [
                13071.9,
                38
            ],
            [
                13068,
                5
            ]
        ],
        "asks":[
            [
                13081.9,
                197
            ],
            [
                13099.7,
                371
            ]
        ],
        "ts":1603707576467,
        "version":1603707576,
        "ch":"market.BTC-USDT.depth.step6"
    }
}
    
```

### 返回参数
 
参数名称   |   是否必须  |   数据类型   |   描述   |   取值范围   |
-------- | -------- | -------- |  --------------------------------------- | -------------- | 
ch | true |  string | 数据所属的 channel，格式： market.period | | 
ts | true | long | 数据进入行情服务器时间戳，单位：毫秒 | |
\<tick\>   |               |    |      |            | 
mrid  | true| long | 订单ID | 
id  | true| long | tick ID | 
asks | true | object |卖盘,[price(挂单价), vol(此价格挂单张数)], 按price升序 | | 
bids | true| object | 买盘,[price(挂单价), vol(此价格挂单张数)], 按price降序 | | 
ts | true | long | 深度生成时间戳，每100MS生成一次，单位：毫秒 | |
version | true | long | 版本号 | |
ch | true |  string | 数据所属的 channel，格式： market.period | | 
 \</tick\>    |               |    |      |            | | 

## 【通用】订阅Market Depth增量数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来请求数据:

`{`

     `"sub": "market.$contract_code.depth.size_${size}.high_freq",`

     `"data_type":"incremental",`

     `"id": "id generated by client"`

`}`

> 正确订阅请求参数的例子： 

```json

{
  "sub": "market.BTC-USDT.depth.size_20.high_freq",
  "data_type":"incremental",
  "id": "id generated by client"
}
```

### 请求参数
| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| sub | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.depth.size_${size}.high_freq，详细参数见sub订阅参数说明	 | 
| id | false | string | 选填;Client 请求唯一 ID  |  |
| data_type   |  false   |  string     |  Depth 类型     |  不填默认为全量数据，"incremental"：增量数据，"snapshot"：全量数据 |  

### sub订阅参数说明
  参数名称   |  是否必须    |  类型     |  描述      |  默认值     |  取值范围  |
  -------------- |   -------------- |  ---------- |  ------------ |  ------------ |  --  |
 contract_code         |  true           |  string     |  交易对            |        |  合约代码，支持大小写，比如"BTC-USDT"   |
  size           |  true           |  string     |   档位数       |        |  20:表示20档不合并的深度，150:表示150档不合并的深度  |

  
> response：

```json
{
    "ch":"market.BTC-USDT.depth.size_20.high_freq",
    "tick":{
        "asks":[
            [
                13081.9,
                206
            ],
            [
                13099.7,
                371
            ]
        ],
        "bids":[
            [
                13071.9,
                38
            ],
            [
                13060,
                400
            ]
        ],
        "ch":"market.BTC-USDT.depth.size_20.high_freq",
        "event":"snapshot",
        "id":131597620,
        "mrid":131597620,
        "ts":1603707712356,
        "version":1512467
    },
    "ts":1603707712357
}
```

### 返回参数

参数名称   |   是否必须  |   数据类型   |   描述   |   取值范围   |
-------- | -------- | -------- |  --------------------------------------- | -------------- | 
ch | true |  string | 数据所属的 channel，格式： market.$contract_code.depth.size_${size}.high_freq | | 
ts | true | long | 进入行情服务器系统时间点，单位：毫秒 | |
 \<tick\>    |               |    |      |            | 
mrid  | true| long | 订单ID | 
id  | true| long | tick ID | 
asks | true | object |卖盘,[price(挂单价), vol(此价格挂单张数)], 按price升序 | | 
bids | true| object | 买盘,[price(挂单价), vol(此价格挂单张数)], 按price降序 | | 
ts | true | long | 系统检测orderbook时间点，单位：毫秒 | |
version | true | long | 版本号 | |
ch | true |  string | 数据所属的 channel，格式： market.$symbol.depth.size_${size}.high_freq | | 
event | true |  string | 事件类型；"update":更新，表示推送买卖各20档或150档不合并深度的增量数据；"snapshot":快照值，表示推送买卖各20档或150档不合并深度的全量数据 | | 
 \</tick\>    |               |    |      |            | | 

### 备注

1、当"data_type"为incremental时，首次推送的"event"为"snapshot"的数据，且当重新发送订阅请求时，首次返回都是"snapshot"的数据；

2、深度即可以按照合约周期订阅，也可以按照合约代码订阅，行情系统在进行数据计算时，需要更新对应类型的数据；

3、version（版本号），是自增的序号，每次增加1，不管是增量还是全量数据,每个连接是唯一的。多个websocket连接的version是可能不同的。

4、每30ms检查一次orderbook，如果有更新，则推送，如果没有更新，则不推送。

5、如果是增量数据，要自己维护好本地的orderbook bids\asks 数据。

## 【通用】订阅 Market Detail 数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来请求数据:

  `{ `
  
  ` "sub": "market.$contract_code.detail", `
  
  ` "id": "id generated by client" `
  
  `} `

> 订阅 Market Detail 数据请求参数的例子：

```json
                                      
 {                                    
  "sub": "market.BTC-USDT.detail",     
  "id": "id6"                         
 }                                    

```

### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| sub | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.detail，详细参数见sub订阅参数说明	 | 
| id | false | string | 选填;Client 请求唯一 ID  |  |

### sub订阅参数说明

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| contract_code   |  true           |  string     |  交易对            |   合约代码，支持大小写，比如"BTC-USDT"   |
   

> 请求成功返回数据的例子：

```json

{
    "ch":"market.BTC-USDT.detail",
    "ts":1603707870528,
    "tick":{
        "id":1603707840,
        "mrid":131599205,
        "open":12916.2,
        "close":13065.8,
        "high":13205.3,
        "low":12852.8,
        "amount":30.316,
        "vol":30316,
        "trade_turnover":395073.4918,
        "count":2983,
        "asks":[
            13081.9,
            206
        ],
        "bids":[
            13071.9,
            38
        ]
    }
}
  
```
### 返回参数

参数名称     |  是否必须    |   数据类型     |  描述  |
-------------- |  -------------- |  -------------- |  ----------------------------------------------------------  |
ch  |  true  |  string  |    数据所属的 channel，格式： market.$contract_code.detail   |     
ts  |  true  |  long  |    响应生成时间点，单位：毫秒  |    
\<tick\>   |               |    |      |           
id  |  true  |  long  |    ID  |    
mrid  |  true  |  long  |    订单ID  |    
open  |  true  |  decimal  |    开盘价  |     
close  |  true  |  decimal  |    收盘价,当K线为最晚的一根时，是最新成交价  |    
high  |  true  |  decimal  |    最高价  |     
low  |  true  |  decimal  |    最低价  |     
amount  |  true  |  decimal  |    成交量(币), 即 sum(每一笔成交量(张)*单张合约面值/该笔成交价)。 值是买卖双边之和 |   
vol  |  true  |  decimal  |   成交量（张）。 值是买卖双边之和  |     
trade_turnover   | true | decimal  | 成交额，即sum（每一笔成交张数 * 合约面值 * 成交价格）。 值是买卖双边之和 |  |
count  |  true  |  decimal  |   成交笔数  |     
ask  |  true  |  array  |   [卖1价,卖1量(张)]  |     
bid  |  true  |  array  |   [买1价,买1量(张)]	  |     
 \</tick\>    |               |    |      |  

#### 备注
 - 买一卖一并非实时更新，会存在部分延迟（500ms左右）。


## 【通用】订阅买一卖一逐笔行情推送

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来请求数据：

  `{`
  
  `"req": "market.$contract_code.bbo", `
  
  `"id": "id generated by client" `
  
  `}`

> 正确请求参数的例子：

```json

    {
     "sub": "market.BTC-USDT.bbo",
     "id": "id8"
    }

```

### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| sub | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.bbo，详细参数见sub订阅参数说明	 | 
| id | false | string | 选填;Client 请求唯一 ID  |  |

### sub请求参数说明

| 字段名称 | 是否必须| 类型   | 描述  | 默认值  |
| ------- | ----- | ----- | ------- | ------- |
| contract_code   |  true    |  string     |    交易对         |  合约代码，支持大小写，比如"BTC-USDT"   |

> **返回示例**:

```json

{
    "ch":"market.BTC-USDT.bbo",
    "ts":1603707934525,
    "tick":{
        "mrid":131599726,
        "id":1603707934,
        "bid":[
            13064,
            38
        ],
        "ask":[
            13072.3,
            205
        ],
        "ts":1603707934525,
        "version":131599726,
        "ch":"market.BTC-USDT.bbo"
    }
}
```

### **返回参数说明**：

| 参数名称   |   是否必须  |   数据类型   |   描述   |   取值范围   |
| -------- | -------- | -------- |  --------------------------------------- | -------------- |
| ch | true |  string | 数据所属的 channel，格式： market.$contract_code.bbo | |
| ts | true | long | 响应生成时间点，单位：毫秒（指接口响应时间） | |
| \<tick\> | true | object |  | |
| ch | true |  string | 数据所属的 channel，格式： market.$contract_code.bbo | |
| mrid  | true| string | 订单ID | |
| id  | true| long | tick ID | |
| ask | true | array |卖一盘,[price(挂单价), vol(此价格挂单张数)] | |
| bid | true| array | 买一盘,[price(挂单价), vol(此价格挂单张数)] | |
| version | true| long | 版本号 | |
| ts | true | long | 响应生成时间点，单位：毫秒（指数据生成时间）| |
| \<\tick\> | | |  | |

- **说明**：
- 当买一价、买一量、卖一价、卖一量，其中任一数据发生变化时，进行逐笔推送；
- 如果同一时刻有多个买一卖一的价格/单量的变化，直接用最新的买一卖一进行推送，直接丢弃中间结果；
- 由于客户端网络等原因导致接收数据失败，服务端会丢弃旧的队列数据；
- version（版本号），直接取撮合id，保证全局唯一并且最新的推送版本号都是数值最大的。

## 【通用】请求 Trade Detail 数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来请求数据：

  `{`
  
  `"req": "market.$contract_code.trade.detail", `
  
  `"id": "id generated by client" `
  
  `}`



仅返回当前 Trade Detail

> 请求 Trade Detail 数据请求参数的例子：

```json

    {
     "req": "market.BTC-USDT.trade.detail",
     "size": 50 ,
     "id": "id8"
    }

```
### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值  |
| ------ | ------ | ------ | ------ | ------ |
| req | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.trade.detail，详细参数见req请求参数说明	 | 
| id | false | string | 选填;Client 请求唯一 ID  |  |
| size   | false | int | 数据条数，最多50，不填默认50                      | [1,50]  |

### req请求参数说明

| 字段名称 | 是否必须| 类型   | 描述  | 默认值  |
| ------- | ----- | ----- | ------- | ------- |
| contract_code   |  true    |  string     |  交易对            |   合约代码，支持大小写，比如"BTC-USDT" .  |

> 请求成功返回数据的例子：

```json

{
    "data":[
        {
            "amount":"22",
            "ts":1603706942240,
            "id":1315909380000,
            "price":"13068.4",
            "direction":"sell"
        },
        {
            "amount":"2",
            "ts":1603706947767,
            "id":1315909430000,
            "price":"13068.5",
            "direction":"buy"
        }
    ],
    "id":"id8",
    "rep":"market.BTC-USDT.trade.detail",
    "status":"ok",
    "ts":1603708046534
}
```

### 返回参数

参数名称     |  是否必须   |  类型   |  描述  |  默认值   | 
--------------  | --------------  | ----------  | ---------------------------------------------------------  | ------------ | 
rep  |  true  |  string  |  数据所属的 channel，格式： market.$contract_code.trade.detail  |  |   
status  |  true  |  string  |  返回状态  |  |   
id  |  true  |  long  |  请求唯一 ID  |   |    
\<data\>    |               |    |      | 
id  |  true  |  long  |  成交唯一id（品种唯一）  |   |    
price  |  true  |  string  |  价格  |   |    
amount  |  true  |  string  |  数量（张）。 值是买卖双边之和 |   |    
direction  |  true  |  string  |  买卖方向  |   |    
ts  |  true  |  long  |  订单成交时间  |   |    
\</data\>    |               |    |      | 
ts  |  true  |  long  |  发送时间  |   |  

## 【通用】订阅 Trade Detail 数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

  `{`  
  
  `"sub": "market.$contract_code.trade.detail",`
  
  `"id": "id generated by client"`
  
  `}`


> 正确订阅请求参数的例子：

```json

    {
     "sub": "market.BTC-USDT.trade.detail",
     "id": "id7"
    }

```

### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| sub | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.trade.detail，详细参数见sub订阅参数说明	 | 
| id | false | string | 选填;Client 请求唯一 ID  |  |

### sub订阅参数说明

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| contract_code   |  true           |  string     |  交易对            |   合约代码，支持大小写，比如"BTC-USDT"   |


> 之后每当 Trade Detail 有更新时，client 会收到数据，例子：

```json

{
    "ch":"market.BTC-USDT.trade.detail",
    "ts":1603708208346,
    "tick":{
        "id":131602265,
        "ts":1603708208335,
        "data":[
            {
                "amount":2,
                "ts":1603708208335,
                "id":1316022650000,
                "price":13073.3,
                "direction":"buy"
            }
        ]
    }
}

```

### 返回参数

参数名称     |  是否必须   |  类型   |  描述  |  默认值   | 
--------------  | --------------  | ----------  | ---------------------------------------------------------  | ------------ | 
ch  |  true  |  string  |  数据所属的 channel，格式： market.$contract_code.trade.detail  |  |   
ts  |  true  |  long  |  发送时间  |   |    
\<tick\>   |               |    |      | 
id  |  true  |  long  |  订单唯一id（品种唯一）  |   |    
ts  |  true  |  long  |  tick数据戳  |   |    
\<data\>    |               |    |      | 
amount  |  true  |  decimal  |  数量（张）。 值是买卖双边之和 |   |    
ts  |  true  |  long  |  订单时间戳  |   |    
id  |  true  |  long  |   成交唯一id（品种唯一）  |   |    
price  |  true  |  decimal  |  价格  |   |    
direction  |  true  |  string  |  买卖方向  |   |    
 \</data\>    |               |    |      | 
 \</tick\>    |               |    |      | 



# WebSocket指数与基差数据接口

- 指数与基差数据订阅ws地址：wss://api.hbdm.com/ws_index

## 【通用】订阅(sub)指数K线数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

`{`

  `"sub": "market.$contract_code.index.$period",`

  `"id": "id generate by client"`

`}`

> 正确订阅请求参数的例子：

```json

    {
    "sub": "market.BTC-USDT.index.1min",
    "id": "id1"
    }

```
### 请求参数
  参数名称  |   是否必须   |   类型    |   描述   |    默认值  |  
--------------| -----------------| ---------- |----------| ------------  | 
  sub  |       true         |  string  |  需要订阅的主题，该接口固定为：market.$contract_code.index.$period，详细参数见sub订阅参数说明    |               |  
  id   |     false          | string   |  业务方自主生成的id      |           |  

### sub订单参数说明
| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 指数标识          |         | 支持大小写，"BTC-USDT","ETH-USDT"...                           |
| period          | true     | string  | K线类型               |         | 仅支持小写,1min, 5min, 15min, 30min, 60min,4hour,1day, 1mon     |


### 备注
  - 当指数有变化时会推送;
  
  - 指数无变化时会根据订阅的周期推送；


> 之后每当 KLine 有更新时，client 会收到数据

```json

{
    "ch":"market.BTC-USDT.index.15min",
    "ts":1607309592214,
    "tick":{
        "id":1607309100,
        "open":"19213.505",
        "close":"19242.05",
        "high":"19248.31",
        "low":"19213.505",
        "amount":"0",
        "vol":"0",
        "count":0
    }
}
```
### 返回参数
| **参数名称**    | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| -----------  | ------ | ------------- | ------- | ---------------------------------------- |
| ch      | string | 数据所属的 channel，格式： market.$contract_code.index.$period |                | |
| ts      | long | 响应生成时间点，单位：毫秒                   |                | |
| tick      | object array | tick返回，详情：推送tick参数                  |                | |

### 推送tick参数
| **参数名称** | **类型** | **描述**        |                                  |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| id | string | 指数K线id,也就是K线时间戳，K线起始时间  |
| vol | string  | 成交量张数为0             |
| count | decimal  | 成交笔数为0              |
| open | string  | 开盘指数价               |
| close | string  | 收盘指数价              |
| low | string  |  最低指数价             |
| high | string  | 最高指数价               |
| amount | string  | 数值为0              |

## 【通用】请求(req)指数K线数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来请求数据：

`{`
     
   `"req": "market.$contract_code.index.$period",`
    
   `"id": "id generated by client",`

   `"from": "type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒",`
   
   `"to": "type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒，必须比 from 大",`
    
`}`

> 正确订阅请求参数的例子:

```json

    {
    "req": "market.btc-usdt.index.1min",
    "id": "id4",
    "from":1571000000,
    "to":1573098606
    }
```

### 请求参数

  参数名称  |   是否必须   |   类型    |   描述   |    默认值  |  
--------------| -----------------| ---------- |----------| ------------  | 
  req  |       true         |  string  |  需要订阅的主题，该接口固定为：market.$contract_code.index.$period，详细参数见req请求参数说明    |               |  
  id   |     false          | string   |  业务方自主生成的id      |           |  
  from     | true     | long  | 开始时间,2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒               |         |  
  to       | true     | long  | 结束时间, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒，必须比 from 大              |         | 

### req请求参数说明：
| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 指数标识          |         |支持大小写, "BTC-USDT","ETH-USDT"...                           |
| period          | true     | string  | K线类型               |         | 1min, 5min, 15min, 30min, 60min,4hour,1day, 1mon     |


### 说明：
- 一次返回最多2000条数据；

> 请求成功返回数据的例子：

```json

{
    "id":"id4",
    "rep":"market.BTC-USDT.index.15min",
    "wsid":3673570133,
    "ts":1607310136031,
    "status":"ok",
    "data":[
        {
            "id":1607309100,
            "open":19213.505,
            "close":19207.245,
            "low":19207.245,
            "high":19248.31,
            "amount":0,
            "vol":0,
            "count":0
        },
        {
            "id":1607310000,
            "open":19199.655,
            "close":19174.48,
            "low":19174.48,
            "high":19208.11,
            "amount":0,
            "vol":0,
            "count":0
        }
    ]
}
```

### 返回参数
| **参数名称**    | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| -----------  | ------ | ------------- | ------- | ---------------------------------------- |
| req     | true | string | 数据所属的 channel，格式：market.$contract_code.index.$period  |                | |
| status | true | string | 请求处理结果                          | "ok" , "error" | |
| id     | true | string | 业务方id       |                | |
| wsid     | true | long | wsid           |                | |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | |
| tick    |    object array    |  tick返回，详情：推送tick参数         |                | |

### 推送tick参数
| **参数名称** | **类型** | **描述**        |                                  |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| id | decimal | 指数K线id,也就是K线时间戳，K线起始时间  |
| vol | decimal  | 成交量张数为0             |
| count | decimal  | 成交笔数为0              |
| open | decimal  | 开盘指数价               |
| close | decimal  | 收盘指数价              |
| low | decimal  |  最低指数价             |
| high | decimal  | 最高指数价               |
| amount | decimal  | 数值为0              |

## 【通用】订阅溢价指数K线数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

  `{`  
  
  `"sub": "market.$contract_code.premium_index.$period",`
  
  `"id": "id generated by client"`
  
  `}`

> 正确订阅请求参数的例子：

```json

    {
     "sub": "market.BTC-USDT.premium_index.1min",
     "id": "id7"
    }

```
### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| sub | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.premium_index.$period，详细参数见sub订阅参数说明	 | 
| id | false | string | 选填;Client 请求唯一 ID  |  |

### sub订阅参数说明

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约代码         |         | "BTC-USDT","ETH-USDT"...                           |
| period          | true     | string  | K线类型               |         | 1min, 5min, 15min, 30min, 60min,4hour,1day, 1week, 1mon     |

> 之后每当溢价指数有更新时，client 会收到数据，例子：

```json

{
    "ch":"market.BTC-USDT.premium_index.1min",
    "ts":1603708380380,
    "tick":{
        "id":1603708380,
        "open":"0.000068125",
        "close":"0.000068125",
        "high":"0.000068125",
        "low":"0.000068125",
        "amount":"0",
        "vol":"0",
        "count":"0",
        "trade_turnover":"0"
    }
}

```

### 返回参数

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| ch     | true | string | 数据所属的 channel，格式： market.period |                | |
| \<tick\> |   true   |    object array    |               |                | |
| id     | true | long | 指数K线ID,也就是K线时间戳，K线起始时间        |                | |
| vol     | true | string | 成交量(张)，数值为0        |                | |
| count     | true | string | 成交笔数，数值为0        |                | |
| open     | true | string | 开盘值（溢价指数）        |                | |
| close     | true | string | 收盘值（溢价指数）       |                | |
| low     | true | string | 最低值（溢价指数）        |                | |
| high     | true | string | 最高值 （溢价指数）       |                | |
| amount     | true | string | 成交量(币), 数值为0        |                | |
| trade_turnover     | true | string | 成交额， 数值为0        |                | |
| \</tick\>            |      |        |               |                | |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | |

## 【通用】请求溢价指数K线数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来请求数据：

  `{`
  
  `"req": "market.$contract_code.premium_index.$period",`
  
  `"id": "id generated by client",`
  
  `"from": " type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒",`
  
   `"to": "type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒，必须比 from 大"`
  
  `} `

> 数据请求参数的例子：

```json

    {
    "req": "market.BTC-USDT.premium_index.1min",
    "id": "id4",
    "from":1571000000,
    "to":1573098606
    }
```
### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| req | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.premium_index.$period，详细参数见req请求参数说明	 | 
| id | false | string | 选填;Client 请求唯一 ID  |  |
| from          | true     | long  | 开始时间（时间戳，单位秒）          |         |    
| to          | true     | long  | 结束时间 （时间戳，单位秒）           |         |    

### req请求参数说明

|  参数名称   |  是否必须  |  类型  |    描述        |   默认值  |  取值范围                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约代码         |         | "BTC-USDT","ETH-USDT"...                           |
| period          | true     | string  | K线类型               |         | 1min, 5min, 15min, 30min, 60min,4hour,1day, 1week, 1mon     |


#### 备注：

- 一次返回最多2000条数据；

- from和to都为必填。

> 请求成功返回数据的例子：

```json

{
    "id":"id4",
    "rep":"market.BTC-USDT.premium_index.15min",
    "wsid":1524762738,
    "ts":1603782744066,
    "status":"ok",
    "data":[
        {
            "id":1603641600,
            "open":"0",
            "close":"0.0000970833333333",
            "low":"0",
            "high":"0.0000997916666666",
            "amount":"0",
            "vol":"0",
            "count":"0",
            "trade_turnover":"0"
        }
    ]
}

```

### 返回参数

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| rep     | true | string | 数据所属的 channel，格式： market.period |                | |
| status | true | string | 请求处理结果                          | "ok" , "error" | |
| id     | true | string | 业务方id       |                | |
| wsid     | true | long | wsid           |                | |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | |
| \<data\> |   true   |    object array    |               |                | |
| id     | true | long | 指数K线ID,也就是K线时间戳，K线起始时间        |                | |
| vol     | true | string | 成交量(张)，数值为0        |                | |
| count     | true | string | 成交笔数，数值为0        |                | |
| open     | true | string | 开盘值（溢价指数）        |                | |
| close     | true | string | 收盘值（溢价指数）      |                | |
| low     | true | string | 最低值 （溢价指数）       |                | |
| high     | true | string | 最高值  （溢价指数）      |                | |
| amount     | true | string | 成交量(币), 数值为0        |                | |
| trade_turnover     | true | string | 成交额, 数值为0        |                | |
| \</data\>            |      |        |               |                | |

## 【通用】订阅预测资金费率K线数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

  `{`  
  
  `"sub": "market.$contract_code.estimated_rate.$period",`
  
  `"id": "id generated by client"`
  
  `}`

> 正确订阅请求参数的例子：

```json

    {
     "sub": "market.btc-usdt.estimated_rate.1min",
     "id": "id7"
    }

```

### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| sub | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.estimated_rate.$period，详细参数见sub订阅参数说明	 | 
| id | false | string | 选填;Client 请求唯一 ID  |  |

### sub订阅参数说明

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约代码         |         | "BTC-USDT","ETH-USDT"...                           |
| period          | true     | string  | K线类型           |         | 1min, 5min, 15min, 30min, 60min,4hour,1day, 1week, 1mon     |

> 之后每当预测资金费率有更新时，client 会收到数据，例子：

```json

{
    "ch":"market.BTC-USDT.estimated_rate.1min",
    "ts":1603708560233,
    "tick":{
        "id":1603708560,
        "open":"0.0001",
        "close":"0.0001",
        "high":"0.0001",
        "low":"0.0001",
        "amount":"0",
        "vol":"0",
        "count":"0",
        "trade_turnover":"0"
    }
}

```

### 返回参数

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| ch     | true | string | 数据所属的 channel，格式： market.period |                | |
| \<tick\> |   true   |    object array    |               |                | |
| id     | true | long | k线id        |                | |
| vol     | true | string | 成交量(张)，数值为0        |                | |
| count     | true | string | 成交笔数，数值为0        |                | |
| open     | true | string | 开盘值 （预测资金费率）       |                | |
| close     | true | string | 收盘值 （预测资金费率）      |                | |
| low     | true | string | 最低值 （预测资金费率）       |                | |
| high     | true | string | 最高值  （预测资金费率）      |                | |
| amount     | true | string | 成交量(币), 数值为0        |                | |
| trade_turnover     | true | string | 成交额 数值为0        |                | |
| \</tick\>            |      |        |               |                | |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | |

## 【通用】请求预测资金费率K线数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来请求数据：

  `{`
  
  `"req": "market.$contract_code.estimated_rate.$period",`
  
  `"id": "id generated by client",`
  
  `"from": " type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒",`
  
   `"to": "type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒，必须比 from 大"`
  
  `} `

> 数据请求参数的例子：

```json

    {
    "req": "market.BTC-USDT.estimated_rate.1min",
    "id": "id4",
    "from": 1579247342,
    "to": 1579247342
    }

```
### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| req | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.estimated_rate.$period，详细参数见req请求参数说明	 |  |
| id | false | string | 选填;Client 请求唯一 ID  |  |
| from          | true     | long  | 开始时间（时间戳，单位秒）          |         |    |
| to          | true     | long  | 结束时间 （时间戳，单位秒）           |         |    |

### req请求参数说明

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约代码         |         | "BTC-USDT","ETH-USDT"...                           |
| period          | true     | string  | K线类型               |         | 1min, 5min, 15min, 30min, 60min,4hour,1day, 1week, 1mon     |


#### 备注：

- 一次返回最多2000条数据；

- from和to都为必填。

> 请求成功返回数据的例子：

```json

{
    "id":"id4",
    "rep":"market.BTC-USDT.estimated_rate.15min",
    "wsid":3674722864,
    "ts":1603782867314,
    "status":"ok",
    "data":[
        {
            "id":1603641600,
            "open":"0.0001",
            "close":"0.0001",
            "low":"0.0001",
            "high":"0.0001",
            "amount":"0",
            "vol":"0",
            "count":"0",
            "trade_turnover":"0"
        }
    ]
}

```

### 返回参数

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| rep     | true | string | 数据所属的 channel，格式： market.period |                | |
| status | true | string | 请求处理结果                          | "ok" , "error" | |
| id     | true | string | 业务方id       |                | |
| wsid     | true | long | wsid           |                | |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | |
| \<data\> |   true   |    object array    |               |                | |
| id     | true | long | k线id        |                | |
| vol     | true | string | 成交量(张)，数值为0        |                | |
| count     | true | string | 成交笔数，数值为0        |                | |
| open     | true | string | 开盘值（预测资金费率）        |                | |
| close     | true | string | 收盘值（预测资金费率）       |                | |
| low     | true | string | 最低值（预测资金费率）        |                | |
| high     | true | string | 最高值 （预测资金费率）       |                | |
| amount     | true | string | 成交量(币), 数值为0        |                | |
| trade_turnover     | true | string | 成交额 数值为0        |                | |
| \</data\>            |      |        |               |                | |

## 【通用】订阅基差数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

  `{`  
  
  `"sub": "market.$contract_code.basis.$period.$basis_price_type",`
  
  `"id": "id generated by client"`
  
  `}`

> 正确订阅请求参数的例子：

```json

    {
     "sub": "market.BTC-USDT.basis.1min.open",
     "id": "id7"
    }

```

### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| sub | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.basis.$period.$basis_price_type，详细参数见sub订阅参数说明	 | 
| id | false | string | 选填;Client 请求唯一 ID  |  |

### sub订阅参数说明

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约名称          |         | 如"BTC-USDT"                          |
| period          | true     | string  | 周期               |         | 1min, 5min, 15min, 30min, 60min,4hour,1day,1week, 1mon     |
| basis_price_type     | false     | string  | 基差价格类型，表示在周期内计算基差使用的价格类型              |    不填，默认为使用开盘价     |    开盘价：open，收盘价：close，最高价：high，最低价：low，平均价=（最高价+最低价）/2：average   |

> 之后每当预测资金费率有更新时，client 会收到数据，例子：

```json

{
    "ch":"market.BTC-USD.basis.15min.open",
    "ts":1603709195504,
    "tick":{
        "id":1603709100,
        "index_price":"13101.595",
        "contract_price":"13100.9",
        "basis":"-0.695",
        "basis_rate":"-0.0000530469763414301846454572897422031"
    }
}
```

### 返回参数

| **参数名称**    | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| -----------  | ------ | ------------- | ------- | ---------------------------------------- |
| ch      | string | 数据所属的 channel，格式： market.period |                | |
| \<tick\>    |    object array    |               |                | |
| id  | long | 唯一标识 |  |
| contract_price  | string | 合约最新成交价 |  |
| index_price  | string | 指数基准价，与基差价格类型匹配 |  |
| basis  | string | 基差=合约基准价 - 指数基准价 |  |
| basis_rate | string | 基差率=基差/指数基准价 |  |
| \</tick\>            |      |        |               |                | |
| ts      | long | 响应生成时间点，单位：毫秒                   |                | |

## 【通用】请求基差数据

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来请求数据：

  `{`
  
  `"req": "market.$contract_code.basis.$period.$basis_price_type",`
  
  `"id": "id generated by client",`
  
  `"from": " type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒",`
  
   `"to": "type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒，必须比 from 大"`
  
  `} `

> 数据请求参数的例子：

```json

    {
    "req": "market.btc-usdt.basis.1min.open",
    "id": "id4",
    "from": 1579247342,
    "to": 1579247342
    }

```
### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| req | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.basis.$period.$basis_price_type，详细参数见req请求参数说明	 |  |
| id | false | string | 选填;Client 请求唯一 ID  |  |
| from          | true     | long  | 开始时间（时间戳，单位秒）          |         |    
| to          | true     | long  | 结束时间 （时间戳，单位秒）           |         |    

### req请求参数说明

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约名称          |         | 如"BTC-USDT"                          |
| period          | true     | string  | 周期               |         | 1min, 5min, 15min, 30min, 60min,4hour,1day,1week, 1mon     |
| basis_price_type     | false     | string  | 基差价格类型，表示在周期内计算基差使用的价格类型              |    不填，默认为使用开盘价     |    开盘价：open，收盘价：close，最高价：high，最低价：low，平均价=（最高价+最低价）/2：average   |


> 请求成功返回数据的例子：

```json

{
    "data":[
        {
            "basis":"-27.593412766666006",
            "basis_rate":"-0.0021317871729511838",
            "contract_price":"12916.2",
            "id":1603641600,
            "index_price":"12943.793412766667"
        }
    ],
    "id":"id4",
    "rep":"market.BTC-USDT.basis.15min.open",
    "status":"ok",
    "ts":1603783024207,
    "wsid":1308653018
}

```

### 返回参数

| **参数名称**    | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| -----------  | ------ | ------------- | ------- | ---------------------------------------- |
| rep     | true | string | 数据所属的 channel，格式： market.basis |                | |
| status | true | string | 请求处理结果                          | "ok" , "error" | |
| id     | true | string | 业务方id       |                | |
| wsid     | true | long | wsid           |                | |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | |
| \<data\>    |    object array    |               |                | |
| id | true  | long | 唯一标识 |  |
| contract_price | true  | string | 合约最新成交价 |  |
| index_price | true  | string | 指数基准价，与基差价格类型匹配 |  |
| basis | true  | string | 基差=合约基准价 - 指数基准价 |  |
| basis_rate | true | string | 基差率=基差/指数基准价 |  |
| \</data\>            |      |        |               |                | |



## 【通用】订阅标记价格K线数据

#### 备注：
 - 该接口支持全仓模式和逐仓模式。

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

  `{`
  
  `"sub": "market.$contract_code.mark_price.$period",`
  
  `"id": "id generate by client"`
  
  `}`
  
> 正确订阅请求参数的例子：

```json

 {
    "sub": "market.$contract_code.mark_price.$period",
    "id": "id1"
 }
```

### 请求参数
| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| sub | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.mark_price.$period，详细参数见sub订阅参数说明	 |  |
| id | false | string | 选填;Client 请求唯一 ID  |  |

### sub订阅参数说明
| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约代码         |         | "BTC-USDT","ETH-USDT"...                          |
| period          | true     | string  | K线类型               |         | 1min, 5min, 15min, 30min, 60min,4hour,1day, 1week, 1mon     |

> 当标记价格有更新时，client 会收到数据，例如：

```json

{
 "ch": "market.BTC-USDT.mark_price.1min",
 "ts": 1489474082831,
 "tick": 
    {
      "vol": "0",
      "close": "9800.12",
      "count": "0",
      "high": "9800.12",
      "id": 1529898780,
      "low": "9800.12",
      "open": "9800.12",
      "trade_turnover": "0",
      "amount": "0"
    }
}

```

### 返回参数
| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| ch     | true | string | 数据所属的 channel，格式： market.period |                | |
| \<tick\> |   true   |    object array    |               |                | |
| id     | true | long | k线id        |                | |
| vol     | true | string | 成交量(张)，数值为0        |                | |
| count     | true | string | 成交笔数，数值为0        |                | |
| open     | true | string | 开盘值        |                | |
| close     | true | string | 收盘值       |                | |
| low     | true | string | 最低值        |                | |
| high     | true | string | 最高值       |                | |
| amount     | true | string | 成交量(币), 数值为0        |                | |
| trade_turnover     | true | string | 成交额, 数值为0        |                | |
| \</tick\>            |      |        |               |                | |
| status | true | string | 请求处理结果                          | "ok" , "error" | |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | |


## 【通用】请求标记价格K线数据

#### 备注：
 - 该接口支持全仓模式和逐仓模式。

### 成功建立和 WebSocket API 的连接之后，向Server发送如下格式的数据来请求数据：

  `{`
  
  `"req": "market.$contract_code.mark_price.$period",`
  
  `"id": "id generated by client",`
  
  `"from": " type: long, 单位：秒",`
  
  `"to": "type: long,单位：秒，必须比 from 大"`
  
  `}`

> 请求参数的例子：

```json

    {
    "req": "market.BTC-USDT.mark_price.5min",
    "id": "id4",
    "from": 1579247342,
    "to": 1579247342
    }

```
### 请求参数

| 参数名称 | 是否必须   | 类型 | 描述  | 默认值
| ------ | ------ | ------ | ------ | ------ |
| req | true | string | 需要订阅的主题，该接口固定为：market.$contract_code.mark_price.$period，详细参数见req请求参数说明	 |  |
| id | false | string | 选填;Client 请求唯一 ID  |  |
| from   | true | long  |  开始时间 | | 
| to     | true | long | 结束时间 | | 

### req请求参数说明

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code      | true     | string | 合约代码         |         | "BTC-USDT","ETH-USDT"...                          |
| period          | true     | string  | K线类型               |         | 1min, 5min, 15min, 30min, 60min,4hour,1day, 1week, 1mon     |

#### 备注

 - 一次返回最多2000条数据；
 - from和to都为必填。

> 请求成功返回数据的例子：

```json
{
 "rep": "market.BTC-USDT.mark_price.1min",
 "status": "ok",
 "id": "id4",
 "wsid": 1231323423,
 "ts": 1579489028884,
 "data": [
   {
      "vol": "0",
      "close": "9800.12",
      "count": "0",
      "high": "9800.12",
      "id": 1529898780,
      "low": "9800.12",
      "open": "9800.12",
      "trade_turnover": "0",
      "amount": "0"
   }
 ]
}
```

### 返回参数  
| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| req     | true | string | 数据所属的 channel，格式： market.period |                | |
| status | true | string | 请求处理结果                          | "ok" , "error" | |
| id     | true | string | 业务方id       |                | |
| wsid     | true | long | wsid           |                | |
| ts     | true | long | 响应生成时间点，单位：毫秒                   |                | |
| \<data\> |   true   |    object array    |               |                | |
| id     | true | long | k线id        |                | |
| vol     | true | string | 成交量(张)，数值为0        |                | |
| count     | true | string | 成交笔数，数值为0        |                | |
| open     | true | string | 开盘值        |                | |
| close     | true | string | 收盘值      |                | |
| low     | true | string | 最低值        |                | |
| high     | true | string | 最高值      |                | |
| amount     | true | string | 成交量(币), 数值为0        |                | |
| trade_turnover     | true | string | 成交额, 数值为0        |                | |
| \</data\>            |      |        |               |                | |


# WebSocket订单和用户数据接口

## 【逐仓】订阅订单成交数据（sub）

#### 备注
 - 该接口仅支持逐仓模式。

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

### 订阅请求数据格式

  `{ `
  
  `"op": "sub",`
  
  `"cid": "cid",`
  
  `"topic": "orders.$contract_code"`
  
  `} `

> 正确的订阅请求:

```json

{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "topic": "orders.btc-usdt"
}
```
### 订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                        |
| ------- | ----- | ------------------------------------------ |
| op       | string | 必填；操作名称，订阅固定值为sub             |
| cid      | string | 选填;Client 请求唯一 ID                     |
| topic    | string |  订阅主题名称，必填 (orders.$contract_code) 订阅、取消订阅某个合约下的成交订单信息； $contract_code为合约代码（BTC-USDT、ETH-USDT...），如果值为 * 时代表订阅所有合约; |

 - 备注：postOnly的报单收到的WS推送要么是报单成功，状态为3，要么是7，已撤单。

> 成交详情通知数据格式说明

```json

{
    "op": "notify", 
    "topic": "orders.btc-usdt", 
    "ts": 1489474082831, 
    "uid": "123456789",
    "symbol": "BTC", 
    "contract_code": "BTC-USDT", 
    "volume": 111, 
    "price": 1111, 
    "order_price_type": "limit",
    "direction": "buy", 
    "offset": "open", 
    "status": 6,
    "lever_rate": 10, 
    "order_id":758684042347171840,
    "order_id_str":"758684042347171840", 
    "client_order_id": 10683, 
    "order_source": "web", 
    "order_type": 1, 
    "created_at": 1408076414000,
    "trade_volume": 1,
    "trade_turnover": 1200, 
    "fee": 0, 
    "liquidation_type": "0",
    "trade_avg_price": 10, 
    "margin_asset": "USDT",
    "margin_frozen": 10, 
    "profit": 2,
    "canceled_at": 1408076414000, 
    "fee_asset": "USDT",
    "margin_mode": "isolated",
    "margin_account": "BTC-USDT",
    "is_tpsl": 0,
    "real_profit": 0,
    "trade": [{
        "trade_id":14469,
        "id":"14469-758684042347171840-1", 
        "trade_volume": 1, 
        "trade_price": 123.4555, 
        "trade_fee": 0.234,
        "fee_asset": "USDT", 
        "trade_turnover": 34.123, 
        "created_at": 1490759594752, 
        "role": "maker",
        "profit": 2,
        "real_profit": 0
  }]
}
```

### 成交推送请求数据格式说明

| 参数名称   | 是否必须 | 类型  | 描述   |取值范围           |
| -------------- | ---- | ------- | -------------------------- | ----- |
| op   | true <img width=250/> | string  | 操作名称，推送固定值为 notify; <img width=1000/>   |    |
| topic   | true | string  | 推送的主题   |    |
| ts   | true | long  | 服务端应答时间戳   |    |
| uid   | true | string  | 用户uid  |    |
| symbol   | true | string  | 品种代码   |  "BTC","ETH"...  |
| contract_code   | true | string  | 合约代码   |    |
| volume   | true | decimal  | 委托数量   |    |
| price   | true | decimal  | 委托价格   |    |
| order_price_type   | true | string  | 订单报价类型    | "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单 |
| direction   | true | string  |  买卖方向  |  "buy":买 "sell":卖  |
| offset   | true | string  |  开平方向  |    "open":开 "close":平 |
| status   | true | int  | 订单状态   |  1准备提交 2准备提交 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单  |
| lever_rate   | true | int  | 杠杆倍数   |     |
| order_id   | true | long  | 订单ID   |    |
| order_id_str   | true | string  | string格式的订单ID   |    |
| client_order_id   | true | long  | 客户订单ID   |    |
| order_source   | true | string  | 订单来源   |  system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发  |
| order_type   | true | int  | 订单类型    |  1:报单 、 2:撤单 、 3:强平、4:交割  |
| created_at   | true | long  | 订单创建时间   |    |
| trade_volume   | true | decimal  | 成交总数量   |    |
| trade_turnover   | true | decimal  | 成交总金额，即sum（每一笔成交张数 * 合约面值 *成交价格）   |    |
| fee   | true | decimal  | 手续费   |    |
| trade_avg_price   | true | decimal  | 成交均价   |    |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_frozen   | true | decimal  | 冻结保证金   |    |
| profit   | true | decimal  | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）   |    |
| liquidation_type   | true | decimal  | 强平类型 0:非强平类型，1：多空轧差， 2:部分接管，3：全部接管   |    |
| canceled_at               | true     | long    | 撤单时间   |  |
| fee_asset               | true     | string    | 手续费币种          | “USDT” |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| is_tpsl | true | int | 是否设置止盈止损  | 1：是；0：否 |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \<trade\>   | true | object array |     |    |
| id   | true | string  | 全局唯一的交易标识    |    |
| trade_id | true | long  | 与linear-swap-api/v1/swap_matchresults返回结果中的match_id一样，是撮合结果id， 非唯一，可重复，注意：一个撮合结果代表一个taker单和N个maker单的成交记录的集合，如果一个taker单吃了N个maker单，那这N笔trade都是一样的撮合结果id   |    |
| trade_volume   | true | decimal  | 成交数量    |    |
| trade_price   | true | decimal  | 成交价格    |    |
| trade_fee   | true | decimal  | 成交手续费    |    |
| trade_turnover   | true | decimal  | 成交金额（成交数量*合约面值*成交价格 ）    |    |
| created_at   | true | long  | 成交创建时间    |    |
| role   | true | string  | taker或maker    |    |
| real_profit | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| profit                  | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）             |
| fee_asset   | true | string  | 手续费币种   |  “USDT”  |
| \</trade\>   |  |   |     |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 只有在2021年1月30日0点后创建的订单，订单级别的真实收益（real_profit）字段才会有值。而成交级别的真实收益（real_profit）在2020年12月10日后就会有值。

## 【逐仓】取消订阅订单成交数据（unsub）

#### 备注
 - 该接口仅支持逐仓模式。

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`

  `"op": "unsub",`
  
  `"topic": "orders.$contract_code", `
  
  `"cid": "id generated by client",`
  
  `}`

> 正确的取消订阅请求:

```json

{                                
  "op": "unsub",                   
  "topic": "orders.BTC-USDT",       
  "cid": "40sG903yz80oDFWr"        
}                                  
```                                


### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;待取消订阅主题名称:orders.$contract_code，订阅、取消订阅某个合约下的成交订单信息； $contract_code为合约代码（BTC-USDT、ETH-USDT...），如果值为 * 时代表订阅所有合约;  |


### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| orders.*       | orders.*        | 允许   |
| orders.contract_code1 | orders.*        | 允许   |
| orders.contract_code1 | orders.contract_code1  | 允许   |
| orders.contract_code1 | orders.contract_code2  | 不允许 |
| orders.*       | orders.contract_code1  | 不允许 |

## 【全仓】订阅订单成交数据（sub）

#### 备注
 - 该接口仅支持全仓模式。

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

### 订阅请求数据格式

  `{ `
  
  `"op": "sub",`
  
  `"cid": "cid",`
  
  `"topic": "orders_cross.$contract_code"`
  
  `} `

> 正确的订阅请求:

```json

{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "topic": "orders_cross.btc-usdt"
}
```
### 订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                        |
| ------- | ----- | ------------------------------------------ |
| op       | string | 必填；操作名称，订阅固定值为sub             |
| cid      | string | 选填;Client 请求唯一 ID                     |
| topic    | string |  订阅主题名称，必填 (orders_cross.$contract_code) 订阅、取消订阅某个合约下的成交订单信息； $contract_code为合约代码（BTC-USDT、ETH-USDT...），如果值为 * 时代表订阅所有合约; |

 - 备注：postOnly的报单收到的WS推送要么是报单成功，状态为3，要么是7，已撤单。

> 成交详情通知数据格式说明

```json

{
    "op":"notify",
    "topic":"orders_cross.btc-usdt",
    "ts":1606878438414,
    "symbol":"BTC",
    "contract_code":"BTC-USDT",
    "volume":8,
    "price":50000,
    "order_price_type":"limit",
    "direction":"buy",
    "offset":"close",
    "status":6,
    "lever_rate":100,
    "order_id":783650498317316098,
    "order_id_str":"783650498317316098",
    "client_order_id":null,
    "order_source":"risk",
    "order_type":3,
    "created_at":1606878438320,
    "trade_volume":8,
    "trade_turnover":4000,
    "fee":0,
    "trade_avg_price":50000,
    "margin_frozen":0,
    "profit":-1866.704,
    "trade":[
        {
            "trade_fee":0,
            "fee_asset":"USDT",
            "trade_id":783650498317316098,
            "id":"783650498317316098-783650498317316098-1",
            "trade_volume":8,
            "trade_price":50000,
            "trade_turnover":4000,
            "created_at":1606878438320,
            "profit":-1866.704,
            "real_profit": 0,
            "role":"taker"
        }
    ],
    "canceled_at":0,
    "fee_asset":"USDT",
    "margin_asset":"USDT",
    "uid":"123456789",
    "liquidation_type":"1",
    "margin_mode":"cross",
    "margin_account":"USDT",
    "is_tpsl": 0,
    "real_profit": 0
}
```

### 成交推送请求数据格式说明

| 参数名称   | 是否必须 | 类型  | 描述   |取值范围           |
| -------------- | ---- | ------- | -------------------------- | ----- |
| op   | true | string  | 操作名称，推送固定值为 notify;    |    |
| topic   | true | string  | 推送的主题   |    |
| ts   | true | long  | 服务端应答时间戳   |    |
| uid   | true | string  | 用户uid  |    |
| symbol   | true | string  | 品种代码   |  "BTC","ETH"...  |
| contract_code   | true | string  | 合约代码   |    |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| volume   | true | decimal  | 委托数量   |    |
| price   | true | decimal  | 委托价格   |    |
| order_price_type   | true | string  | 订单报价类型    | "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单  |
| direction   | true | string  |  买卖方向  |  "buy":买 "sell":卖  |
| offset   | true | string  |  开平方向  |    "open":开 "close":平 |
| status   | true | int  | 订单状态   |  1准备提交 2准备提交 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单  |
| lever_rate   | true | int  | 杠杆倍数   |     |
| order_id   | true | long  | 订单ID   |    |
| order_id_str   | true | string  | string格式的订单ID   |    |
| client_order_id   | true | long  | 客户订单ID   |    |
| order_source   | true | string  | 订单来源   |  system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发 |
| order_type   | true | int  | 订单类型    |  1:报单 、 2:撤单 、 3:强平、4:交割  |
| created_at   | true | long  | 订单创建时间   |    |
| trade_volume   | true | decimal  | 成交总数量   |    |
| trade_turnover   | true | decimal  | 成交总金额，即sum（每一笔成交张数 * 合约面值 *成交价格）   |    |
| fee   | true | decimal  | 手续费   |    |
| trade_avg_price   | true | decimal  | 成交均价   |    |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_frozen   | true | decimal  | 冻结保证金   |    |
| profit   | true | decimal  | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）   |    |
| liquidation_type   | true | decimal  | 强平类型 0:非强平类型，1：多空轧差， 2:部分接管，3：全部接管   |    |
| canceled_at               | true     | long    | 撤单时间   |  |
| fee_asset               | true     | string    | 手续费币种          | “USDT” |
| is_tpsl | true | int | 是否设置止盈止损  | 1：是；0：否 |
| real_profit | true | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| \<trade\>   | true | object array |     |    |
| id   | true | string  | 全局唯一的交易标识    |    |
| trade_id | true | long  | 与linear-swap-api/v1/swap_cross_matchresults返回结果中的match_id一样，是撮合结果id， 非唯一，可重复，注意：一个撮合结果代表一个taker单和N个maker单的成交记录的集合，如果一个taker单吃了N个maker单，那这N笔trade都是一样的撮合结果id    |    |
| trade_volume   | true | decimal  | 成交数量    |    |
| trade_price   | true | decimal  | 成交价格    |    |
| trade_fee   | true | decimal  | 成交手续费    |    |
| trade_turnover   | true | decimal  | 成交金额（成交数量*合约面值*成交价格 ）    |    |
| created_at   | true | long  | 成交创建时间    |    |
| role   | true | string  | taker或maker    |    |
| real_profit | decimal | 真实收益（使用开仓均价计算，包含仓位跨结算的已实现盈亏。）  |  |
| profit                  | decimal | 平仓盈亏（使用持仓均价计算，不包含仓位跨结算的已实现盈亏。）             |
| fee_asset   | true | string  | 手续费币种   |  “USDT”  |
| \</trade\>   |  |   |     |

#### 备注：
 - 真实收益为开仓均价和成交价计算得出（订单的真实收益为订单下每笔成交的真实收益之和）。
 - 只有在2021年1月30日0点后创建的订单，订单级别的真实收益（real_profit）字段才会有值。而成交级别的真实收益（real_profit）在2020年12月10日后就会有值。

## 【全仓】取消订阅订单成交数据（unsub）

#### 备注
 - 该接口仅支持全仓模式。

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`

  `"op": "unsub",`
  
  `"topic": "orders_cross.$contract_code", `
  
  `"cid": "id generated by client",`
  
  `}`

> 正确的取消订阅请求:

```json

{                                
  "op": "unsub",                   
  "topic": "orders_cross.BTC-USDT",       
  "cid": "40sG903yz80oDFWr"        
}                                  
```                                


### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;待取消订阅主题名称:orders_cross.$contract_code，订阅、取消订阅某个合约下的成交订单信息； $contract_code为合约代码（BTC-USDT、ETH-USDT...），如果值为 * 时代表订阅所有合约;  |


### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| orders_cross.*       | orders_cross.*        | 允许   |
| orders_cross.contract_code1 | orders_cross.*        | 允许   |
| orders_cross.contract_code1 | orders_cross.contract_code1  | 允许   |
| orders_cross.contract_code1 | orders_cross.contract_code2  | 不允许 |
| orders_cross.*       | orders_cross.contract_code1  | 不允许 |

## 【逐仓】资产变动数据（sub）

#### 备注
 - 该接口仅支持逐仓模式。

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

### 订阅请求数据格式

  `{`
  
  `"op": "sub",`
  
  `"topic": "accounts.$contract_code",`
  
  `"cid": "id generated by client",`
  
  `}`


> 正确的订阅请求:                           
                                    
```json                             
                                    
{                                   
  "op": "sub",                      
  "cid": "40sG903yz80oDFWr",        
  "topic": "accounts.BTC-USDT"       
}                                   
                                    
```                                 

### 订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                        |
| :------- | :----- | :------------------------------------------ |
| op       | string | 必填；操作名称，订阅固定值为sub             |
| cid      | string | 选填;Client 请求唯一 ID                     |
| topic    | string | 必填；订阅主题名称，必填 (accounts.$contract_code)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码; contract_code支持大小写，比如BTC-USDT|

#### 备注：

- 推送接口新增定期推送逻辑：每 5 秒进行一次定期推送，由定期推送触发的数据中 event 参数值为“snapshot”，表示由系统定期推送触发。 如果5秒内某合约资产已触发过推送，则该合约资产跳过此次推送。


> 当资产有更新时，返回的参数示例如下:

```json

{
    "op":"notify",
    "topic":"accounts.btc-usdt",
    "ts":1603711370689,
    "event":"order.open",
    "data":[
        {
            "symbol":"BTC",
            "contract_code":"BTC-USDT",
            "margin_balance":79.72434662,
            "margin_static":79.79484662,
            "margin_position":1.31303,
            "margin_frozen":4.0662,
            "margin_available":74.34511662,
            "profit_real":0.03405608,
            "profit_unreal":-0.0705,
            "withdraw_available":74.34511662,
            "risk_rate":14.745772976801512484,
            "liquidation_price":92163.420962779156327543,
            "lever_rate":10,
            "adjust_factor":0.075,
            "margin_asset":"USDT",
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT"
        }
    ],
    "uid":"123456789"
}

```

### 返回字段说明

| 参数名称   | 是否必须 | 类型  | 描述   | 取值范围   |
| -------------- | ---- | ------- | -------------------------- |---- |
| op   | true <img width=250/> | string  | 操作名称，推送固定值为 notify; <img width=1000/>   |   |
| topic   | true | string  | 推送的主题   |   |
| ts   | true | long  | 服务端应答时间戳   |   |
| uid   | true | string  | 用户uid  |    |
| event   | true | string  | 资产变化通知相关事件说明 |  比如订单创建开仓(order.open) 、订单成交(order.match)（除开强平和结算交割）、结算交割(settlement)、订单强平成交(order.liquidation)（对钆和接管仓位）、订单撤销(order.cancel) 、合约账户划转（contract.transfer)（包括外部划转、母子划转和不同保证金账户划转）、系统（contract.system)、其他资产变化(other)、切换杠杆（switch_lever_rate）、初始资金（init）、由系统定期推送触发（snapshot） |
| \<data\>   | true | object array |     |   |
| symbol   | true | string  | 品种代码   | "BTC","ETH"...   |
| contract_code   | true | string  | 合约代码   | "BTC-USDT","ETH-USDT"...   |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_balance   | true | decimal  | 账户权益  |   |
| margin_static   | true | decimal  | 静态权益  |   |
| margin_position   | true | decimal  |  持仓保证金（当前持有仓位所占用的保证金） |   |
| margin_frozen   | true | decimal  | 冻结保证金  |   |
| margin_available   | true | decimal  | 可用保证金  |   |
| profit_real   | true | decimal  | 已实现盈亏  |   |
| profit_unreal   | true | decimal  | 未实现盈亏  |   |
| risk_rate   | true | decimal  | 保证金率  |   |
| liquidation_price   | true | decimal  | 预估强平价  |   |
| withdraw_available   | true | decimal  | 可划转数量  |   |
| lever_rate   | true | int  | 杠杆倍数  |   |
| adjust_factor   | true | decimal  | 调整系数  |   |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| \</data\>   |  |   |     |   |

## 【逐仓】取消订阅资产变动数据（unsub）

#### 备注
 - 该接口仅支持逐仓模式。

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`
  
  `"op": "unsub",`
  
  `"topic": "accounts.$contract_code",`
  
  `"cid": "id generated by client",`
  
  `}`

> 正确的取消订阅请求:

```json
                               
{                                 
  "op": "unsub",                  
  "topic": "accounts.BTC-USDT",    
  "cid": "40sG903yz80oDFWr"       
}   
                                 
```  
                             
### 取消订阅请求数据格式说明

字段名称 | 类型   | 说明                                               |
------- | ----- | ------------------------------------------------- |
op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
cid      | string | 选填;Client 请求唯一 ID                            |
topic    | string | 必填;必填；必填；订阅主题名称，必填 (accounts.$contract_code)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码;contract_code支持大小写; |

### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| accounts.*       | accounts.*        | 允许   |
| accounts.contract_code1 | accounts.*        | 允许   |
| accounts.contract_code1 | accounts.contract_code1  | 允许   |
| accounts.contract_code1 | accounts.contract_code2  | 不允许 |
| accounts.*       | accounts.contract_code1  | 不允许 |

## 【全仓】资产变动数据（sub）

#### 备注
 - 该接口仅支持全仓模式。

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

### 订阅请求数据格式

  `{`
  
  `"op": "sub",`
  
  `"topic": "accounts_cross.$margin_account",`
  
  `"cid": "id generated by client",`
  
  `}`


> 正确的订阅请求:                           
                                    
```json                             
                                    
{                                   
  "op": "sub",                      
  "cid": "40sG903yz80oDFWr",        
  "topic": "accounts_cross.USDT"       
}                                   
                                    
```                                 

### 订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                        |
| ------- | ----- | ------------------------------------------ |
| op       | string | 必填；操作名称，订阅固定值为sub             |
| cid      | string | 选填;Client 请求唯一 ID                     |
| topic    | string | 必填；订阅主题名称，必填 (accounts_cross.$margin_account)  订阅、取消订阅某个全仓账户下的资产变更信息，margin_account目前只有一个全仓账户（USDT） |

#### 备注：

- 推送接口新增定期推送逻辑：每 5 秒进行一次定期推送，由定期推送触发的数据中 event 参数值为“snapshot”，表示由系统定期推送触发。 如果5秒内某合约资产已触发过推送，则该合约资产跳过此次推送。


> 当资产有更新时，返回的参数示例如下:

```json

{
    "op":"notify",
    "topic":"accounts_cross.usdt",
    "ts":1606878438415,
    "event":"order.liquidation",
    "data":[
        {
            "margin_mode":"cross",
            "margin_account":"USDT",
            "margin_asset":"USDT",
            "margin_balance":1591.122082549410817836,
            "margin_static":1591.122082549410817836,
            "margin_position":47.99916,
            "margin_frozen":0,
            "profit_real":-1866.704,
            "profit_unreal":0,
            "withdraw_available":1543.122922549410817836,
            "risk_rate":59.270830593679738555,
            "contract_detail":[
                {
                    "symbol":"BTC",
                    "contract_code":"BTC-USDT",
                    "margin_position":47.99916,
                    "margin_frozen":0,
                    "margin_available":1497.561881274705408918,
                    "profit_unreal":0,
                    "liquidation_price":42160.036464495601721318,
                    "lever_rate":100,
                    "adjust_factor":0.55
                }
            ]
        }
    ],
    "uid":"123456789"
}

```

### 返回字段说明

| 参数名称   | 是否必须 | 类型  | 描述   | 取值范围   |
| -------------- | ---- | ------- | -------------------------- |---- |
| op   | true <img width=250/> | string  | 操作名称，推送固定值为 notify; <img width=1000/>    |   |
| topic   | true | string  | 推送的主题   |   |
| ts   | true | long  | 服务端应答时间戳   |   |
| uid   | true | string  | 用户uid  |    |
| event   | true | string  | 资产变化通知相关事件说明 |  比如订单创建开仓(order.open) 、订单成交(order.match)（除开强平和结算交割）、结算交割(settlement)、订单强平成交(order.liquidation)（对钆和接管仓位）、订单撤销(order.cancel) 、合约账户划转（contract.transfer)（包括外部划转、母子划转和不同保证金账户划转）、系统（contract.system)、其他资产变化(other)、切换杠杆（switch_lever_rate） 、初始资金（init）、由系统定期推送触发（snapshot） |
| \<data\>   | true | object array |     |   |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| margin_balance       | true   | decimal | 账户权益                 |                |
| margin_static        | true   | decimal | 静态权益                 |                |
| margin_position      | true   | decimal | 持仓保证金（当前持有仓位所占用的保证金） |                |
| margin_frozen        | true   | decimal | 冻结保证金                |                |
| profit_real          | true   | decimal | 已实现盈亏                |                |
| profit_unreal        | true   | decimal | 未实现盈亏                |                |
| withdraw_available   | true   | decimal | 可划转数量                |                |
| risk_rate            | true   | decimal | 保证金率                 |                |
| \<contract_detail\> |    true    |  object array       |    支持全仓的合约相关字段                  |                |
| symbol     | true   | string  | 品种代码                 | "BTC","ETH"... |
| contract_code     | true   | string  | 合约代码                 |  "BTC-USDT" ... |
| margin_position      | true   | decimal | 持仓保证金（当前持有仓位所占用的保证金） |                |
| margin_frozen        | true   | decimal | 冻结保证金                |                |
| margin_available     | true   | decimal | 可用保证金                |                |
| profit_unreal        | true   | decimal | 未实现盈亏                |                |
| liquidation_price | true | decimal | 预估强平价         |                |
| lever_rate           | true   | decimal | 杠杠倍数                 |                |
| adjust_factor        | true   | decimal | 调整系数                 |                |
| \</contract_detail\>            |        |         |                      |                |
| \</data\>   |  |   |     |   |

## 【全仓】取消订阅资产变动数据（unsub）

#### 备注
 - 该接口仅支持全仓模式。

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`
  
  `"op": "unsub",`
  
  `"topic": "accounts_cross.$margin_account",`
  
  `"cid": "id generated by client",`
  
  `}`

> 正确的取消订阅请求:

```json
                               
{                                 
  "op": "unsub",                  
  "topic": "accounts_cross.USDT",    
  "cid": "40sG903yz80oDFWr"       
}   
                                 
```  
                             
### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| ------- | ----- | ------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填；订阅主题名称，必填 (accounts_cross.$margin_account)  订阅、取消订阅某个全仓账户的资产变更信息|

### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| accounts_cross.*       | accounts_cross.*        | 允许   |
| accounts_cross.margin_account1 | accounts_cross.*        | 允许   |
| accounts_cross.margin_account1 | accounts_cross.margin_account1  | 允许   |
| accounts_cross.margin_account1 | accounts_cross.margin_account2  | 不允许 |
| accounts_cross.*       | accounts_cross.margin_account1  | 不允许 |

## 【逐仓】持仓变动更新数据（sub）

#### 备注
 - 该接口仅支持逐仓模式。

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

### 订阅请求数据格式

  `{`
  
  `"op": "sub",`
  
  `"topic": "positions.$contract_code",`
  
  `"cid": "topic to sub"`
  
  `}`

> 正确的订阅请求:

```json
                               
{                                 
  "op": "sub",                    
  "cid": "40sG903yz80oDFWr",      
  "topic": "positions.BTC-USDT"    
}
                                 
```                               

### 订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                        |
| :------- | :----- | :------------------------------------------ |
| op       | string | 必填；操作名称，订阅固定值为sub             |
| cid      | string | 选填;Client 请求唯一 ID                     |
| topic    | string | 必填；订阅主题名称，必填 (positions.$contract_code)  订阅、取消订阅某个合约代码下的持仓变更信息，当 $contract_code值为 * 时代表订阅所有合约代码,contract_code支持大小写;  |


> 当持仓有更新时，返回的参数示例如下:

```json

{
    "op":"notify",
    "topic":"positions",
    "ts":1603711371803,
    "event":"snapshot",
    "data":[
        {
            "symbol":"BTC",
            "contract_code":"BTC-USDT",
            "volume":1,
            "available":0,
            "frozen":1,
            "cost_open":13059.8,
            "cost_hold":13059.8,
            "profit_unreal":-0.0705,
            "profit_rate":-0.05398244996094886,
            "profit":-0.0705,
            "position_margin":1.31303,
            "lever_rate":10,
            "direction":"sell",
            "last_price":13130.3,
            "margin_asset":"USDT",
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT"
        }
    ],
    "uid":"123456789"
}

```

### 返回参数

| 字段名称                | 类型    | 说明                                                         |
| ----------------------- | ------- | ------------------------------------------------------------ |
| op       | string |             |
| topic       | string |               订阅主题   |
| uid           | string    | 账户id	                                             |
| ts                     | long  | 响应生成时间点，单位：毫秒                           |
| event                  | string  | 持仓变化通知相关事件说明，比如订单创建平仓(order.close) 、订单成交(order.match)（除开强平和结算交割）、结算交割(settlement)、订单强平成交(order.liquidation)（对钆和接管仓位）、订单撤销(order.cancel)、切换杠杆（switch_lever_rate）、 初始持仓（init）、由系统定期推送触发（snapshot）    |
| \<data\>  | array object |  | |
| symbol                 | string    | 品种代码 ,"BTC","ETH"...                                             |
| contract_code          | string  | 合约代码，"BTC-USDT"                                                       |
| volume                 | decimal  | 持仓量                                                     |
| available              | decimal | 可平仓数量                                                     |
| frozen                 | decimal | 冻结数量                                                      |
| cost_open              | decimal  | 开仓均价                |
| cost_hold              | decimal  | 持仓均价                                          |
| profit_unreal          | decimal  |未实现盈亏                                        |
| profit_rate            | decimal     | 收益率 |
| profit                 | decimal     | 收益                                                     |
| position_margin        | decimal    | 持仓保证金                                                       |
| lever_rate             | int     | 杠杆倍数                                                      |
| direction              | string    | 仓位方向   "buy":买 "sell":卖                                                     |
| last_price             | decimal    | 最新价                                                       |
| margin_asset           | string | 保证金币种（计价币种）                 |  
| margin_account        |  string | 保证金账户  比如“BTC-USDT” |
| margin_mode           |  string | 保证金模式  isolated：逐仓模式 |
| \</data\> | | |  | |


#### 备注：

- 推送接口新增定期推送逻辑：每 5 秒进行一次定期推送，由定期推送触发的数据中 event 参数值为“snapshot”，表示由系统定期推送触发。 如果5秒内某仓位已触发过推送，则该仓位跳过此次推送。

- 当用户持仓量为0时使用切换杠杆的接口，持仓推送接口不会推送"switch_lever_rate"。

## 【逐仓】取消订阅持仓变动数据（unsub）

#### 备注
 - 该接口仅支持逐仓模式。

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`
  
  `"op": "unsub",`
  
  `"topic": "positions.$contract_code",`
  
  `"cid": "id generated by client", `
  
  `} `

> 正确的取消订阅请求:

```json
                                 
{                                    
  "op": "unsub",                     
  "topic": "positions.BTC-USDT",      
  "cid": "40sG903yz80oDFWr"          
}                                    
```                                  

### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| ------- | ----- | ------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;必填；必填；订阅主题名称，必填 (positions.$contract_code)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码;contract_code支持大小写,比如BTC-USDT  |


### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| positions.*       | positions.*        | 允许   |
| positions.contract_code1 | positions.*        | 允许   |
| positions.contract_code1 | positions.contract_code1  | 允许   |
| positions.contract_code1 | positions.contract_code2  | 不允许 |
| positions.*       | positions.contract_code1  | 不允许 |

## 【全仓】持仓变动更新数据（sub）

#### 备注
 - 该接口仅支持全仓模式。

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

### 订阅请求数据格式

  `{`
  
  `"op": "sub",`
  
  `"topic": "positions_cross.$contract_code",`
  
  `"cid": "topic to sub"`
  
  `}`

> 正确的订阅请求:

```json
                               
{                                 
  "op": "sub",                    
  "cid": "40sG903yz80oDFWr",      
  "topic": "positions_cross.BTC-USDT"    
}
                                 
```                               

### 订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                        |
| :------- | :----- | :------------------------------------------ |
| op       | string | 必填；操作名称，订阅固定值为sub             |
| cid      | string | 选填;Client 请求唯一 ID                     |
| topic    | string | 必填；订阅主题名称，必填 (positions_cross.$contract_code)  订阅、取消订阅某个合约代码下的持仓变更信息，当 $contract_code值为 * 时代表订阅所有合约代码,contract_code支持大小写;  |


> 当持仓有更新时，返回的参数示例如下:

```json

{
    "op":"notify",
    "topic":"positions_cross.btc-usdt",
    "ts":1606878438415,
    "event":"order.liquidation",
    "data":[
        {
            "symbol":"BTC",
            "contract_code":"BTC-USDT",
            "volume":18,
            "available":18,
            "frozen":0,
            "cost_open":19361.088515384615384611,
            "cost_hold":26666.2,
            "profit_unreal":0,
            "profit_rate":-37.7308924485864104,
            "profit":-1314.92006723076923077,
            "margin_asset":"USDT",
            "position_margin":47.99916,
            "lever_rate":100,
            "direction":"sell",
            "last_price":26666.2,
            "margin_mode":"cross",
            "margin_account":"USDT"
        }
    ],
    "uid":"123456789"
}

```

### 返回参数

| 参数名称   | 是否必须 | 类型  | 描述   | 取值范围   |
| -------------- | ---- | ------- | -------------------------- | ----- |
| op   | true <img width=250/> | string  | 操作名称，推送固定值为 notify; <img width=1000/>   |    |
| topic   | true | string  | 推送的主题   |    |
| ts   | true | long  | 服务端应答时间戳   |    |
| uid   | true | string  | 用户uid  |    |
| event   | true | string  | 持仓变化通知相关事件说明 | 比如订单创建平仓(order.close) 、订单成交(order.match)（除开强平和结算交割）、结算交割(settlement)、订单强平成交(order.liquidation)（对钆和接管仓位）、订单撤销(order.cancel) 、切换杠杆（switch_lever_rate）、初始持仓（init）、由系统定期推送触发（snapshot）   |
| \<data\>   | true | object array |     |    |
| symbol   | true | string  | 品种代码    | "BTC","ETH"...   |
| contract_code   | true | string  | 合约代码  |    |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| volume   | true | decimal  | 持仓量（张）  |    |
| available   | true | decimal  | 可平仓数量 （张） |    |
| frozen   | true | decimal  |  冻结数量（张） |    |
| cost_open   | true | decimal  | 开仓均价  |    |
| cost_hold   | true | decimal  | 持仓均价  |    |
| profit_unreal   | true | decimal  | 未实现盈亏  |    |
| profit_rate   | true | decimal  | 收益率  |    |
| profit   | true | decimal  | 收益  |    |
| margin_asset       | true   | string | 保证金币种（计价币种）                 |                |
| position_margin   | true | decimal  | 持仓保证金  |    |
| lever_rate   | true | int  | 杠杆倍数  |    |
| direction   | true | string  | 仓位方向|   "buy":买 "sell":卖    |
| last_price   | true | decimal  | 最新成交价  |    |
| \</data\>   |  |   |     |    |


#### 备注：

- 推送接口新增定期推送逻辑：每 5 秒进行一次定期推送，由定期推送触发的数据中 event 参数值为“snapshot”，表示由系统定期推送触发。 如果5秒内某仓位已触发过推送，则该仓位跳过此次推送。

- 当用户持仓量为0时使用切换杠杆的接口，持仓推送接口不会推送"switch_lever_rate"。

## 【全仓】取消订阅持仓变动数据（unsub）

#### 备注
 - 该接口仅支持全仓模式。

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`
  
  `"op": "unsub",`
  
  `"topic": "positions_cross.$contract_code",`
  
  `"cid": "id generated by client", `
  
  `} `

> 正确的取消订阅请求:

```json
                                 
{                                    
  "op": "unsub",                     
  "topic": "positions_cross.BTC-USDT",      
  "cid": "40sG903yz80oDFWr"          
}                                    
```                                  

### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| ------- | ----- | ------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;必填；必填；订阅主题名称，必填 (positions_cross.$contract_code)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码;contract_code支持大小写,比如BTC-USDT  |


### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| positions_cross.*       | positions_cross.*        | 允许   |
| positions_cross.contract_code1 | positions_cross.*        | 允许   |
| positions_cross.contract_code1 | positions_cross.contract_code1  | 允许   |
| positions_cross.contract_code1 | positions_cross.contract_code2  | 不允许 |
| positions_cross.*       | positions_cross.contract_code1  | 不允许 |

## 【逐仓】订阅合约订单撮合数据（sub）

#### 备注
 - 该接口仅支持逐仓模式。

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

  `{`
  
  `"op": "sub",`
  
  `"cid": "40sG903yz80oDFWr",`
  
  `"topic": "matchOrders.$contract_code"`
  
  `}`
  
> 正确的订阅请求:

```json

{                                    
  "op": "sub",                     
  "topic": "matchOrders.BTC-USDT",      
  "cid": "40sG903yz80oDFWr"          
}                                    
``` 

### 请求参数

| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围           |
| ------ | ---- | ------ | -------- | -------------- |
| op | true | string | 订阅固定值为sub	 |  |
| cid | false| string | Client 请求唯一 ID	 | |
| topic | true| string | 订阅主题名称，(matchOrders.$contract_code) 订阅某个品种下的合约变动信息；$contract_code为品种代码（BTC-USDT、ETH-USDT），如果值为 * 时代表订阅所有品种; contract_code支持大小写; | |

#### 备注：
- postOnly的报单收到的WS推送要么是报单成功，状态为3，要么是7，已撤单;
- 撮合完成后就将订单的更新信息推送给客户端;
- 强平以及轧差订单不会推送；
- 外部划转或内部转账订单不作为订单推送；
- 通常情况下，撮合完成后的推送要比清算完成后的推送快，但不能保证撮合完成后的推送一定比清算完成后的推送更快;
- 撮合后的推送，假设1个matchresult包含N笔成交，包括1个taker和N个maker，那最多推送N+1笔；
- 如果遇到推送的status状态为9或者10，可以直接忽略。

> 返回的参数为：

```json

{
    "op":"notify",
    "topic":"matchOrders.btc-usdt",
    "ts":1600926986125,
    "symbol":"BTC",
    "contract_code":"BTC-USDT",
    "status":6,
    "order_id":758688290195656704,
    "order_id_str":"758688290195656704",
    "client_order_id":null,
    "order_type":1,
    "created_at":1600926984112,
    "trade":[
        {
            "trade_id":14470,
            "id":"14470-758688290195656704-1",
            "trade_volume":1,
            "trade_price":10329.11,
            "trade_turnover":103.2911,
            "created_at":1600926986046,
            "role":"taker"
        }
    ],
    "uid":"123456789",
    "volume":1,
    "trade_volume":1,
    "direction":"buy",
    "offset":"open",
    "lever_rate":5,
    "price":10329.11,
    "order_source":"web",
    "order_price_type":"opponent",
    "margin_mode": "isolated",
    "margin_account": "BTC-USDT",
    "is_tpsl": 0
}

```

### 返回参数

| 参数名称   | 是否必须 | 类型  | 描述   |  取值范围   |
| -------------- | ---- | ------- | -------------------------- |  ---- |
| op   | true <img width=250/> | string <img width=250/> | 操作名称，推送固定值为 notify; <img width=1000/>   |   |
| topic   | true | string  | 推送的主题   |   |
| ts   | true | long  | 服务端应答时间戳   |   |
| uid   | true | string  | 用户uid  |    |
| symbol   | true | string  | 品种代码  |  "BTC","ETH"...  |
| contract_code   | true | string  | 合约代码  |   |
| status   | true | int  | 订单状态 | (3未成交 4部分成交 5部分成交已撤单 6全部成交 7已撤单)   |
| order_id   | true | long  | 订单ID  |    |
| order_id_str   | true | string  |订单ID ,字符串类型  |   |
| client_order_id               | true     | long    | 客户订单id             |  |
| order_type   | true | int  | 订单类型  | 1:报单 、 2:撤单 、 3:强平、4:交割  |
| trade_volume    | true     | decimal  |   订单已成交数量    |                |
| volume                  | true     | decimal  |      订单总委托数量        |                |
| direction   | true | string  |  买卖方向  |  "buy":买 "sell":卖  |
| offset   | true | string  |  开平方向  |    "open":开 "close":平 |
| lever_rate              | true | int     | 杠杆倍数        |                  |
| price            | true     | decimal      | 委托价格                                                     |                                                              |
| created_at       | true     | long         | 创建时间                                                     |                                                              |
| order_source     | true     | string       | 订单来源                                                     | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发）    |
| order_price_type | true     | string       | 订单报价类型                                                 |  "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单    |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| is_tpsl | true | int | 是否设置止盈止损  | 1：是；0：否 |
| \<trade\>   | true | object array |     |    |
| id   | true | string  | 全局唯一的交易标识  |   |
| trade_id   | true | long  | 与linear-swap-api/v1/swap_matchresults返回结果中的match_id一样，是撮合结果id， 非唯一，可重复，注意：一个撮合结果代表一个taker单和N个maker单的成交记录的集合，如果一个taker单吃了N个maker单，那这N笔trade都是一样的撮合结果id   |   |
| trade_price   | true | decimal  | 成交价格  |   |
| trade_volume   | true | decimal  | 成交量（张）  |   |
| trade_turnover   | true | decimal  | 成交金额（成交数量*合约面值*成交价）  |   |
| created_at   | true | long  | 创建时间  |   |
| role   | true | string  | taker或maker  |   |
| \</trade\>   |  |  |     |    |

## 【逐仓】取消订阅合约订单撮合数据（unsub）

#### 备注
 - 该接口仅支持逐仓模式。

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`
  
  `"op": "unsub",`
  
  `"topic": "matchOrders.$contract_code",`
  
  `"cid": "id generated by client",`
  
  `}`
 
> 正确的取消订阅请求:

```json
                                  
{                                    
  "op": "unsub",                     
  "topic": "matchOrders.BTC-USDT",   
  "cid": "40sG903yz80oDFWr"          
}                                    
```                                  
 
### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;必填；必填；订阅主题名称，必填 (matchOrders.$contract_code)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码; |

### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| matchOrders.*       | matchOrders.*       | 允许   |
| matchOrders.contract_code1 | matchOrders.*        | 允许   |
| matchOrders.contract_code1 | matchOrders.contract_code1 | 允许   |
| matchOrders.contract_code1 | matchOrders.contract_code2  | 不允许 |
| matchOrders.*       | matchOrders.contract_code1  | 不允许 |

## 【全仓】订阅合约订单撮合数据（sub）

#### 备注
 - 该接口仅支持全仓模式。

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

  `{`
  
  `"op": "sub",`
  
  `"cid": "40sG903yz80oDFWr",`
  
  `"topic": "matchOrders_cross.$contract_code"`
  
  `}`
  
> 正确的订阅请求:

```json

{                                    
  "op": "sub",                     
  "topic": "matchOrders_cross.BTC-USDT",      
  "cid": "40sG903yz80oDFWr"          
}                                    
``` 

### 请求参数

| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围           |
| ------ | ---- | ------ | -------- | -------------- |
| op | true | string | 订阅固定值为sub	 |  |
| cid | false| string | Client 请求唯一 ID	 | |
| topic | true| string | 订阅主题名称，(matchOrders_cross.$contract_code) 订阅某个品种下的合约变动信息；$contract_code为品种代码（BTC-USDT、ETH-USDT），如果值为 * 时代表订阅所有品种; contract_code支持大小写; | |

#### 备注：
- postOnly的报单收到的WS推送要么是报单成功，状态为3，要么是7，已撤单;
- 撮合完成后就将订单的更新信息推送给客户端;
- 强平以及轧差订单不会推送；
- 外部划转或内部转账订单不作为订单推送；
- 通常情况下，撮合完成后的推送要比清算完成后的推送快，但不能保证撮合完成后的推送一定比清算完成后的推送更快;
- 撮合后的推送，假设1个matchresult包含N笔成交，包括1个taker和N个maker，那最多推送N+1笔；
- 如果遇到推送的status状态为9或者10，可以直接忽略。

> 返回的参数为：

```json

{
    "op":"notify",
    "topic":"matchOrders_cross.btc-usdt",
    "ts":1606981093177,
    "uid":"123456789",
    "symbol":"BTC",
    "contract_code":"BTC-USDT",
    "status":6,
    "order_id":784081061787873280,
    "order_id_str":"784081061787873280",
    "client_order_id":null,
    "order_type":1,
    "volume":1,
    "trade_volume":1,
    "created_at":1606981092647,
    "direction":"sell",
    "offset":"open",
    "lever_rate":100,
    "price":51179.1,
    "order_source":"web",
    "order_price_type":"opponent",
    "trade":[
        {
            "trade_id":33380,
            "id":"33380-784081061787873280-1",
            "trade_volume":1,
            "trade_price":51179.1,
            "trade_turnover":511.791,
            "created_at":1606981093104,
            "role":"taker"
        }
    ],
    "margin_mode":"cross",
    "margin_account":"USDT",
    "is_tpsl": 0
}

```

### 返回参数

| 参数名称   | 是否必须 | 类型  | 描述   |  取值范围   |
| -------------- | ---- | ------- | -------------------------- |  ---- |
| op   | true <img width=250/> | string  <img width=250/> | 操作名称，推送固定值为 notify; <img width=1000/>    |   |
| topic   | true | string  | 推送的主题   |   |
| ts   | true | long  | 服务端应答时间戳   |   |
| uid   | true | string  | 用户uid  |    |
| symbol   | true | string  | 品种代码  |  "BTC","ETH"...  |
| contract_code   | true | string  | 合约代码  |   |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| status   | true | int  | 订单状态 | (3未成交 4部分成交 5部分成交已撤单 6全部成交 7已撤单)   |
| order_id   | true | long  | 订单ID  |    |
| order_id_str   | true | string  |订单ID ,字符串类型  |   |
| client_order_id               | true     | long    | 客户订单id             |  |
| order_type   | true | int  | 订单类型  | 1:报单 、 2:撤单 、 3:强平、4:交割  |
| trade_volume    | true     | decimal  |   订单已成交数量    |                |
| volume                  | true     | decimal  |      订单总委托数量        |                |
| direction   | true | string  |  买卖方向  |  "buy":买 "sell":卖  |
| offset   | true | string  |  开平方向  |    "open":开 "close":平 |
| lever_rate              | true | int     | 杠杆倍数        |                  |
| price            | true     | decimal      | 委托价格                                                     |                                                              |
| created_at       | true     | long         | 创建时间                                                     |    |
| is_tpsl           | true | int | 是否设置止盈止损  | 1：是；0：否 |
| order_source     | true     | string       | 订单来源                                                     |  （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发、tpsl:止盈止损触发）     |
| order_price_type | true     | string       | 订单报价类型                                                 |  "limit":限价，"opponent":对手价，"post_only":只做maker单,post only下单只受用户持仓数量限制，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单, "opponent_ioc": 对手价-IOC下单，"lightning_ioc": 闪电平仓-IOC下单，"optimal_5_ioc": 最优5档-IOC下单，"optimal_10_ioc": 最优10档-IOC下单，"optimal_20_ioc"：最优20档-IOC下单，"opponent_fok"： 对手价-FOK下单，"lightning_fok"：闪电平仓-FOK下单，"optimal_5_fok"：最优5档-FOK下单，"optimal_10_fok"：最优10档-FOK下单，"optimal_20_fok"：最优20档-FOK下单    |
| \<trade\>   | true | object array |     |    |
| id   | true | string  | 全局唯一的交易标识  |   |
| trade_id   | true | long  | 与linear-swap-api/v1/swap_cross_matchresults返回结果中的match_id一样，是撮合结果id， 非唯一，可重复，注意：一个撮合结果代表一个taker单和N个maker单的成交记录的集合，如果一个taker单吃了N个maker单，那这N笔trade都是一样的撮合结果id  |   |
| trade_price   | true | decimal  | 成交价格  |   |
| trade_volume   | true | decimal  | 成交量（张）  |   |
| trade_turnover   | true | decimal  | 成交金额（成交数量*合约面值*成交价）  |   |
| created_at   | true | long  | 创建时间  |   |
| role   | true | string  | taker或maker  |   |
| \</trade\>   |  |  |     |    |

## 【全仓】取消订阅合约订单撮合数据（unsub）

#### 备注
 - 该接口仅支持全仓模式。

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`
  
  `"op": "unsub",`
  
  `"topic": "matchOrders_cross.$contract_code",`
  
  `"cid": "id generated by client",`
  
  `}`
 
> 正确的取消订阅请求:

```json
                                  
{                                    
  "op": "unsub",                     
  "topic": "matchOrders_cross.BTC-USDT",   
  "cid": "40sG903yz80oDFWr"          
}                                    
```                                  
 
### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填；订阅主题名称，必填 (matchOrders_cross.$contract_code)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码; |

### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| matchOrders_cross.*       | matchOrders_cross.*       | 允许   |
| matchOrders_cross.contract_code1 | matchOrders_cross.*        | 允许   |
| matchOrders_cross.contract_code1 | matchOrders_cross.contract_code1 | 允许   |
| matchOrders_cross.contract_code1 | matchOrders_cross.contract_code2  | 不允许 |
| matchOrders_cross.*       | matchOrders_cross.contract_code1  | 不允许 |

## 【通用】订阅强平订单数据(免鉴权)（sub）

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 订阅强平订单数据格式

`{`

  `“op”: “sub”,`
  
  `“topic": "public.$contract_code.liquidation_orders”,`
  
  `"cid": "id generated by client”,`

`}`

> 正确的订阅请求:

```json

{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "topic": "public.BTC-USDT.liquidation_orders"
}

```

### **请求参数**
| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围           |
| ------ | ---- | ------ | -------- | -------------- |
| op | true | string | 订阅固定值为sub	 |  |
| cid | false| string | Client 请求唯一 ID	 | |
| topic | true| string | 订阅主题名称，必填 (public.$contract_code.liquidation_orders) 订阅某个品种下的强平订单信息；$contract_code为品种代码（BTC-USDT、ETH-USDT），如果值为 * 时代表订阅所有品种; contract_code支持大小写; | |


> 当有订单被爆仓账户接管后，返回的参数示例如下：

```json
{
    "op":"notify",
    "topic":"public.BTC-USDT.liquidation_orders",
    "ts":1580815422403,
    "data":[
        {
            "contract_code": "BTC-USDT",
            "symbol": "BTC",
            "direction": "sell",
            "offset": "close",
            "volume": 624,
            "price": 16701.4,
            "created_at": 1606380004694,
            "amount": 0.624,
            "trade_turnover": 10421.6736
        }
    ]
}
```

### **返回参数说明**
| 参数名称   |   是否必须  |   数据类型   |   描述   |   取值范围   |
| -------- | -------- | -------- |  --------------------------------------- | -------------- | 
| op   | true | string  | 操作名称，推送固定值为 notify;    |   |
| topic   | true | string  | 推送的主题   |   |
| ts   | true | long  | 服务端应答时间戳   |   |
| \<data\> | true | array object |  | |
| symbol   | true | string  | 品种代码  |  "BTC","ETH"...  |
| contract_code   | true | string  | 合约代码  |   |
| direction   | true | string  | 仓位方向 | "buy":买 "sell":卖    |
| offset   | true | string  | 开平方向 | "open":开 "close":平    |
| volume   | true | decimal  | 强平数量（张）  |   |
| amount   | true | decimal  | 强平数量（币）  |   |
| trade_turnover   | true | decimal  | 强平金额（计价币种）  |   |
| price   | true | decimal  | 破产价格  |   |
| created_at   | true | long  | 订单创建时间  |   |
| \</data\> | | |  | |

## 【通用】取消订阅强平订单(免鉴权)（unsub）

#### 备注
 - 该接口支持全仓模式和逐仓模式

### 取消订阅强平订单数据格式

`{`

  `“op”: “unsub”,`
  
  `“topic": "public.$contract_code.liquidation_orders”,`
  
  `"cid": "id generated by client”,`

`}`

> 正确的取消订阅请求:

```json

{
  "op": "unsub",
  "topic": "public.BTC-USDT.liquidation_orders",
  "cid": "40sG903yz80oDFWr"
}

```

### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| ------- | ------- | ------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 订阅主题名称，必填 (public.$contract_code.liquidation_orders)  订阅、取消订阅某个品种下的资产变更信息，当 $contract_code值为 * 时代表订阅所有品种;  |

### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| public.*.liquidation_orders      | public.*.liquidation_orders        | 允许   |
| public.$contract_code.liquidation_orders | public.*.liquidation_orders        | 允许   |
| public.contract_code1.liquidation_orders | public.contract_code1.liquidation_orders  | 允许   |
| public.contract_code1.liquidation_orders | public.contract_code2.liquidation_orders  | 不允许 |
| public.*.liquidation_orders      | public.contract_code1.liquidation_orders  | 不允许 |

## 【通用】订阅资金费率推送(免鉴权)（sub）

#### 备注
 - 该接口支持全仓模式和逐仓模式

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

  `{`
  
  `"op": "sub",`
  
  `"cid": "40sG903yz80oDFWr",`
  
  `"topic": "public.$contract_code.funding_rate"`
  
  `}`

> 正确的订阅请求:

```json

{
  "op": "sub",
  "topic": "public.btc-usdt.funding_rate",
  "cid": "40sG903yz80oDFWr"
}

```

### **请求参数**
| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围           |
| ------ | ---- | ------ | -------- | -------------- |
| op | true | string | 订阅固定值为sub	 |  |
| cid | false| string | Client 请求唯一 ID	 | |
| topic | true| string | 订阅主题名称，必填 (public.$contract_code.funding_rate) 订阅某个品种下的强平订单信息；$contract_code为品种代码（BTC-USDT、ETH-USDT），如果值为 * 时代表订阅所有品种; contract_code支持大小写; | |

> 当资金费率有更新时，返回的参数示例如下

```json

{
    "op":"notify",
    "topic":"public.BTC-USDT.funding_rate",
    "ts":1603778748166,
    "data":[
        {
            "symbol":"BTC",
            "contract_code":"BTC-USDT",
            "fee_asset":"USDT",
            "funding_time":"1603778700000",
            "funding_rate":"-0.000220068774978695",
            "estimated_rate":"-0.000684397270167616",
            "settlement_time":"1603785600000"
        }
    ]
}

```

### 返回参数

| 参数名称   | 是否必须 | 类型  | 描述   |  取值范围   |
| -------------- | ---- | ------- | -------------------------- |  ---- |
| op   | true | string  | 操作名称，推送固定值为 notify;    |   |
| topic   | true | string  | 推送的主题   |   |
| ts   | true | long  | 服务端应答时间戳   |   |
| \<data\>   | true | object array |     |    |
| symbol   | true | string  | 品种代码  |  "BTC","ETH"...  |
| contract_code   | true | string  | 合约代码  |   |
| fee_asset   | true | string  | 资金费币种 | "USDT"...    |
| funding_time   | true | string  | 当期资金费率时间 | "open":开 "close":平    |
| funding_rate   | true | string  | 当期资金费率  |   |
| estimated_rate   | true | string  | 下一期预测资金费率  |   |
| settlement_time   | true | string  | 结算时间  |如"1490759594752"   |
| \</data\>   |  |   |     |    |

## 【通用】取消订阅资金费率(免鉴权)（unsub）

#### 备注
 - 该接口支持全仓模式和逐仓模式

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`
  
  `"op": "unsub",`
  
  `"topic": "public.$contract_code.funding_rate",`
  
  `"cid": "id generated by client",`
  
  `}`
 
> 正确的取消订阅请求:

```json

{                                    
  "op": "unsub",                     
  "topic": "public.BTC-USDT.funding_rate",   
  "cid": "40sG903yz80oDFWr"          
}                                    
```                                  
 
### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;必填；必填；订阅主题名称，必填 (public.$contract_code.funding_rate)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码; |

### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| public.*.funding_rate       | pubic.*.funding_rate       | 允许   |
| public.contract_code1.funding_rate | public.*.funding_rate        | 允许   |
| public.contract_code1.funding_rate | public.contract_code1.funding_rate | 允许   |
| public.contract_code1.funding_rate | public.contract_code2.funding_rate  | 不允许 |
| public.*.funding_rate       | public.contract_code1.funding_rate  | 不允许 |

### 备注

推送逻辑一般是1分钟一次，但是出现以下情况时不会计算资金费率：

- 合约处于 非交易状态 （待上市，停牌，待开盘，结算中，交割中，结算完成，交割完成，下市）
- 指数update_time超过5分钟没更新，不计算资金费率
- 深度数据的updateTime超过5分钟没有更新，不计算资金费率
- 每次读取到的150档买盘深度和卖盘深度进行md5加密，如果连续5次（或以上）和前一个点的数值一致，则认为系统处于停服状态，此时不计算该点位的资金费率

## 【通用】订阅合约信息变动(免鉴权)（sub）

#### 备注
 - 该接口支持全仓模式和逐仓模式

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

  `{`
  
  `"op": "sub",`
  
  `"cid": "40sG903yz80oDFWr",`
  
  `"topic": "public.$contract_code.contract_info"`
  
  `}`
  
> 正确的订阅请求:

```json

{
  "op": "sub",
  "topic": "public.btc-usdt.contract_info",
  "cid": "40sG903yz80oDFWr"
}

```

### 请求参数

| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围           |
| ------ | ---- | ------ | -------- | -------------- |
| op | true | string | 订阅固定值为sub	 |  |
| cid | false| string | Client 请求唯一 ID	 | |
| topic | true| string | 订阅主题名称，必填 (public.$contract_code.contract_info) 订阅某个品种下的合约变动信息；$contract_code为品种代码（BTC-USDT、ETH-USDT），如果值为 * 时代表订阅所有品种; contract_code支持大小写; | |

> 返回的参数为：

```json

{
    "op":"notify",
    "topic":"public.BTC-USDT.contract_info",
    "ts":1603778748167,
    "event":"init",
    "data":[
        {
            "symbol":"BTC",
            "contract_code":"BTC-USDT",
            "contract_size":0.001,
            "price_tick":0.1,
            "settlement_date":"1603785600000",
            "create_date":"20201021",
            "delivery_time": "",
            "contract_status":1,
            "support_margin_mode": "all"
        }
    ]
}
```

### 返回参数

| 参数名称   |   是否必须  |   数据类型   |   描述   |   取值范围   |
| -------- | -------- | -------- |  --------------------------------------- | -------------- |
| op | true |  string | 操作名称，推送固定值为 notify | |
| topic | true |  string | 推送的主题 | |
| ts     | true | long    | 响应生成时间点，单位：毫秒    |     |
| event | true  | string | 通知相关事件说明 |   订阅成功返回的初始合约信息（init），合约信息字段变化触发（update），系统定期推送触发（snapshot）  |
| \<data\> |   true   |  object array   |   |   |
| symbol  | true | string  | 品种代码  | "BTC","ETH"...   |
| contract_code   | true | string  | 合约代码 |  "BTC-USDT" ...   |
| contract_size  | true | decimal | 合约面值，即1张合约对应多少标的币种（如BTC-USDT合约则面值单位就是BTC） | 10, 100... |
| price_tick  | true | decimal | 合约价格最小变动精度 | 0.001, 0.01... |
| settlement_date  | true | string  | 合约下次结算时间    | 时间戳，如"1490759594752"  |
| delivery_time  | true | string  | 交割时间（合约无需交割时，该字段值为空字符串），单位：毫秒	    |   |
| create_date   | true | string  | 合约上市日期    | 如"20180706" |
| contract_status      | true | int     | 合约状态  | 合约状态: 0:已下市、1:上市、2:待上市、3:停牌，4:待开盘、5:结算中、6:交割中、7:结算完成、8:交割完成 |
| support_margin_mode | true | string | 合约支持的保证金模式  | cross：全仓模式；isolated：逐仓模式；all：全逐仓都支持 |
| \</data\>   |      |         |        |       |

### 说明：
- 合约信息变动WS推送接口有定期推送逻辑，每60秒进行一次定期推送，由定期推送触发的数据中event参数值为“snapshot”，表示由系统定期推送触发。如果60秒内已经触发过推送，则跳过该次定期推送。
- 订阅成功时，会立即推送一条最新的合约信息，event为init。
- 订阅成功后，当合约信息任何一个字段发生变化时推送最新合约信息，多个字段同时变化时仅推送一条最新合约信息，event为update。
- 当合约状态流转为“交割完成”时，合约下次结算时间为空字符串。
- 只有状态为1：上市，才能够正常交易，其他状态不可交易；

## 【通用】取消订阅合约信息变动(免鉴权)（unsub）

#### 备注
 - 该接口支持全仓模式和逐仓模式

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`
  
  `"op": "unsub",`
  
  `"topic": "public.$contract_code.contract_info",`
  
  `"cid": "id generated by client",`
  
  `}`
 
> 正确的取消订阅请求:

```json
                                  
{                                    
  "op": "unsub",                     
  "topic": "public.BTC-USDT.contract_info",   
  "cid": "40sG903yz80oDFWr"          
}                                    
```                                  
 
### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;必填；必填；订阅主题名称，必填 (public.$contract_code.contract_info)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码; |

### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| public.*.contract_info       | public.*.contract_info       | 允许   |
| public.contract_code1.contract_info | public.*.contract_info        | 允许   |
| public.contract_code1.contract_info | public.contract_code1.contract_info | 允许   |
| public.contract_code1.contract_info | public.contract_code2.contract_info  | 不允许 |
| public.*.contract_info       | public.contract_code1.contract_info  | 不允许 |

## 【逐仓】订阅计划委托订单更新(sub)

#### 备注
 - 该接口仅支持逐仓模式。

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

  `{`
  
  `"op": "sub",`
  
  `"cid": "id generated by client",`
  
  `"topic": "trigger_order.$contract_code"`
  
  `}`
  
> 正确的订阅请求:

```json

{
  "op": "sub",
  "topic": "trigger_order.BTC-USDT",
  "cid": "40sG903yz80oDFWr"
}

```

### 请求参数

| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围           |
| ------ | ---- | ------ | -------- | -------------- |
| op | true | string | 订阅固定值为sub	 |  |
| cid | false| string | Client 请求唯一 ID	 | |
| topic | true| string | 订阅主题名称，必填 (trigger_order.$contract_code) 订阅某个品种下的合约计划委托订单更新信息；$contract_code为品种代码（BTC-USDT、ETH-USDT），如果值为 * 时代表订阅所有品种; contract_code支持大小写; | |

> **返回示例**:

```json

{
    "op":"notify",
    "topic":"trigger_order.btc-usdt",
    "ts":1603778055069,
    "event":"order",
    "uid":"123456789",
    "data":[
        {
            "symbol":"BTC-USDT",
            "contract_code":"BTC-USDT",
            "trigger_type":"ge",
            "volume":1,
            "order_type":1,
            "direction":"sell",
            "offset":"open",
            "lever_rate":10,
            "order_id":5,
            "order_id_str":"5",
            "relation_order_id":"-1",
            "order_price_type":"limit",
            "status":2,
            "order_source":"web",
            "trigger_price":15000,
            "triggered_price":null,
            "order_price":15000,
            "created_at":1603778055064,
            "triggered_at":0,
            "order_insert_at":0,
            "canceled_at":0,
            "margin_mode": "isolated",
            "margin_account": "BTC-USDT",
            "fail_code":null,
            "fail_reason":null
        }
    ]
}
```

### **返回参数说明**：

| 参数名称   |   是否必须  |   数据类型   |   描述   |   取值范围   |
| -------- | -------- | -------- |  --------------------------------------- | -------------- |
| op | true |  string | 操作名称，推送固定值为 notify | |
| topic | true |  string | 推送的主题，与订阅的入参一样 | |
| ts     | true | long    | 响应生成时间点，单位：毫秒    |     |
| uid     | true | string    | 用户uid    |     |
| event | true  | string | 通知相关事件说明 |   计划委托订单下单成功（order），计划委托撤单成功（cancel），计划委托触发成功（trigger_success），计划委托触发失败（trigger_fail）  |
| \<data\> |   true   |  object array   |   |   |
| symbol                 | true | string  | 品种代码               |                                          |
| contract_code          | true | string  | 合约代码               | "BTC-USDT" ...                          |
| trigger_type              | true | string  | 触发类型    |  ge大于等于；le小于等于   |
| volume                 | true | decimal  | 委托数量 |      |
| order_type           | true | int | 订单类型              |  1、报单     |
| direction            | true | string | 买卖方向               |             买："buy",卖："sell"          |
| offset         | true | string | 开平方向             |                                开："open",平："close"            |
| lever_rate            | true | int    | 杠杆倍数              |                         |
| order_id      | true | decimal | 计划委托单订单ID                |                                          |
| order_id_str             | true | string | 字符串类型的订单ID              |                                          |
| relation_order_id             | true | string | 该字段为关联限价单的关联字段，未触发前数值为-1  |         |
| order_price_type        | true  | string | 订单报价类型 |                  "limit":限价，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档     |
| status        | true  | int | 订单状态|    2:已提交、4:报单成功、5:报单失败、6:已撤单    |
| order_source      | true | string  | 来源        |  （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发）   |
| trigger_price         | true | decimal  | 触发价       |       |
| triggered_price         | true | decimal  | 被触发时的价格       |       |
| order_price           | true | decimal  | 委托价   |                                          |
| created_at        | true  | long | 订单创建时间 |                      |
| triggered_at        | true  | long | 触发时间 |                      |
| order_insert_at        | true  | long | 下order单时间 |                      |
| canceled_at        | true  | long | 撤单时间 |                      |
| margin_account | true | string | 保证金账户  | 比如“BTC-USDT” |
| margin_mode | true | string | 保证金模式  | isolated：逐仓模式 |
| fail_code        | true  | int | 被触发时下order单失败错误码 |                      |
| fail_reason        | true  | string | 被触发时下order单失败原因（英文） |                      |
| \</data\>   |      |         |        |       |

#### **说明**：

- 订单状态系统处理的中间态不进行推送，比如报单中和撤单中；具体通知事件说明映射如下：
   -  当订单状态流转到2（已提交），event通知事件为order（计划委托订单下单成功）；
   -  当订单状态流转到4（报单成功），event通知事件为trigger_success（计划委托触发成功）；
   -  当订单状态流转到6（已撤单），event通知事件为cancel（计划委托撤单成功）；
   -  当订单状态流转到5（报单失败），event通知事件为trigger_fail（计划委托触发失败）；
- 订阅时，单合约无法重复订阅，全合约订阅可覆盖单合约的订阅，订阅全合约后无法订阅单合约；

## 【逐仓】取消订阅计划委托订单更新（unsub）

#### 备注
 - 该接口仅支持逐仓模式。

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`
  
  `"op": "unsub",`
  
  `"topic": "trigger_order.$contract_code",`
  
  `"cid": "id generated by client",`
  
  `}`
 
> 正确的取消订阅请求:

```json
                                  
{                                    
  "op": "unsub",                     
  "topic": "trigger_order.BTC-USDT",   
  "cid": "40sG903yz80oDFWr"          
}                                    
```                                  
 
### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;必填；必填；订阅主题名称，必填 (trigger_order.$contract_code)  订阅、取消订阅某个合约代码下的计划委托订单更新信息，当 $contract_code值为 * 时代表订阅所有合约代码; |

### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| trigger_order.*       | trigger_order.*      | 允许   |
| trigger_order.contract_code1 | trigger_order.*       | 允许   |
| trigger_order.contract_code1 | trigger_order.contract_code1 | 允许   |
| trigger_order.contract_code1 | trigger_order.contract_code2  | 不允许 |
| trigger_order.*       | trigger_order.contract_code1  | 不允许 |

## 【全仓】订阅计划委托订单更新(sub)

#### 备注
 - 该接口仅支持全仓模式。

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

  `{`
  
  `"op": "sub",`
  
  `"cid": "id generated by client",`
  
  `"topic": "trigger_order_cross.$contract_code"`
  
  `}`
  
> 正确的订阅请求:

```json

{
  "op": "sub",
  "topic": "trigger_order_cross.BTC-USDT",
  "cid": "40sG903yz80oDFWr"
}

```

### 请求参数

| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围           |
| ------ | ---- | ------ | -------- | -------------- |
| op | true | string | 订阅固定值为sub	 |  |
| cid | false| string | Client 请求唯一 ID	 | |
| topic | true| string | 订阅主题名称，必填 (trigger_order_cross.$contract_code) 订阅某个品种下的合约计划委托订单更新信息；$contract_code为品种代码（BTC-USDT、ETH-USDT），如果值为 * 时代表订阅所有品种; contract_code支持大小写; | |

> **返回示例**:

```json

{
    "op":"notify",
    "topic":"trigger_order_cross.*",
    "ts":1607047088014,
    "event":"order",
    "uid":"11438787",
    "data":[
        {
            "symbol":"ETH",
            "contract_code":"ETH-USDT",
            "trigger_type":"ge",
            "volume":1,
            "order_type":1,
            "direction":"sell",
            "offset":"open",
            "lever_rate":30,
            "order_id":1882,
            "order_id_str":"1882",
            "relation_order_id":"-1",
            "order_price_type":"limit",
            "status":2,
            "order_source":"api",
            "trigger_price":90,
            "triggered_price":null,
            "order_price":90,
            "created_at":1607047088020,
            "triggered_at":0,
            "order_insert_at":0,
            "canceled_at":0,
            "fail_code":null,
            "fail_reason":null,
            "margin_mode":"cross",
            "margin_account":"USDT"
        }
    ]
}
```

### **返回参数说明**：

| 参数名称   |   是否必须  |   数据类型   |   描述   |   取值范围   |
| -------- | -------- | -------- |  --------------------------------------- | -------------- |
| op | true |  string | 操作名称，推送固定值为 notify | |
| topic | true |  string | 推送的主题，与订阅的入参一样 | |
| ts     | true | long    | 响应生成时间点，单位：毫秒    |     |
| uid     | true | string    | 用户uid    |     |
| event | true  | string | 通知相关事件说明 |   计划委托订单下单成功（order），计划委托撤单成功（cancel），计划委托触发成功（trigger_success），计划委托触发失败（trigger_fail）  |
| \<data\> |   true   |  object array   |   |   |
| symbol                 | true | string  | 品种代码               |                                          |
| contract_code          | true | string  | 合约代码               | "BTC-USDT" ...                          |
| margin_mode | true | string | 保证金模式  | cross：全仓模式； |
| margin_account | true | string | 保证金账户  | 比如“USDT” |
| trigger_type              | true | string  | 触发类型   |  ge大于等于；le小于等于    |
| volume                 | true | decimal  | 委托数量 |      |
| order_type           | true | int | 订单类型              |  1、报单     |
| direction            | true | string | 买卖方向               |             买："buy",卖："sell"          |
| offset         | true | string | 开平方向             |                                开："open",平："close"            |
| lever_rate            | true | int    | 杠杆倍数              |                         |
| order_id      | true | decimal | 计划委托单订单ID                |                                          |
| order_id_str             | true | string | 字符串类型的订单ID              |                                          |
| relation_order_id             | true | string | 该字段为关联限价单的关联字段，未触发前数值为-1  |         |
| order_price_type        | true  | string | 订单报价类型 |                  "limit":限价，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档     |
| status        | true  | int | 订单状态|    2:已提交、4:报单成功、5:报单失败、6:已撤单、7:错单     |
| order_source      | true | string  | 来源        | （system:系统、web:用户网页、api:用户API、m:用户M站、risk:风控系统、settlement:交割结算、ios：ios客户端、android：安卓客户端、windows：windows客户端、mac：mac客户端、trigger：计划委托触发）   |
| trigger_price         | true | decimal  | 触发价       |       |
| triggered_price         | true | decimal  | 被触发时的价格       |       |
| order_price           | true | decimal  | 委托价   |                                          |
| created_at        | true  | long | 订单创建时间 |                      |
| triggered_at        | true  | long | 触发时间 |                      |
| order_insert_at        | true  | long | 下order单时间 |                      |
| canceled_at        | true  | long | 撤单时间 |                      |
| fail_code        | true  | int | 被触发时下order单失败错误码 |                      |
| fail_reason        | true  | string | 被触发时下order单失败原因（英文） |                      |
| \</data\>   |      |         |        |       |

#### **说明**：

- 订单状态系统处理的中间态不进行推送，比如报单中和撤单中；具体通知事件说明映射如下：
   -  当订单状态流转到2（已提交），event通知事件为order（计划委托订单下单成功）；
   -  当订单状态流转到4（报单成功），event通知事件为trigger_success（计划委托触发成功）；
   -  当订单状态流转到6（已撤单），event通知事件为cancel（计划委托撤单成功）；
   -  当订单状态流转到5（报单失败），event通知事件为trigger_fail（计划委托触发失败）；
- 订阅时，单合约无法重复订阅，全合约订阅可覆盖单合约的订阅，订阅全合约后无法订阅单合约；

## 【全仓】取消订阅计划委托订单更新（unsub）

#### 备注
 - 该接口仅支持全仓模式。

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

### 取消订阅请求数据格式

  `{`
  
  `"op": "unsub",`
  
  `"topic": "trigger_order_cross.$contract_code",`
  
  `"cid": "id generated by client",`
  
  `}`
 
> 正确的取消订阅请求:

```json
                                  
{                                    
  "op": "unsub",                     
  "topic": "trigger_order_cross.BTC-USDT",   
  "cid": "40sG903yz80oDFWr"          
}                                    
```                                  
 
### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;必填；必填；订阅主题名称，必填 (trigger_order_cross.$contract_code)  订阅、取消订阅某个合约代码下的计划委托订单更新信息，当 $contract_code值为 * 时代表订阅所有合约代码; |

### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| trigger_order_cross.*       | trigger_order_cross.*      | 允许   |
| trigger_order_cross.contract_code1 | trigger_order_cross.*       | 允许   |
| trigger_order_cross.contract_code1 | trigger_order_cross.contract_code1 | 允许   |
| trigger_order_cross.contract_code1 | trigger_order_cross.contract_code2  | 不允许 |
| trigger_order_cross.*       | trigger_order_cross.contract_code1  | 不允许 |

# WebSocket系统状态更新接口

 - 系统状态更新订阅WS地址：wss://api.hbdm.com/center-notification

## 【通用】订阅系统状态更新

### 成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来请求数据：

  `{`
  
      `"op": "sub",`
  
      `"cid": "id generated by client",`
  
      `"topic ": "public.$service.heartbeat"`
  
  `} `

> 数据请求参数的例子：

```json

{
	"op": "sub",
	"cid": "id generated by client",
	"topic ": "public.linear-swap.heartbeat"
}
```

### **请求参数**:
| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围           |
| ------ | ---- | ------ | -------- | -------------- |
| op | true | string | 必填;订阅固定值为sub	 |  |
| cid | false| string | 选填;Client 请求唯一 ID	 | |
| topic | true| string | 必填;订阅主题名称:public.$service.heartbeat; 订阅USDT本位永续合约的系统状态信息 | |

### **sub订阅参数说明**:
| 参数名称   | 是否必须 | 类型     | 描述   | 取值范围           |
| ------ | ---- | ------ | -------- | -------------- |
| service | true | string | 业务代码	 | linear-swap：USDT本位永续 |


> **返回示例**:

```json

{
    "op": "notify",
    "topic": "public.linear-swap.heartbeat",
    "event": "init",
    "ts":1580815422403,
    "data":{
        "heartbeat": 0,
        "estimated_recovery_time": 1408076414000
    }
}

```

### **返回参数说明**：
| 参数名称   |   是否必须  |   数据类型   |   描述   |   取值范围   |
| -------- | -------- | -------- |  --------------------------------------- | -------------- | 
| op   | true | string  | 操作名称，推送固定值为 notify;    |   |
| topic   | true | string  | 推送的主题   |   |
| event   | true | string  | 通知相关事件说明   |  订阅成功返回的初始系统状态信息（init），系统状态变化触发（update） |
| ts   | true | long  | 服务端应答时间戳   |   |
| \<data\> |  |  |  | |
| heartbeat | true | int | 系统状态	 |  1是可用，0为不可用(即停服维护) |
| estimated_recovery_time | true | long |  系统预估恢复时间，单位：毫秒	 |  当系统状态为可用时，返回空值 |
| \</data\> | | |  | |

### 备注

- 这个推送由于是轮询判断状态的，所以推送可能存在1—2秒的延迟。

# WebSocket附录

## 操作类型（OP）说明

| 类型   | 描述                 |
| ------ | -------------------- |
| ping   | ⼼跳发起(server)     |
| pong   | 心跳应答             |
| auth   | 鉴权                 |
| sub    | 订阅消息             |
| unsub  | 取消订阅消息         |
| notify | 推送订阅消息(server) |

## 主题（topic）类型说明

| 类型           | 使用操作类型 | 描述                                                         |
| -------------- | ------------ | ------------------------------------------------------------ |
| orders.$contract_code | sub,unsub    | 订阅、取消订阅指定交易易对的订单变更更消息，当 contract_code 值为 * 时代表订阅所有交易易对 |

## 响应码（Err-Code）说明

| 返回码 | 返回描述                                 |
| ------ | ---------------------------------------- |
| 0      | Request successfully.                    |
| 2001   | Invalid authentication.                  |
| 2002   | Authentication required.                 |
| 2003   | Authentication failed.                   |
| 2004   | Number of visits exceeds limit.          |
| 2005   | Connection has been authenticated.       |
| 2007   | You don’t have access permission as you have not opened contracts trading.|
| 2010   | Topic error.                             |
| 2011   | Contract doesn't exist.                  |
| 2012   | Topic not subscribed.                    |
| 2013   | Authentication type doesn't exist.       |
| 2014   | Repeated subscription.                   |
| 2020   | This contract does not support cross margin mode.| 
| 2021   | Illegal parameter margin_account.| 
| 2030   | Exceeds connection limit of single user. |
| 2040   | Missing required parameter.              |


<br>
<br>
<br>
<br>














