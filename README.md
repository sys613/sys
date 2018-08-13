# 接口API
订单			
	api	返回值说明	备注
币安	/api/v1/depth	出价（价格 数量） 问价（价格 数量）	限制条数 为1000
比特儿（交易市场订单）	 https://data.gateio.io/api2/1/marketinfo	价格精度 最小下单量 交易费	
交易行情参数			
			
			
	api	返回值说明	备注
火币	/market/tickers	"open":日K线 开盘价 "close":日K线 收盘价"low":日K线 最低价"high":日K线 最高价"amount":24小时成交量 "count":24小时成交笔数"vol"24小时成交额"symbol":交易对	获取所有交易行情 当交易对尚未产生成交时  其他值为null
比特儿	https://data.gateio.io/api2/1/tickers	baseVolume: 交易量 high24hr:24小时最高价 highestBid:买方最高价 last:最新成交价 low24hr:24小时最低价lowestAsk:卖方最低价 percentChange:涨跌百分比 quoteVolume: 兑换货币交易量	每10秒刷新一次
			/ticker/[CURR_A]_[CURR_B] 为单行交易量
			[CURR_A] and [CURR_B] 为您需要查看的币种.
市场深度			
			
	api	返回值说明	备注
火币	/market/depth	"tick": {"id": 消息id,"ts": 消息生成时间，单位：毫秒,"bids": 买盘,[price(成交价), amount(成交量)], 按price降序,"asks": 卖盘,[price(成交价), amount(成交量)], 按price升序}	请求参数 symbol:交易对 type:step0, step1, step2, step3, step4, step5（合并深度0-5）；step0时，不合并深度
OKEx（合约深度）	https://www.okex.com/api/v1/future_depth.do	asks :卖方深度 bids :买方深度	请求参数 symbol  contract_type 合约类型( this_week:当周 next_week:下周 quarter:季度) size :最大值 200 merge：0 (不合并) 1(合并)
OKEx（币币深度）	https://www.okex.com/api/v1/depth.do	asks :卖方深度 bids :买方深度	请求参数 symbol  size :最大值 200 
比特儿	https://data.gateio.io/api2/1/orderBooks	asks :卖方深度 bids :买方深度	orderBook/[CURR_A]_[CURR_B]  当前市场深度 
			[CURR_A] and [CURR_B] 为您需要查看的币种.
历史成交记录			
			
	api	返回值说明	备注
火币	/market/depth 获取单个交易对最新成交	"tick": {"id": 消息id,"ts": 最新成交时间,"data": [{"id": 成交id,"price": 成交价钱,"amount": 成交量,"direction": 主动成交方向,"ts": 成交时间}]}	请求参数：symbol(交易对)
	 /market/history/trade 单个交易对批量成交记录		请求参数：symbol(交易对) size：最高值 2000
币安	/api/v1/trades	[{"id": 28457,"price": 价格,"qty": 数量,"time": 时间戳,"isBuyerMaker": true,"isBestMatch": true}]	symbol  limit：Default 500; max 1000. 最近的交易
	/api/v1/historicalTrades		symbol limit:Default 500; max 1000.  fromId ：交易id 没有时 默认得到最近的
OKEx（合约交易记录）	https://www.okex.com/api/v1/future_trades.do	amount：交易数量date_ms：交易时间(毫秒)date：交易时间price：交易价格tid：交易IDtype：交易类型	请求参数：symbol contract_type合约类型( this_week:当周 next_week:下周 quarter:季度)
OKEx（币币交易记录）	https://www.okex.com/api/v1/trades.do	date:交易时间date_ms:交易时间(ms)price: 交易价格amount: 交易数量tid: 交易生成ID type: buy/sell	请求参数：symbol since ：tid:交易记录ID (最多60条)
			不是必填 默认返回最近成交60条数据 
比特儿	https://data.gateio.io/api2/1/tradeHistory/[CURR_A]_[CURR_B]	amount: 成交币种数量 date: 订单时间 rate: 币种单价 total: 订单总额 tradeID: tradeIDtype: 买卖类型, buy买 sell卖	返回最新80条历史成交记录
	https://data.gateio.io/api2/1/tradeHistory/[CURR_A]_[CURR_B]/[TID]		返回从[TID]往后的最多1000历史成交记录：
交易市场k线数据			
			
	api	返回值说明	备注
火币	 /market/history/kline	status ：请求处理结果  ts：响应生成时间点，单位：毫秒 tick：KLine 数据  ch：数据所属的 channel，格式： market.$symbol.kline.$period 	symbol：交易对  period ：k线类型  size：获取数量 （默认150 最大1200）
		 data说明：id": K线id,"amount": 成交量,"count": 成交笔数,"open": 开盘价,"close": 收盘价,当K线为最晚的一根时，是最新成交价"low": 最低价,"high": 最高价,"vol": 成交额, 即 sum(每一笔成交价 * 该笔的成交量)	
币安	/api/v1/klines	开盘时间戳，开，高，低，关，交易量 ，关盘时间戳，Quote asset volume，Number of trades，Taker buy base asset volume，Taker buy quote asset volume	symbol interval:间隔 startTime endTime limit:Default 500; max 1000.
OKEx(合约)	https://www.okex.com/api/v1/future_kline.do	时间戳，开，高，低，交易量，交易量转化BTC或LTC数量	symbol type：时间  contract_type:合约类型（this_week:当周 next_week:下周 quarter:季度） size：指定获取数据的条数 since：时间戳 （返回该时间戳以后的数据）
OKEx(币币)	https://www.okex.com/api/v1/kline.do	时间戳，开，高，低，收，交易量	symbol type：时间 size：指定获取数据的条数 since：时间戳 （返回该时间戳以后的数据）
			每个周期数据条数2000左右
比特儿	https://data.gateio.io/api2/1/candlestick2/[CURR_A]_[CURR_B]?group_sec=[GROUP_SEC]&range_hour=[RANGE_HOUR]	time: 时间戳 volume: 交易量 close: 收盘价 high: 最高价 low: 最低价 open: 开盘价	 [CURR_A] 和 [CURR_B] 为您需要查看的币种，GROUP_SEC 和 RANGE_HOUR 替换为需要获取的时间区域.
获取行情(Ticker)			
			
	api	返回值说明	备注
火币 （最优聚合行情）	/market/detail/merged	"tick": {"id": K线id,"amount": 成交量,"count": 成交笔数,"open": 开盘价,"close": 收盘价,当K线为最晚的一根时，是最新成交价"low": 最低价,"high": 最高价,"vol": 成交额, 即 sum(每一笔成交价 * 该笔的成交量)"bid": [买1价,买1量],"ask": [卖1价,卖1量] }	symbol:交易对
币安	/api/v3/ticker/price（价格行情）	{"symbol": "LTCBTC", "price": "4.00000200 }	symbol 不存在则 返回全部
	/api/v1/aggTrades	[{"a": 聚合id, "p":价格 "q": "数量",y"f": 第一个交易id，"l":最后一个交易id, "T":时间戳，"m": true,"M": true（价格是否最合适）}]	symbol  fromId;聚合交易id  startTime:开始时间  endTime ;结束时间  limit：Default 500; max 1000. 
			结束时间大于开始时间1小时
	/api/v3/ticker/bookTicker（最佳买入卖出）	{"symbol": "LTCBTC","bidPrice": "4.00000000","bidQty": "431.00000000","askPrice": "4.00000200","askQty": "9.00000000"}	symbol 不存在则 返回全部
OKEx （合约行情）	https://www.okex.com/api/v1/future_ticker.do	buy:买一价contract_id:合约IDhigh:最高价last:最新成交价low:最低价sell:卖一价unit_amount:合约面值vol:成交量(最近的24小时)	请求参数：symbol contract_type：合约类型（this_week:当周 next_week:下周 quarter:季度）
OKEx （币币行情）	https://www.okex.com/api/v1/ticker.do	date: 返回数据时服务器时间buy: 买一价high: 最高价last: 最新成交价low: 最低价sell: 卖一价vol:成交量(最近的24小时)	请求参数：symbol
比特儿（交易市场行情）	https://data.gateio.io/api2/1/marketlist	symbol : 币种标识 name: 币种名称 name_en: 英文名称 name_cn: 中文名称 pair: 交易对 rate: 当前价格 vol_a: 被兑换货币交易量 vol_b: 兑换货币交易量 curr_a: 被兑换货币 curr_b: 兑换货币 curr_suffix: 货币类型后缀 rate_percent: 涨跌百分百trend: 24小时趋势 up涨 down跌supply: 币种供应量 marketcap: 总市值plot: 趋势数据	
24小时成交量数据			
	api	返回值说明	备注
火币	/market/detail	"tick": {"id": 消息id,"ts": 24小时统计时间,"amount": 24小时成交量,"open": 前推24小时成交价,"close": 当前成交价,"high": 近24小时最高价,"low": 近24小时最低价,"count": 近24小时累积成交数,"vol": 近24小时累积成交额, 即 sum(每一笔成交价 * 该笔的成交量)}	请求参数 symbol:交易对
币安	/api/v1/ticker/24hr	symbol ，priceChange， priceChangePercent， weightedAvgPrice， prevClosePrice， lastPrice ，lastQty ，bidPrice ，askPrice ，openPrice， highPrice ，lowPrice， volume ，quoteVolume ，openTime， closeTime， firstId ，lastId， count	symbol  不存在 则返回全部

