<template>
  <div style="height: 40px; border: 1px solid red;" :vid="props.item.id">
    {{props.item.value}}
  </div>
</template>
<script setup>
  import { defineProps } from 'vue'
  const props = defineProps({
    item: Object
  })
</script>