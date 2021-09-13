<template>
    <h2>Component C we got data from {{username}}</h2>
</template>

<script>
export default {
   name:"CompC",
   inject:['username']
}
</script>

<style scoped>

</style>
