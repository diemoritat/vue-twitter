<template>
  <div :class="className">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
  props: {
    position: {
      type: String,
      required: false
    }
  },
  computed: {
    className() {
      return `dashboard dashboard__${ this.position }`
    }
  }
}
</script>

<style scoped>
.dashboard {
  float: left;
  width: 30%;
}
@media (max-width: 610px) {
  .dashboard {
    width: 100%;
  }
}
@media (min-width: 611px) {
  .dashboard__center {
    width: calc(70% - 15px);
    margin-left: 15px;
    float: right;
  }
}
</style>
