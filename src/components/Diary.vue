<template>
  <div class="diary-container">
    <p class="absolute-title">root/bash/diary/</p>
    <div class="entry-wrapper">
      <div class="entry" v-for="entry in entries" :key="entry.date">
        <div class="icon" @click="openEntry(entry)">
          <img src="../assets/icon-document.svg" />
          <p>{{ entry.date }}.md</p>
        </div>
      </div>
    </div>

    <div class="diary-page" v-if="diary.isOpen">
      <p>{{ diary.date }}</p>
      <div class="text" v-html="diary.text"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Diary',
  data: function() {
    return {
      entries: [
        {
          date: '08-13-2022',
          text: 'Had a fight with James today. It sucked.'
        },
        {
          date: '12-22-2024',
          text: 'I think Mr. Smith is hiding something from us....'
        }
      ],
      diary: {
        isOpen: false,
        text: '',
        date: ''
      }
    }
  },
  methods: {
    openEntry(entry) {
      this.diary.text = entry.text
      this.diary.date = entry.date
      this.diary.isOpen = true
    },
    closeEntry() {
      this.diary.isOpen = false
      this.diary.text = ''
      this.diary.date = ''
    }
  },
  mounted: function () {
  }
}
</script>

<style lang="scss">
.diary-container {
  display: flex;
  flex-direction: row;
  height: 100%;
}

.absolute-title {
  position: absolute;
  left: 30px;
  top: 4px;
}

.entry-wrapper {
  position: relative;
  width: 170px;
  top: 30px;
  padding: 10px;
  background: darken(#1D1F21, 2%);
}

.diary-page {
  // background: lighten(#1D1F21, 5%);
  position: relative;
  top: 26px;
  padding: 20px;
  height: 100%;
  width: 100%;
}

.entry .icon {
  flex-direction: row;
  align-items: center;
  justify-content: flex-start;
  width: 300px;
  height: 30px;
  margin-bottom: 5px;
  img {
    height: 100%;
    margin-bottom: 2px;
  }
}

.entry {
  display: block;
  position: relative;
  // border-radius: 4px;
  cursor: pointer;
  p {
    margin-bottom: 0px;
  }
  &:hover {
    background: rgba(white, .05)
  }
}
</style>
