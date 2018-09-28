<template>

    <div v-if="this.open" class="window red-bg"
      :isActive="true"
      :isResizeable="false"
      :w="600" :h="300"
      :sticks="[]"
      :x="this.x" :y="this.y">
      <VueCountdown v-if="counting" :time="1.2e+6" :leading-zero="false">
       <template slot-scope="props">
         <h1>{{ props.minutes }}m:{{ props.seconds }}s remaining</h1>
       </template>
     </VueCountdown>
   </div>

</template>

<script>
import VueCountdown from '@xkeshi/vue-countdown'
import VueDragResize from 'vue-drag-resize';

export default {
  name: 'Countdown',
  components: { VueCountdown, VueDragResize },
  data: function() {
    return {
      open: false,
      counting: false,
      x: 300,
      y: 300
    }
  },
  methods: {
    initCountdown () {

    }
  },
  mounted() {
    this.$root.$on('countdown', () => {
      this.open = true
      this.counting = true
    })
  }
}
</script>

<style lang="scss" scoped>
.window {
  position: absolute;
  z-index: 50;
  left: 0;
  right: 0;
  margin: auto;
  top: 10px;
  // transform: translateY(-60%);
  width: 30%;
  text-align: center;
  box-shadow: none;
  border-radius: 0px;
  background: #FF2400;
  padding: 10px;
  * {
    margin-bottom: 0px;
  }
}
</style>
