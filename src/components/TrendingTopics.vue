<template>
  <div class="trending">
      <h2 class="trending__title widget__title">Trending Topics: {{ area }}</h2>
      <ol class="trending__list">
          <li><a>#bagulhos</a></li>
          <li><a>#bagulheiros</a></li>
      </ol>
  </div>
</template>

<script>
export default {
  name: 'TrendingTopics',
  props: {
    area: {
      type: String,
      required: false,
      default: 'Brasil'
    }
  }
}
</script>

<style scoped>
  .trending__list {
    list-style: none;
  }
</style>
