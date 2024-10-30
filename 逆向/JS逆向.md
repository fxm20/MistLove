# JS逆向





AES算法

```
const CryptoJs = require('crypto-js');
```





导入CryptoJs

```
const CryptoJs=require('crypto-js')		//npm install crypto-js
```

可以通过pyexecjs2执行js文件

吐出方法  

方法名.tostring

1. md5

   ```javascript
   const CryptoJs = require('crypto-js');
   encrypt1=CryptoJs.MD5('appId=5053&t=1729599074520&cityCode=110100&pageIndex=2&pageSize=12&categoryCode=138&order=0750F82C2-D8F6-49F6-878C-1E7EBEBC8DA2').toString();
   console.log(encrypt1);
   ```
   

## 关于头部加密



