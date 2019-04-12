<template>
  <span @click="selectWord">
    <span :class="{ selectWord: isSelected}">{{word}}</span>&nbsp;
  </span>
</template>

<script>
  export default {
    name: "Word",
    props: {word: String, index: Number, indexSelected: Number},
    data: function () {
      return {
        selected: false,
      }
    },
    computed: {
      isSelected: function () {
        return this.index === this.indexSelected
      },
    },
    methods: {

      selectWord: function () {
        this.$emit('wordSelected', this.index)
      }
    }
  }
</script>

<style scoped>
  .selectWord {
    background-color: #90CAF9;
  }
</style>
