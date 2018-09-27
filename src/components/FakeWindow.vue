<template>
  <div class="wrapper">
    <div v-if="this.open" class="window"
      :isActive="false"
      :isResizeable="true"
      :w="this.w" :h="this.h"
      :sticks="[]"
      :x="this.x" :y="this.y"
      :style="getStyle()"
      >
      <div class="buttons">
        <button @click="() => { this.open = false }"><span>&#x2715;</span></button>
      </div>

      <slot></slot>
    </div>

    <div class="icon" @click="this.openWindow">
      <img src="../assets/icon-folder.svg" />
      <span>{{ iconName }}</span>
    </div>
  </div>
</template>

<script>
import VueDragResize from 'vue-drag-resize';
export default {
  name: 'FakeWindow',
  props: {
    msg: String,
    iconName: String,
    x: Number,
    y: Number,
    w: Number,
    h: Number
  },
  components: {
    VueDragResize
  },
  data: function() {
    return {
      open: false
    }
  },
  methods: {
    openWindow: function () {
      this.open = true
    },
    getStyle: function() {
      return `top: ${this.y}px; left: ${this.x}px; width: ${this.w}px; height: ${this.h}px`;
    }
  }
}
</script>

<style lang="scss">
.window {
  // border: 1px solid lighten(#1D1E1E, 30%);
  text-align: left;
  padding: 20px 20px;
  background: darken(#1D1F21, 5%);
  box-shadow: 0px 0px 10px rgba(black, .4);
  // border-radius: 4px;
  z-index: 1000 !important;
  position: absolute;
}

.vdr.active::before {
  outline: none !important;
}

.window button {
  background: transparent;
  // color: rgba(black, .8);
  color: white;
  border: none;
  position: absolute;
  left: 5px;
  height: 14px;
  width: 14px;
  font-size: 8px;
  // padding: 2px;
  font-weight: bold;
  top: 7px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  border-radius: 100px;
}


.icon {
  display: flex;
  flex-direction: column;
  width: 70px;
  margin-bottom: 40px;
}

.icon img {
  max-width: 100%;
  margin-bottom: 10px;
}
</style>
