<template>
  <!-- 视窗 -->
  <div class="viewport" @scroll="handleScroll" ref="viewport">
    <!-- 占位区域 -->
    <div class="scroll-bar"></div>
    <!-- 真实渲染内容 -->
    <div class="scroll-list" :style="{transform: `translate3d(0, ${offset}px, 0)`}">
      <div v-for="(item,index) in visibleItems" :key="index">
        <div class="real-item">
          <slot :item="item" name="item"></slot>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { defineProps, ref, computed } from 'vue'
const props = defineProps({
  size: Number, // 每项高度
  remain: Number, // 可见区域个数
  items: Array,  // 数据
  columns: Number, // 展示列数
  preRender:Number // 预渲染的个数
})
// 计算视窗高度
const viewPortHeight = ref()
viewPortHeight.value = props.size * (props.remain / props.columns) + 'px' // 传入的可视个数一定要能被列数整除
// 计算占位区域高度
const scrollBarHeight = ref()
scrollBarHeight.value = Math.ceil(props.items.length / props.columns) * props.size + 'px'
// 根据展示列数计算每个item占用宽度
const itemWidth = ref()
itemWidth.value = `${100 / props.columns}%`
// start为真实渲染数据在列表中的开始索引
// end为真实渲染数据在列表中的结束索引
// offset为真实数据所在位置相对于占位区域顶部的偏移量
const start = ref(0)
const end = ref(0)
const offset = ref(0)
end.value = props.remain
const visibleItems = computed(() => props.items.slice(start.value - Math.min(start.value, props.preRender), end.value + Math.min(props.items.length - end.value, props.preRender)))
// viewport的ref
const viewport = ref()
// 滚动时计算start, end, offset
const handleScroll = () => {
  let scrollTop = viewport.value.scrollTop
  start.value = Math.floor(scrollTop / props.size) * props.columns
  end.value = start.value + props.remain
  offset.value = start.value / props.columns * props.size - props.size * Math.min(start.value, props.preRender) / props.columns
}
// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/master/active-rfcs/0040-script-setup.md
</script>
<style lang="less">
  .viewport {
    overflow-y: scroll;
    height: v-bind(viewPortHeight);
    position: relative;
    width: 100%;
    .scroll-bar {
      height: v-bind(scrollBarHeight);
    }
    .scroll-list {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      .real-item {
        width: v-bind(itemWidth);
        float: left;
      }
    }
  }
</style>