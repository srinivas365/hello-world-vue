<template>
  <div class="card">
      <slot name="header"></slot><br>
      <slot></slot><br>
      <slot name="footer"></slot><br>
  </div>
</template>

<script>
export default {
    name:"Card",
}
</script>

<style>
.card{
    border:1px solid;
    margin: 5px;    
}
</style>