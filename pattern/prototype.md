# 协议
## 1、请求：需要进行签名
惠商+微信公众号受理平台与第三方平台采用公网连接，一方向另一方发送请求数据，并同步等待另一方处理完毕之后返回的响应数据，报文采用标准的http协议包格式(标准http包头+JSON包体)
包体示例：
```json
{
	"amount": "8888",
	"goodsInfo": "真实的全流程测试",
	"sign": "FloG4isf+mSskb4AcF8jcNjX7zbbx1UUGfKUHUt7DWfvF5U1MxX4JcMmGjCnF+epvCjCKQnT0jodoahcCZ7Eqgiyzj/GQtO7JyAtjxEvU8GwzdkrsErpe+IzfACBDbn7N6+mSKJ5DY+txicsyZh/97ZxOq4SJIbI1FyMY37kPgU=",
	"goodsId": "真实的全流程测试",
	"mediaNo": "6255552359041786959",
	"payType": "WX",
	"proxyId": "0048",
	"subMerId": "30000095",
	"mediaType": "05"
}
```
注意：
1. 报文具体内容包含在context内
2. 参数的排列顺序应该按照接口中定义的参数名的顺序进行排列

## 2、响应：需要进行验签

包体示例：
```json
{
	"sign": "KLF/FfpQpff7SKw6x+3hyc8fp8UMtvaHcGeMX0hcJtM/IvU6LMQbuF0EEMbL0pud15uc8q0+wTBF4Dbt2VV6lsqG3H4cfFQSmf3k8Q2Tn4Zx9tw91k0fmqHh5kAR2ynjCdm9Bxl9Vjts5LH6mWj4rvqUTYQeW1RxJHEAJmvSOpQ=",
	"payAmount": "000000008888",
	"amount": "8888",
	"retCode": "0000",
	"tradeNo": "1709964000006324",
	"partnerOrderId": "HSAPI201709141745447451850",
	"Memo": "交易成功",
	"paySeq": "418813867389091730800013",
	"platDate": "20170914",
	"coupAmount": "0",
	"payDay": "20170914"
}
```
注意：
1. 交易的结果无论成功还是失败，响应的http报文头status均为 200OK；
2. 报文体为JSON格式的UTF-8编码字节流
3. 参数的排列顺序应该按照接口中定义的参数名的顺序进行排列，没有值的参数也需要传递，值指定为空串。



