# 使用步骤

## 1. 初始化package.json

在根目录启动命令行（package.json所在的位置，下同）

（需要安装node.js）

```shell
npm init
```

## 2. 安装环境 

```shell
npm install grunt --save-dev

npm install swagger-vue --save-dev
```

## 3. 将接口描述文件放在api目录中 

将swagger.json的接口描述文件放在api目录中，名称必须为swagger.json，yaml的描述文件需要转换为json格式，可以借助swagger-editor另存为功能转换（https://editor2.swagger.io/）

## 3. 生成客户端的接口文件

```shell
grunt vue
```

## 4. 接口文件使用方法

### 4.1 将生成的vue-api-client放入webpack
以src/assets/js为例子
### 4.2 import引入vue中
位置：vue的script的export default之前
```
import {getPetById} from "@assets/js/vue-api-client";
```
### 4.3 在methods中使用
```
methods: {
    getPet() {
        getPetById({
            $domain: '/pet', //这里配置跨域的代理地址，站点加项目的路径
            $config: {
                //配置Request头信息
                header: {
                    'Content-Type': 'application/json'
                }
            },
            petId: '10086', //路径的参数，in: "path" "query" "formData"
            body: {
                //in: "body"，json形式传送时封装的入参对象
                age: '10',
                sex: 'x',
            }
        }).then(resp => {
            let data = resp.data; //后台返回的封装信息
        });
    },
}
```

