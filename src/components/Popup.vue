<template>
  <div>
    <h2>This is a popup window</h2>
    <button @click="$emit('close',{name:'srinivas',age:31})">close</button>
  </div>
</template>

<script>
export default {
    name:'Popup',
    emits:['close']
};
</script>

<style>
</style>