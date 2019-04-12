<template>
  <div id="app">
    <v-card flat>

      <Header/>

      <v-layout row pb-2>
        <v-flex xs8 offset-xs2>
          <v-card class="card--flex-toolbar">
        <control-panel />
            <v-divider></v-divider>

            <v-card-text style="height: 200px;">
              adsd

            </v-card-text>
          </v-card>

        </v-flex>
      </v-layout>
    </v-card>


  </div>
</template>

<script>
import ControlPanel from './components/ControlPanel'
import FileZone from './components/FileZone'
import Header from './components/Header'

export default {
  name: 'App',
  components: {
    Header,
    ControlPanel,
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
