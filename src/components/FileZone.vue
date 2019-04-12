<template>
  <div id="file-zone">
    <v-container>
      <v-layout row wrap>
        <v-flex xs12 md5>
          <div id="file">
            <word v-for="(w,index) in getSplitText"
                  :word="w"
                  :index="index"
                  :indexSelected="indexSelected"
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
</template>

<script>

  import word from './Word.vue'

  export default {
    name: "FileZone",
    components: {word},
    data: function () {
      return {
        text: "",
        indexSelected: null
      }
    },
    methods: {
      wordSelected: function(value){
        this.indexSelected = value
      }
    },
    computed: {
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
</style>
