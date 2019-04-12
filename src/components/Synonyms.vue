<template>
  <span>
    <v-btn
      class="ma-0"
      color="orange"
      dark
      small
      @click.stop="dialog = true"
      :disabled="wordSelected ? false : true"
    >
      Synonyms
    </v-btn>
    <v-dialog
      v-model="dialog"
      max-width="500"
    >
      <v-card>
        <v-card-title class="headline">Input Text</v-card-title>

        <v-card-text>
          Synonyms for {{wordSelected}}
        </v-card-text>
        <v-card-text>
          <v-select

            :items="synonyms"
            label="Synonyms"
            solo
            @change="changeWord"
            :loading="loading"
            v-model="wvalue"
          ></v-select>

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
  </span>
</template>

<script>
  import axios from 'axios'

  export default {
    name: "Synonyms",
    props: {indexSelected: Number, wordSelected: String},
    data: function () {
      return {
        dialog: false,
        synonyms: [],
        loading: false,
        wvalue: null
      }
    },
    watch: {
      wordSelected: function () {
        this.fetchSynonyms()
      }
    },
    methods: {
      changeWord: function(){
        this.$emit("changeWord",{newWord:this.wvalue,index:this.indexSelected})
      },
      fetchSynonyms: function () {
        this.loading = true
        this.synonyms = []
        axios.get('https://api.datamuse.com/words?rel_syn=' + this.wordSelected)
          .then(response => {
            console.log(response);
            for (var i = 0; i < response.data.length; i++) {
              this.synonyms.push({text: response.data[i].word, value: response.data[i].word})
            }
            this.loading = false
          })
      },
    }
  }
</script>

<style scoped>

</style>
