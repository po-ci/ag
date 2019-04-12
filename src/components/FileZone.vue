<template>
  <div>
    <control-panel
      v-on:bold="onBold"
      v-on:italic="onItalic"
      v-on:underlined="onUnderline"
      :toggle="toggle"
      :wordSelected="wordSelected"
    />

    <v-divider></v-divider>

    <div>
      <v-container>
        <v-layout row wrap>

          <v-flex xs12 md12>

            <div id="file">
              <word v-for="(w,index) in getSplitText"
                    :word="w"
                    :index="index"
                    :indexSelected="indexSelected"
                    :bold="bold"
                    :italic="italic"
                    :underlined="underlined"
                    v-on:selectWord="selectWord"
              />

            </div>

          </v-flex>
          <v-flex>
            <v-btn
              class="ma-0"
              color="primary"
              dark
              small
              @click.stop="dialog = true"
            >
              Edit Text
            </v-btn>
            <synonyms
              :word-selected="wordSelected"
              :index-selected="indexSelected"
              v-on:changeWord="changeWord"
            ></synonyms>
          </v-flex>


        </v-layout>
      </v-container>

      <v-dialog
        v-model="dialog"
        max-width="500"
      >
        <v-card>
          <v-card-title class="headline">Input Text</v-card-title>

          <v-card-text>
            <textarea id="tarea" v-model="text"></textarea>
          </v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="indigo darken-1"
              dark
              @click="dialog = false"
            >
              ok
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>
  </div>
</template>

<script>

  import word from './Word.vue'
  import ControlPanel from './ControlPanel'
  import Synonyms from './Synonyms'

  export default {
    name: "FileZone",
    components: {word, ControlPanel, Synonyms},
    data: function () {
      return {
        dialog: false,
        text: "Hello World",
        indexSelected: null,
        wordSelected: null,
        bold: [],
        italic: [],
        underlined: [],
        synonyms: [],
        loading: false
      }
    },

    methods: {
      changeWord: function (obj) {
        var a = this.getSplitText
        a[obj.index] = obj.newWord
        this.text = a.join(" ")
      },
      selectWord: function (obj) {
        this.indexSelected = obj.index
        this.wordSelected = obj.word
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


  #file {
    height: 300px;
    background-color: #fff;
    border: 1px solid #e4dede;
  }


  #tarea {
    width: 100%;
    height: 100%;
  }
</style>
