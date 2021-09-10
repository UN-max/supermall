<template>
  <div class="tab-ctrl">
    <div v-for="(item, index) in titles" class="tab-ctrl-item" :class="{active: index === currentIndex}" @click="itemClick(index)">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'TabCtrl',
    data () {
      return {
        currentIndex: 0
      };
    },
    props: {
      titles: {
        type: Array,
        default() {
          return []
        }
      }
    },
    methods: {
      itemClick(index) {
        this.currentIndex = index;
        this.$emit('tabClick', index);
      }
    }
  }
</script>

<style scoped>
  .tab-ctrl {
    display: flex;
    text-align: center;
    height: 40px;
    line-height: 40px;
    font-size: 15px;
    background-color: #fff;
  }
  .tab-ctrl-item {
    flex: 1;
  }

  .tab-ctrl-item span {
    padding: 0 2px 2px;
  }
  .active {
    color: var(--color-high-text);
  }
  .active span {
    border-bottom: 3px solid var(--color-tint);
  }
</style>