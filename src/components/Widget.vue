<template>
  <div class="widget">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'Widget',
  data () {
    return {
      
    }
  }
}
</script>

<style scoped>
  .widget {
    background: #ffffff;
    padding: 15px;
    margin-bottom: 15px;
    border-radius: 4px;
  }
  .widget__titulo {
      font-size: 20px;
      font-weight: bold;
      margin-bottom: 15px;
    }
</style>
