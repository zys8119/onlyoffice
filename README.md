# onlyoffice 相关搭建注意事项

版本 7.4.1-36

### owncloud默认账号密码

admin/admin

### 通过nodejs 生成 token

```javascript
var jwt = require("jsonwebtoken");
console.log(jwt.sign(JSON.stringify({
    "document": {
        "fileType": "pdf",
        "key": "Khirz6zTPdfd7",
        "title": "Example Document Title.docx",
        "url": "http://192.168.110.140:3000/%E5%8D%95%E4%BD%8D%E8%87%AA%E6%9F%A5(1).pdf"
    },
    "documentType": "word",
    "editorConfig": {
        mode:'view'
    },
}), 'secret'))
```

### 设置私有ip白名单限制

修改 /etc/onlyoffice/documentserver/local.json

```json5
{
  "services": {
    "CoAuthoring": {
      "request-filtering-agent" : {
        "allowPrivateIPAddress": true,
        // 你的私有ip
        "allowMetaIPAddress": "192.168.110.140"
      }
    }
  }
}
```

### 重新启动服务以使配置更改生效

For RPM/DEB packages: 对于RPM/DEB程序包：

```shell
systemctl restart ds-*
```

For Docker: 对于Docker：

```shell
supervisorctl restart all
```

### welcome 页面可开启演示例子

[演示地址](http://localhost:8080/welcome/)


### 字体加载脚本

```
  documentserver-generate-allfonts.sh
```
### 注意项

* 不需要云的时候local.json 为 控对象 {}
* docker-compose1.yml 带有云服务
* docker-compose.yml 仅服务