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