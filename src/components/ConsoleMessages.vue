<template>
  <span class="message-chunks">
    <span v-for="(chunk, chunkIndex) in messages" class="chunk">
      <p v-for="(message, index) in chunk" :key="index">
        <vue-typer :ref="`msg-${chunkIndex}-${index}`" v-if="message.start" :text="message.text " :repeat="0" @completed="activateNext(index, chunkIndex)"></vue-typer>
      </p>
    </span>
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
        [{
            text: 'Welcome back, Zoe.',
            start: true,
            chunk: 1,
            delay: 0
          },
          {
            text: 'You have ONE new message.',
            start: false,
            chunk: 1,
            delay: 100
          }],
        [{
            text: 'WARNING: Unknown external source is tracing your IP address.',
            start: false,
            chunk: 2,
            delay: 1000
          },
          {
            text: 'Attempting to identify source... ',
            start: false,
            chunk: 2,
            delay: 200,
            onComplete: function (app, index, chunk) {
              console.log(app.$refs)
              // Keep the cursor blinking for a second after message ends
              app.$refs[`msg-${chunk}-${index}`][0].$el.classList.add('blink-override')

              setInterval(() => {
                app.$refs[`msg-${chunk}-${index}`][0].$el.classList.remove('blink-override')
              }, 3000)
            }
          },
          {
            text: 'Source Identified: NDCC HQ, ETA: 20 minutes ',
            start: false,
            chunk: 2,
            delay: 3100
          },
          {
            text: 'Recommended Action: Initiate Security Protocol 17 to protect sensitive \ninformation from falling into the wrong hands. ',
            start: false,
            chunk: 2,
            delay: 100
          },
          {
            text: 'Initiating Security Protocol 17: This hard drive will self-destruct in 20 minutes. ',
            start: false,
            chunk: 2,
            delay: 100,
            onComplete: () => {
              this.$root.$emit('countdown')
            }
          }]
      ]
    }
  },

  methods: {
    activateNext(index, chunk) {
      var msg = this.messages[chunk][index]
      var nextmsg = this.messages[chunk][index+1]
      var app = this

      if (nextmsg) {
        setInterval(() => {
          nextmsg.start = true
        }, nextmsg.delay)
      }

      if (msg.onComplete) {
        msg.onComplete(app, index, chunk)
      }
    }
  },
  mounted() {
    var app = this
    this.$root.$on('initTracerMessageSequence', () => {
      app.messages[1][0].start = true
    })
  }
}
</script>

<style lang="scss">
  .console p {
    margin-bottom: 0.25rem;
  }

  .vue-typer.blink-override .caret.complete {
    display: inline-block;
  }

  .chunk {
    margin-bottom: 20px;
    display: block;
  }
</style>
