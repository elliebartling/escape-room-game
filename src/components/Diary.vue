<template>
  <div class="diary-container">
    <div class="entry" v-for="entry in entries" :key="entry.date">
      <div class="icon" @click="this.openEntry(entry)">
        <img src="../assets/icon-document.svg" />
        <span>{{ entry.date }}.md</span>
      </div>
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
      ]
    }
  },
  methods: {

  },
  mounted: function () {
  }
}
</script>

<style lang="scss">
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
  border-radius: 4px;
  &:hover {
    background: rgba(white, .2)
  }
}
</style>
