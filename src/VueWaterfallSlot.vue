<template>
  <div class="vue-waterfall-slot" v-show="isShow">
    <slot></slot>
  </div>
</template>

<style>
.vue-waterfall-slot {
  position: absolute;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>

<script>
export default {
  name: 'VueWaterfallSlot',
  data() {
    return {
      rect: {
        top: 0,
        left: 0,
        width: 0,
        height: 0
      }
    }
  },
  props: {
    width: {
      required: true,
      validator: (val) => val >= 0
    },
    height: {
      required: true,
      validator: (val) => val >= 0
    },
    order: {
      default: 0
    },
    moveClass: {
      default: ''
    },
    isShow: {
      default: false
    }
  },
  computed:{
    meta(){
      return {
        vm: this,
        node: this.$el,
        order: this.order,
        width: this.width,
        height: this.height,
        moveClass: this.moveClass
      }
    },
    sizeWatchArray(){
      return [
        this.width,
        this.height
      ]
    }
  },
  watch:{
    sizeWatchArray: {
      handler(){
        this.notify()
      },
      deep: true
    }
  },
  methods: {
    notify() {
      this.$emit('reflow')
    }
  },
  mounted() {
    this.notify()
  },
  unmounted() {
    this.notify()
  }
}

</script>
