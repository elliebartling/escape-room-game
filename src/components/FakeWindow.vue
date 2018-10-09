<template>
  <div class="wrapper">
    <div v-if="this.open" class="window"
      :active="true"
      :isResizeable="false"
      :w="this.w" :h="this.h"
      :sticks="[]"
      :x="this.x" :y="this.y"
      :style="getStyle()"
      >
      <slot></slot>
      <div class="buttons">
        <button @click="this.closeWindow"><span>&#x2715;</span></button>
      </div>
    </div>

    <div class="icon" @click="this.openWindow">
      <div v-if="this.displayBadge" class="badge bg-danger">
        <span>{{ this.badge }}</span>
      </div>
      <img :src="icon" />
      <span>{{ caption }}</span>
    </div>
  </div>
</template>

<script>
import VueDragResize from 'vue-drag-resize';
export default {
  name: 'FakeWindow',
  props: {
    msg: String,
    caption: String,
    iconName: String,
    x: Number,
    y: Number,
    w: Number,
    h: Number,
    badge: Number
  },
  components: {
    VueDragResize
  },
  data: function() {
    return {
      open: false,
      badgeNum: 0
    }
  },
  computed: {
    displayBadge: function() {
      return (this.badgeNum > 0) ? true : false
    },
    icon: function() {
      return require(`../assets/icon-${this.iconName}.svg`)
    }
  },
  methods: {
    openWindow: function () {
      this.open = true
    },
    closeWindow: function () {
      this.open = false
      if (this.badgeNum > 0) {
        this.badgeNum = 0
      }
    },
    getStyle: function() {
      return `top: ${this.y}px; left: ${this.x}px; width: ${this.w}px; height: ${this.h}px`;
    }
  },
  mounted() {
    this.badgeNum = this.badge
  }
}
</script>

<style lang="scss">
.window {
  // border: 1px solid lighten(#1D1E1E, 30%);
  text-align: left;
  // padding: 20px 20px;
  background: darken(#1D1F21, 5%);
  box-shadow: 0px 0px 10px rgba(black, .4);
  // border-radius: 4px;
  z-index: 1000 !important;
  position: absolute;
  overflow: hidden;
}

.vdr.active::before {
  outline: none !important;
  display: none;
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
  position: relative;
}

.icon img {
  max-width: 100%;
  margin-bottom: 10px;
}

.badge {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 25px;
  height: 25px;
  border-radius: 100px;
  position: absolute;
  top: 2px;
  font-weight: bold;
  right: -10px;
}
</style>
