<template>
  <span @click="selectWord">
    <span :class="{ selectWord: isSelected, bold: isBold, underlined: isUnderlined, italic: isItalic}">{{word}}</span>&nbsp;
  </span>
</template>

<script>
  export default {
    name: "Word",
    props: {word: String, index: Number, indexSelected: Number, bold: Array, italic: Array, underlined: Array},
    data: function () {
      return {
        selected: false,
      }
    },
    computed: {
      isSelected: function () {
        return this.index === this.indexSelected
      },
      isBold: function () {
        if (this.bold.indexOf(this.index) == -1) {
          return false
        }
        return true
      },
      isUnderlined: function () {
        if (this.underlined.indexOf(this.index) == -1) {
          return false
        }
        return true
      },
      isItalic: function () {
        if (this.italic.indexOf(this.index) == -1) {
          return false
        }
        return true
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

  .bold {
    font-weight: bold;
  }

  .italic {
    font-style: italic;
  }

  .underlined {
    text-decoration: underline;
  }

</style>
