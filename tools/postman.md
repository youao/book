# 添加cookie

一般项目很多接口请求都需要先验证登录，而登录信息会保存到本地cookie

测试的时候在 `header` 设置处粘贴浏览器的cookie即可完成添加



# 环境变量

添加环境变量后，用 `{{}}` 包裹使用

如： `{{url}}`



# 设置返回数据默认显示格式为JSON

`postman` 返回数据默认显示为 `html` 

调整为 `json` 步骤：

- 设置 - settings
- 通用面板（General） 找到选项 language detection
- 选择 json
