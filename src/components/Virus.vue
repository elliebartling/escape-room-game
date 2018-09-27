<template>
  <div style="">
    <div class="title">
      <h2>Operation Galt</h2>
      <p>Please enter 3 correct locks to continue.</p>
    </div>
    <div class="locks">
      <div class="lock">
        <input placeholder="XXXX" v-model="input1" @change="checkCombo(input1)"/>
      </div>
      <div class="lock">
        <input placeholder="XXXX" v-model="input2" @change="checkCombo(input2)"/>
      </div>
      <div class="lock">
        <input placeholder="XXXX" v-model="input3" @change="checkCombo(input3)"/>
      </div>
    </div>
    <div class="feedback text-center">
      <p v-bind:class="{ 'red': victory }">{{ numCorrect }} of 3 locks correct</p>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
export default {
  name: 'Virus',
  data: function() {
    return {
      codes: [
        { key: '1776', used: false },
        { key: '1913', used: false },
        { key: '1984', used: false },
      ],
      // numCorrect: 0,
      input1: '',
      input2: '',
      input3: ''
    }
  },
  computed: {
    numCorrect: function () {
      return _.sumBy(this.codes, (o) => {
        if (o.used) {
          return 1
        }
      })
    },
    victory: function() {
      if (this.numCorrect == 3) {
        return true
      } else {
        return false
      }
    }
  },
  methods: {
    checkCombo: function(value) {
      // var correct = _.some(this.codes, { 'key': value, used: false })
      var correct = _.findIndex(this.codes, { 'key': value, used: false })
      console.log(correct)
      if (correct > -1) {
        this.codes[correct].used = true
      }
    }
  }
}
</script>

<style lang="scss">
.title {
  text-align: center;
}

.locks {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  margin-top: 60px;
  z-index: 100;
  position: relative;
}

.lock input {
  // outline: none;
  border: 0px;
  display: block;
  padding: 10px;
  width: 100px;
  text-align: center;
  letter-spacing: 4px;
}

.feedback {
  margin-top: 20px;
  margin-bottom: 40px;
}
</style>
