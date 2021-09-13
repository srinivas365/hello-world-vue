<template>
    <div>
        <h2>Component B</h2>
        <CompC/>
    </div>
</template>

<script>
import CompC from './CompC.vue'
export default {
   name:"CompB",
   components:{
       CompC
   }
}
</script>

<style scoped>

</style>
