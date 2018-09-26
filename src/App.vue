<template>
  <div id="app">
    <img class="background" src="./assets/logo.svg" />
    <div class="right-column">
      <FakeWindow iconName="Logs" :x="200" :y="400">
        <p>root/bash/diary/</p>
        <Diary></Diary>
      </FakeWindow>
      <FakeWindow iconName="Shrug" :x="500" :y="200">
        <p>Activate virus?</p>
      </FakeWindow>
    </div>

    <div class="left-column">
      <div class="console">
        <div class="date-time">
          <span>{{ date }}</span>
          <br/>
          <span>{{ time }}</span>
          <br/>
        </div>
        <!-- <p><strong class="red">WARNING:</strong> Level 4 Clearance Needed</p> -->
        <br/>
        <br/>
        <!-- <p><vue-typer text="Welcome back, Zoe. " :repeat="0"></vue-typer></p>
        <p><vue-typer text="WARNING: external IP backtrace in progress. " :repeat="0" :pre-type-delay="3000"></vue-typer></p>
        <p><vue-typer text="Triangulating source... " :repeat="0" :pre-type-delay="3000"></vue-typer></p>
        <p><vue-typer text="Source: NDCC HQ " :repeat="0" :pre-type-delay="3000"></vue-typer></p>
        <p><vue-typer text="Estimating time until NDCC has lock on your location... " :repeat="0" :pre-type-delay="3000"></vue-typer></p>
        <p><vue-typer text="ETA: 20 min " :repeat="0" :pre-type-delay="3000"></vue-typer></p> -->
        <p></p>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import FakeWindow from './components/FakeWindow.vue'
import Diary from './components/Diary.vue'
import { VueTyper } from 'vue-typer'

export default {
  name: 'app',
  data: function () {
    return {
      passcodes: [1776, 1913, 1984],
      date: '2018-09-26 WED',
      time: '15:24:05',
      messages: [false, false, false, false]
    }
  },
  components: {
    HelloWorld,
    FakeWindow,
    VueTyper,
    Diary
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
  z-index: 100;
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
</style>
