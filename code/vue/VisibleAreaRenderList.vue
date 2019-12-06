<template>
  <div class="list-view" ref="list" @scroll="handleScroll($event)">
    <div class="list-view-phantom" :style="{height: listData.length * itemHeight + 'px'}"></div>
    <div class="list-view-content" ref="content">
      <div class="list-view-item" v-for="item in visibleData" :key="item">{{item}}</div>
    </div>
  </div>
</template>
<script>
export default {
  // 可视区域渲染列表: 列表高度400px;item高度30px;一次加载10000条数据
  name: 'VisibleAreaRenderList',
  props: {
    // listData: {
    //   type: array
    // },
    itemHeight: {
      type: Number,
      default: 30
    }
  },
  mounted () {
    this.visibleCount = Math.ceil(this.$el.clientHeight / this.itemHeight)
    this.start = 0
    this.end = this.start + this.visibleCount
    this.visibleData = this.listData.slice(this.start, this.end)
  },
  data () {
    const listData = []
    for (let i = 0; i < 10000; i++) {
      listData.push(i)
    }
    return {
      listData,
      start: 0,
      end: null,
      visibleCount: null,
      visibleData: [],
      scrollTop: 0
    }
  },
  methods: {
    handleScroll: function () {
      const scrollTop = this.$refs.list.scrollTop
      // 滚动距离不一定是单个item高度的倍数
      const fixedScrollTop = scrollTop - scrollTop % this.itemHeight
      this.$refs.content.style.webkitTransform = `translateY(${fixedScrollTop}px)`
      this.start = Math.floor(scrollTop / this.itemHeight)
      this.end = this.start + this.visibleCount
      this.visibleData = this.listData.slice(this.start, this.end)
    }
  }
}
</script>
<style lang="less" scoped>
.list-view {
  position: relative;
  height: 800px;
  overflow: auto;
  border: 1px solid #666;
}
.list-view-phantom {
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  z-index: -1;
}
.list-view-content {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
}
.list-view-item {
  padding: 5px;
  color: #666;
  height: 60px;
  line-height: 60px;
  box-sizing: border-box;
}
</style>
