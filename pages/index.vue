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
        provinceid: '1',
        province: '1',
        provincename: '上海',
        tradername: 'yw_app',
        trader: 'h5',
        closesignature: 'yes',
        signature_method: 'md5',
        timestamp: '1593247103157',
        signature: '****',
        siteid: '9',
        itemId: '972419',
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
            await axios.post('https://gateway.fangkuaiyi.com/product/v1/product/getProductBaseInfo', params)
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