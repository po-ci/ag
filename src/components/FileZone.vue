<template>
  <div>
    <control-panel
      v-on:bold="onBold"
      v-on:italic="onItalic"
      v-on:underlined="onUnderline"
      :toggle="toggle"
    />

    <v-divider></v-divider>
    <div id="file-zone">
      <v-container>
        <v-layout row wrap>
          <v-flex xs12 md5>
            <div id="file">
              <word v-for="(w,index) in getSplitText"
                    :word="w"
                    :index="index"
                    :indexSelected="indexSelected"
                    :bold="bold"
                    :italic="italic"
                    :underlined="underlined"
                    v-on:wordSelected="wordSelected"
              />

            </div>
          </v-flex>

          <v-flex xs12 md5 offset-md2>
            <div id="inputtext">
              <textarea style="width: 100%; height:100%;" v-model="text"></textarea>
            </div>
          </v-flex>
        </v-layout>
      </v-container>
    </div>
  </div>
</template>

<script>

  import word from './Word.vue'
  import ControlPanel from './ControlPanel'

  export default {
    name: "FileZone",
    components: {word, ControlPanel},
    data: function () {
      return {
        text: "",
        indexSelected: null,
        bold: [],
        italic: [],
        underlined: [],
        //  toggle: [false, false, false]
      }
    },

    methods: {
      wordSelected: function (value) {
        this.indexSelected = value
      },
      onUnderline: function (value) {
        var i = this.underlined.findIndex(item => item == this.indexSelected)

        if (i == -1) {
          this.underlined.push(this.indexSelected)
        } else {
          this.$delete(this.underlined, i)
        }
      },
      onItalic: function (value) {
        var i = this.italic.findIndex(item => item == this.indexSelected)

        if (i == -1) {
          this.italic.push(this.indexSelected)
        } else {
          this.$delete(this.italic, i)
        }
      },
      onBold: function (value) {
        var i = this.bold.findIndex(item => item == this.indexSelected)

        if (i == -1) {
          this.bold.push(this.indexSelected)
        } else {
          this.$delete(this.bold, i)
        }
      }
    },
    computed: {
      toggle: function () {
        let arr = []
        if (this.bold.findIndex(item => item == this.indexSelected) != -1) {
          arr.push(0)
        }
        if (this.italic.findIndex(item => item == this.indexSelected) != -1) {
          arr.push(1)
        }
        if (this.underlined.findIndex(item => item == this.indexSelected) != -1) {
          arr.push(2)
        }
        return arr
      },
      getSplitText: function () {
        return this.text.split(" ")
      }
    }
  };
</script>
<style scoped>

  #inputtext {
    width: 300px;
    height: 300px;
    flex-grow: 1;
    background-color: #fff;
    border: 1px solid #e4dede;
  }

  #file {
    width: 300px;
    height: 300px;
    flex-grow: 1;
    background-color: #fff;
    border: 1px solid #e4dede;
  }

  #file-zone {
    background-color: #f1f0f0;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 5px;
  }
</style>
