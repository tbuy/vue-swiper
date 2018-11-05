<template>
    <div class="demo">
        <scrollText :content="content" height="40px"></scrollText>
    </div>
</template>
<script>
    import scrollText from '../components/scrollText.vue'
    export default {
        components: {
            scrollText
        },
        data() {
            return {
                content: "事件原理，闭包，调用栈，Promise，ES6， 工程化，webpack, 性能优化，跨域"
            }
        }
    }

</script>
<style>
.demo {
    width: 500px;
    border: 1px solid #ccc;
    margin: 50px auto;
    line-height: 40px;
}
</style>
