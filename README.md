# myDroplist
可以传默认值或者接口请求的下拉（样式需自行编写）

使用说明：

1. 需引入jquery,然后引入本drop.js
2. 兼容ie需引入es6（本插件使用了promise）的polyfill相应插件，如 “https://cdn.polyfill.io/v2/polyfill.min.js”
3. 启动插件需要严格按照格式传递相应参数

本插件使用表单元素select，目的为了简化取值，控件元素自定义name值；接口参数名称自定义；接口返回值状态判断及接口返回自定义参数值名称。e.g.

1.不请求接口直接传下拉数据

		`<div id="myDrop"></div>`
		`var data = {
				'title': '我的',  //droplist主标题
				'placeholder': '请选择', //droplist默认显示
				'keyword': 'id',  //droplist下拉表点击条目，需获取的关键字作为select的value值
				'value': 'value',  //droplist下拉表点击条目展示用的文字
				//'order': 'key',	//droplist下拉表可能需要展示的另一个文字，如编号等
				'data': {  //droplist列表数据
					'one': [{  //各数组的key值作为该select的name值，如本条数据生成select的name值为one
						'key': '001',
						'value': '北京北京北京北京',
						'id': '001'
					},{
						'key': '002',
						'value': '天津',
						'id': '002'
					}],
					'two': [{
						'key': '002',
						'value': '天津',
						'id': '002'
					},{
						'key': '001',
						'value': '北京',
						'id': '001'
					}],
					'three': [{
						'key': '002',
						'value': '天津',
						'id': '002'
					},{
						'key': '001',
						'value': '北京',
						'id': '001'
					}],
					'four': [{
						'key': '002',
						'value': '天津',
						'id': '002'
					},{
						'key': '001',
						'value': '北京',
						'id': '001'
					}]
				}
			}`
			`$("#myDrop").drop(data);`

2.下拉列表数据需要通过接口调用并且具有依赖关系，如区域联动

			`<div id="myDrop"></div>`
			`var data = {
				title: 'mydrop', //droplist主标题
				ajaxUrls: 'http://10.1.3.221:1000/api/tableDatalist,http://10.1.3.221:1000/api/tableDatalist', //droplist获取接口下拉表数据需用到的接口地址，需按顺序填写，用“,”连接，e.g. a,b,c
				ajaxMethods: 'get', //droplist接口对行请求方式，与ajaxUrls严格一一对应或者统一请求方式，e.g.["post","get"]或者"post"
				ajaxCompNames: ["province","city"], //droplist下拉控件的name属性值，与ajaxUrls必须严格一一对应，e.g.["a","b"]
				ajaxPramas: ["","province"], //droplist接口请求参数名，与ajaxUrls必须严格一一对应（如果第一个接口不需要参数需传空），e.g.["","a","b"]
				keyword: 'id', //droplist下拉表点击条目，需获取的关键字，e.g. id
				value: 'province', //droplist下拉表点击条目展示用的文字， e.g. value
				order: 'id', //droplist下拉表可能需要展示的另一个文字，如编号等
				successKey: 'code', //droplist下拉表接口请求成功标志，e.g. code:0 code
				successCode: '0', //droplist下拉表接口请求成功标志，e.g. code:0 0
				successData: 'data', //droplist下拉表接口请求成功标志，e.g. data
			}`
			`$("#myDrop").drop(data);`
