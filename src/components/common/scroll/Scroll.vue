<template>
  <!-- ref如果是绑定在组件中的，那么通过this.$refs.refname获取到的是一个组件对象 -->
  <!-- ref如果是绑定在普通元素中的，那么通过this.$refs.refname获取到的是一个元素对象 -->
  <!-- ref通常绑定在子组件上 -->
  <div class="wrapper" ref="wrapper">
    <div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll';

  export default {
    name: 'Scroll',
    props: {
      probeType: {
        type: Number,
        default: 0
      },
      pullUpLoad: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        scroll: null,
        message: '哈哈哈哈哈哈'
      }
    },
    mounted() {
      // 1. 创建BScroll
      this.scroll = new BScroll(this.$refs.wrapper, {
        click: true,
        scrollY: true,
        observeImage: true,
        probeType: this.probeType,
        pullUpLoad: this.pullUpLoad
      })
      // 2. 监听滚动的位置
      this.scroll.on('scroll', (position) => {
        this.$emit('scroll', position);
      })
      // 3. 监听上拉事件
      this.scroll.on('pullingUp', () => {
        this.$emit('pulling');
      })
    },
    methods: {
      scrollTo(x, y, time = 300) {
        this.scroll.scrollTo(x, y, time)
      },
      finishPullUp() {
        this.scroll.finishPullUp();
      },
      // refresh() {
      //   this.scroll.refresh();
      // }
    }

  }
</script>

<style scoped>

</style>