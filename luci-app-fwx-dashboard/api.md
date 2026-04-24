

## 接口定义

### 获取dashboard接口

- 接口名称: `get_dashboard_common`

- object说明
system_status: 系统信息，在页面中可以分为系统信息和系统状态，根据字段名称可以看出区分
比如system_status.model表示型号，而system_status.cpu表示cpu占用

network_status： 网络状态

active_app: 活跃app列表

interface_traffic： 接口流量统计


- 返回实例  
```
{
		"system_status":{
			"model":"Cudy Tr3000",
			"version": "24.10.4",
			"kernel_version":"6.1.99",
			"uptime": 188282,
			"cpu": "12",
			"total_mem": 256,
			"used_mem": 128,
			"cpu_temp": 50,
			"wifi_temp": 40,
			"connections":182,
			"client_num": 12,
			"flow":{
				"today_up": 13772,
				"today_down": 6529
			}
		},

		"network_status":{
			"internet": 1,
			"work_mode": 1,
			"lan":{
				"ip": "192.168.1.1",
				"mask":  "255.255.255.0",
				"gateway": "192.168.1.1",
				"dns":["192.168.1.1", "8.8.8.8"]
			},
			"wan":{
				"ip": "192.168.1.1",
				"mask":  "255.255.255.0",
				"gateway": "192.168.1.1",
				"dns":["192.168.1.1", "8.8.8.8"]
			}
		},
		"active_app":{
				"total": 10,
				"list":[
					{
						"id":1001,
						"name": "weixin"
					},
					{
						"id":1002,
						"name": "qq"
					}
				]
		},
		
		"interface_traffic":{
			"interface":"wan",
			"traffic": [
				{
					"up":1001,
					"down" 18828
				},
				{
					"up": 2772,
					"down": 28828
				}
			]
		}
}

```

---

### 获取用户流量Top8接口

- 接口名称: `get_top_users`

- 请求参数

| 参数     | 类型 | 必填 | 说明                                       |
|--------|----|----|------------------------------------------|
| period | 整数 | 否  | 统计天数，可选值：1、3、7、30，默认值为 1               |
| limit  | 整数 | 否  | 返回用户数量上限，固定传 8                          |

- 返回实例
```json
{
	"period": 7,
	"total_count": 2,
	"users": [
		{
			"mac": "AA:BB:CC:DD:EE:01",
			"ip": "192.168.1.10",
			"hostname": "my-phone",
			"nickname": "小明的手机",
			"up_bytes": 1048576,
			"down_bytes": 5242880,
			"total_bytes": 6291456
		},
		{
			"mac": "AA:BB:CC:DD:EE:02",
			"ip": "192.168.1.11",
			"hostname": "laptop",
			"nickname": "",
			"up_bytes": 524288,
			"down_bytes": 2097152,
			"total_bytes": 2621440
		}
	]
}
```

> **注意：** 旧接口 `get_daily_top_users`（仅返回今日数据）保留以兼容旧版本，建议新开发使用 `get_top_users`。