<template>
    <div>
        <h2 v-bind="$attrs">{{title}}</h2>
        <h3>{{price}}</h3>
        <p>Description:{{desc}}</p>
    </div>
</template>

<script>
export default {
   name:'Article',
   props:{
       title:String,
       desc:String,
       price:Number,
   },
   inheritAttrs:false
}
</script>

<style scoped>

</style>