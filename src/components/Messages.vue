<template>
  <div class="messages">
    <video-player class="video-player-box"
      :options="playerOptions"
      @ended="onVideoEnd"
      ref="videoPlayer">
    </video-player>
  </div>
</template>

<script>
import 'video.js/dist/video-js.css'
import { videoPlayer } from 'vue-video-player'

export default {
  name: 'Messages',
  components: { videoPlayer },
  data: function() {
    return {
      playerOptions: {
        muted: false,
        sources: [{
          type: "video/mp4",
          src: require('../assets/test-video.mp4')
        }],
        autoplay: true,
        controls: false,
        height: 540
      }
    }
  },
  methods: {
    onVideoEnd: function () {
      console.log(this.$root.$emit('initTracerMessageSequence'))
      this.$parent.open = false
    }
  },
  mounted() {
  }
}
</script>

<style lang="scss">

</style>
