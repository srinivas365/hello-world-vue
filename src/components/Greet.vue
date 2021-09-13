<template>
    <h2>{{name}} : {{heroName}}</h2>
</template>

<script>
export default {
   name:"Greet",
   props:[
       'name',
       'heroName',
   ]

}
</script>

<style scoped>

</style>
