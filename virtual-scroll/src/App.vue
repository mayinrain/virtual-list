<template>
<!-- size:每个item的高度 -->
<!-- remain:可视个数 -->
<!-- items:传入的数据 -->
  <VirtualList :size="40" :remain="12" :items="items" class="virtual-list" :columns="3" :preRender="3">
    <template #item="item">
      <Item :item="item.item"></Item>
    </template> 
  </VirtualList>
</template>
：
<script setup>
import VirtualList from "./components/virtualList.vue"
import Item from './components/item.vue'
import { ref } from 'vue'
const items = ref([])
for(let i = 0; i < 10000; i++) {
  items.value.push({
    id:i,
    value:`${i}`
  })
}
// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/master/active-rfcs/0040-script-setup.md
</script>

<style lang="less">
#app {
  position: relative;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 30%;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
