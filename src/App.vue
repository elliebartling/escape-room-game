<template>
  <div id="app">
    <img class="background" src="./assets/logo.svg" />
    <div class="left-column">
      <div class="console">
        <div class="date-time">
          <span>{{ date }}</span>
          <br/>
          <span>{{ time }}</span>
          <br/>
        </div>
        <br/>
        <br/>
        <ConsoleMessages></ConsoleMessages>
        <p></p>
      </div>
    </div>
    <div class="right-column">
      <Countdown></Countdown>
      <FakeWindow iconName="Logs" :x="100" :y="200" :w="500" :h="600">
        <Diary></Diary>
      </FakeWindow>
      <FakeWindow iconName="Shrug.exe" :x="900" :y="50" :w="500" :h="250">
        <Virus></Virus>
      </FakeWindow>
    </div>
    <div v-if="victory" class="bg-danger victory-box">
      <h1>GALT INITIATED</h1>
      <p>Deploying virus world wide.</p>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import FakeWindow from './components/FakeWindow.vue'
import Diary from './components/Diary.vue'
import ConsoleMessages from './components/ConsoleMessages.vue'
import Countdown from './components/Countdown.vue'
import Virus from './components/Virus.vue'

export default {
  name: 'app',
  data: function () {
    return {
      date: '2018-09-26 WED',
      time: '15:24:05',
      messages: [false, false, false, false],
      victory: false
    }
  },
  components: {
    HelloWorld,
    FakeWindow,
    ConsoleMessages,
    Diary,
    Countdown,
    Virus
  },
  methods: {
    updateTime: function() {
      var week = ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'];
      var d = new Date();

      this.time = this.zeroPadding(d.getHours(), 2) + ':' + this.zeroPadding(d.getMinutes(), 2) + ':' + this.zeroPadding(d.getSeconds(), 2)
      this.date = this.zeroPadding(d.getFullYear(), 4) + '-' + this.zeroPadding(d.getMonth()+1, 2) + '-' + this.zeroPadding(d.getDate(), 2) + ' ' + this.zeroPadding(week[d.getDay()])
    },
    zeroPadding(num, digit) {
      var zero = '';
      for(var i = 0; i < digit; i++) {
          zero += '0';
      }
      return (zero + num).slice(-digit);
    }
  },
  mounted: function() {
    setInterval(this.updateTime, 1000);
    this.updateTime();

    this.$root.$on('victory', () => {
      this.victory = true
    })
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Hack', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 0.8rem;
  text-align: center;
  color: #FFFFFF;
  position: relative;
  width: 100%;
  height: 100vh;
}

body {
  min-height: 80vh;
  background-color: #1D1F21;
  background-repeat: no-repeat;
  background-size: 40%;
  background-position: center center;
}

.background {
  width: 500px;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  left: 0;
  right: 0;
  margin: auto;
  opacity: .05;
}

.right-column {
  width: calc(100% - 40px);
  height: 100%;
  position: absolute;
  top: 40px;
  left: 0;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-end;
  overflow: visible;
  z-index: 1000;
}

.left-column {
  width: 40%;
  height: 100%;
  position: absolute;
  top: 15px;
  left: 10px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  text-align: left;
}

.special {
  margin-top: 0px;
}

.vue-typer .custom.char.typed {
  color: #FFF;
}
.vue-typer .custom.caret {
  background-color: #FFF;
  width: 4px;
}

.date-time {
  opacity: .3
}

.victory-box {
  position: absolute;
  top: 40%;
  width: 700px;
  padding: 20px;
  margin: auto;
  left: 0;
  right: 0;
  animation: flash 0.8s infinite;
  border: 2px solid #dc3545;
  p {
    margin-bottom: 0px;
  }
}

@keyframes flash {
	0% { background-color: transparent; }
	49% { background-color: transparent; }
	50% { background-color: #dc3545; }
}
</style>
