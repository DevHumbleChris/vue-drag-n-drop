<script>
import { ref } from 'vue';

export default {
  setup () {
    const items = ref([
      { id: 0, title: 'Item A', list: 1},
      { id: 1, title: 'Item B', list: 1},
      { id: 2, title: 'Item C', list: 2}
    ])

    const getList = (list) => {
      return items.value.filter((item) => item.list === list)
    }

    return {
       getList
    }
  }
}
</script>

<template>
  <main>
    <h1>Vue 3 Drag N Drop</h1>
  </main>
</template>

<style scoped>
</style>
