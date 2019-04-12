<template>
  <div id="app">
    <v-card flat>

      <Header/>

      <v-layout row pb-2>
        <v-flex xs8 offset-xs2>
          <v-card class="card--flex-toolbar">


            <v-card-text id="file-zone">
              <file-zone/>

            </v-card-text>
          </v-card>

        </v-flex>
      </v-layout>
    </v-card>


  </div>
</template>

<script>

  import FileZone from './components/FileZone'
  import Header from './components/Header'

  export default {
    name: 'App',
    components: {
      Header,
      FileZone
    }
  }
</script>

<style>


  #app {
    display: flex;
    height: 100%;
    flex-direction: column;
  }

  main {
    display: flex;
    flex-direction: column;
    flex-grow: 1;
  }

  .card--flex-toolbar {
    margin-top: -64px;
  }



</style>
