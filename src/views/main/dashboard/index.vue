<template>
  <div class="box">
    <Card />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Card from './components/card/index.vue'
export default defineComponent({
  components: {
    Card,
  }
})
</script>

<style lang="scss" scoped>
  .box {
    padding: 15px;
  }
</style>