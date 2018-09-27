<template>
  <span>
    <p v-for="(message, index) in messages" :key="index">
      <vue-typer v-if="message.start" :text="message.text " :repeat="0" @completed="activateNext(index)"></vue-typer>
    </p>
  </span>
</template>

<script>
import { VueTyper } from 'vue-typer'

export default {
  name: 'ConsoleMessages',
  components: {
    VueTyper
  },
  data: function() {
    return {
      messages: [
        {
          text: 'Welcome back, Zoe.',
          start: true,
          delay: 0
        },
        {
          text: 'WARNING: Unknown external source is tracing your IP address.',
          start: false,
          delay: 1000
        },
        {
          text: 'Attempting to identify source... ',
          start: false,
          delay: 200
        },
        {
          text: 'Source Identified: NDCC HQ ',
          start: false,
          delay: 3000
        },
        // {
        //   text: 'ETA: 20 minutes ',
        //   start: false,
        //   delay: 500,
        //   triggerEvent: 'countdown'
        // },
      ]
    }
  },

  methods: {
    activateNext(index) {
      var msg = this.messages[index]
      var nextmsg = this.messages[index+1]

      if (nextmsg) {
        setInterval(() => {
          nextmsg.start = true
        }, nextmsg.delay)
      }

      if (msg.triggerEvent) {
        this.$root.$emit(msg.triggerEvent)
      }
    }
  }
}
</script>
