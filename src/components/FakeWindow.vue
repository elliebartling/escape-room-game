<template>
  <div>
    <VueDragResize v-if="this.open" class="window"
      :isActive="true"
      :isResizeable="false"
      :w="500" :h="300"
      v-on:resizing="resize"
      v-on:dragging="resize"
      :sticks="[]"
      :x="this.x" :y="this.y">
      <button @click="() => { this.open = false }">&#x2715;</button>

      <slot></slot>
    </VueDragResize>

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
    x: String,
    y: String
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
    }
  }
}
</script>

<style lang="scss">
.window {
  // border: 1px solid lighten(#1D1E1E, 30%);
  text-align: left;
  padding: 10px 20px;
  background: darken(#1D1F21, 5%);
  box-shadow: 0px 0px 20px rgba(black, .4);
  border-radius: 4px;
}

.vdr.active::before {
  outline: none !important;
}

.window button {
  background: transparent;
  color: white;
  border: none;
  font-size: 15px;
  position: absolute;
  right: 5px;
  top: 7px;
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
