# 快速体验一次SSR

### 官方文档
英文：https://nuxtjs.org/  
中文：https://zh.nuxtjs.org/

### 新建项目
```
mkdir nuxtjs-demo
cd nuxtjs-demo
```
### 初始化项目
生成`package.json`文件
```
npm init
```
### 安装依赖
- nuxt(主框架)
- axios(http请求工具)
```
npm install nuxt --save
npm install axios --save
```
### 配置运行脚本
```
{
    "scripts": {
        "dev": "nuxt",
        "build": "nuxt build",
        "start": "nuxt start"
    }
}
```
### 新建页面目录
```
mkdir pages
cd pages
```
### 新建一个页面
页面路径：`/pages/index.vue`
页面代码：
```
<template>
    <h1>{{productName}}</h1>
</template>

<script>
    export default {
        name: "index",
        data() {
            return {
                productName: '感冒药'
            }
        },
    }
</script>

<style scoped>

</style>
```
### 完整实例代码
```
<template>
    <h1>{{productName}}</h1>
</template>

<script>

    function getQueryParams(obj) {
        let params = [];
        for (let key in obj) {
            params.push(`${key}=${obj[key]}`)
        }
        return params.join('&')
    }

    let params = getQueryParams({
        ...data
    });

    import axios from 'axios';

    export default {
        name: "index",
        data() {
            return {
                productName: ''
            }
        },
        async asyncData() {
            let productName = '';
            await axios.post('https://www.abc.com/', params)
                .then((res) => {
                    productName = res.data.data.product_info.productName;
                })
            return {productName}
        },
        head() {
            return {
                title: this.productName,
                meta: [
                    {hid: 'keywords', name: 'keywords', content: `${this.productName}`},
                    {hid: 'description', name: 'description', content: `${this.productName}`}
                ]
            }
        }
    }
    
</script>

<style scoped>

</style>
```













