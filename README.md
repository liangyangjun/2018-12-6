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

let newArr = [],
    data = {};
arr.map(value => {
    let first = value.orderId;
    if (!data[first]) {
        data[first] = [];
    }
    data[first].push(value.dataList);
});
Object.keys(data).forEach((orderId)=>{
    let obj = {orderId: "", dataList: []};
    obj.orderId = orderId;
    obj.dataList = data[orderId];
    newArr.push(obj);
})

console.log(newArr)
//expect export  图2结果
```

