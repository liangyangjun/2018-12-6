```js
      
[
    {
        "orderId":1976,
        "dataList":{
            "orderProductId":2833,
            "deliverQuantity":20
        }
    },
    {
        "orderId":2358,
        "dataList":{
            "orderProductId":3284,
            "deliverQuantity":30
        }
    },
    {
        "orderId":2358,
        "dataList":{
            "orderProductId":3285,
            "deliverQuantity":40
        }
    }
]
```

#将上图数据格式转换为下图数据格式（以ID去重，并将dataList数据合并）

```js
[
    {
        "orderId":1976,
        "dataList":[
            {
                "orderProductId":2833,
                "deliverQuantity":20
            }
        ]
    },
    {
        "orderId":2358,
        "dataList":[
            {
                "orderProductId":3284,
                "deliverQuantity":30
            },
            {
                "orderProductId":3285,
                "deliverQuantity":40
            }
        ]
    }
]
```

代码如下

```js
function flatten(list) {
    list.forEach((item, index) => {
        if (Array.isArray(item.dataList)) {
            item.dataList.forEach((v) => {
                list.push({
                    orderId: item.orderId,
                    dataList:{
                        orderProductId: v.orderProductId, 
                        deliverQuantity: v.deliverQuantity
                    }
                })
            })
            list.splice(index, 1)
        }
    })
    return list
}
let arr = [
    {
        "orderId":1976,
        "dataList":{
            "orderProductId":2833,
            "deliverQuantity":20
        }
    },
    {
        "orderId":2358,
        "dataList":{
            "orderProductId":3284,
            "deliverQuantity":30
        }
    },
    {
        "orderId":2358,
        "dataList":{
            "orderProductId":3285,
            "deliverQuantity":40
        }
    }
]



flatten(arr)

//expect export  图2结果
```

