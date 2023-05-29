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

    const startDrop = (event, item) => {
      event.dataTransfer.dropEffect = 'move'
      event.dataTransfer.effectAllowed = 'move'
      event.dataTransfer.setData('itemID', item.id)
    }

    const onDrop = (event, list) => {
      const itemID = event.dataTransfer.getData('itemID')
      const item = items.value.find(item => item.id == itemID)
      item.list = list
    }

    return {
       getList,
       startDrop,
       onDrop
    }
  }
}
</script>

<template>
  <main>
    <h1>Vue 3 Drag N Drop</h1>

    <div @drop="onDrop($event, 1)" @dragenter.prevent @dragover.prevent class="drop-zone">
      <div @dragstart="startDrop($event, item)" draggable="true" v-for="item in getList(1)" :key="item.id" class="drag-el">{{ item.title }}</div>
    </div>
    <div @drop="onDrop($event, 2)" @dragenter.prevent @dragover.prevent class="drop-zone">
      <div @dragstart="startDrop($event, item)" draggable="true" v-for="item in getList(2)" :key="item.id" class="drag-el">{{ item.title }}</div>
    </div>
  </main>
</template>

<style scoped>
main {
  max-width: 40rem;
  margin: auto;
  text-align: center;
}

.drop-zone {
  width: 50%;
  margin: 50px auto;
  background-color: rgb(199, 193, 193);
  padding: 10px;
}
.drag-el {
  background-color: brown;
  padding: 5px;
  margin: 10px;
  color: white;
}
</style>
