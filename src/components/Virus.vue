<template>
  <div class="virus-wrap">
    <div class="title">
      <h4>Operation Galt</h4>
      <p>Please enter 3 correct locks to continue.</p>
    </div>
    <div class="locks">
      <div v-for="(input, index) in inputs" class="lock" :key="index">
        <input class="form-control" type="text" placeholder="XXXX" v-model="input.value" @change="checkCombo(input.value, index)" v-bind:class="{ 'is-valid' : input.isValid, 'is-error': input.isError }"/>
      </div>
    </div>
    <div class="feedback text-center">
      <p class="feedback-text text-danger" v-if="displayError">That code is incorrect.</p>
      <p class="feedback-text" v-bind:class="{ 'red': victory }">{{ numCorrect }} of 3 locks correct</p>
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
      inputs: [
        { value: '', isValid: false, isError: false },
        { value: '', isValid: false, isError: false },
        { value: '', isValid: false, isError: false }
      ],
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
        } else {
          return 0
        }
      })
    },
    displayError: function () {
      if (_.some(this.inputs, { isError: true })) {
        return true
      } else {
        return false
      }
    },
    victory: function() {
      if (this.numCorrect == 3) {
        console.log('Victory!')
        this.$root.$emit('victory')
        return true
      } else {
        return false
      }
    }
  },
  methods: {
    checkCombo: function(value, index) {
      // var correct = _.some(this.codes, { 'key': value, used: false })
      var correct = _.findIndex(this.codes, { 'key': value, used: false })
      console.log(correct)
      if (correct > -1) {
        this.codes[correct].used = true
        this.inputs[index].isValid = true
        this.inputs[index].isError = false
      } else {
        this.inputs[index].isError = true
      }
    }
  }
}
</script>

<style lang="scss">
.virus-wrap {
  width: 100%;
  height: 100%;
  display: block;
  padding-top: 30px;
}

.title {
  text-align: center;
}

.locks {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  margin-top: 40px;
  z-index: 100;
  position: relative;
}

.lock input {
  border-radius: 0px;
  display: block;
  padding: 10px;
  border: 2px solid;
  width: 100px;
  text-align: center;
  letter-spacing: 4px;
  box-shadow: none;
  outline: none;
}

.feedback {
  margin-top: 20px;
  margin-bottom: 40px;
}

.form-control.is-valid {
  position: relative;
  background: transparent;
  border-color: transparent !important;
  color: #17a2b8;
  // color: #94B524;
  // outline-color: rgba(#17a2b8, .2);
}

.form-control.is-error {
  position: relative;
  background: #dc3545;
  border-color: #dc3545 !important;
  color: rgba(black, .5);
  // color: #94B524;
  // outline-color: rgba(#dc3545, .2);
}

.feedback-text {
  margin-bottom: 0px;
}
</style>
