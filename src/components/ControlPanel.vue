<template>


  <v-toolbar card prominent>


    <v-btn-toggle :value="toggle" multiple>
      <v-btn @click="$emit('bold')">
        <v-icon>format_bold</v-icon>
      </v-btn>
      <v-btn @click="$emit('italic')">
        <v-icon>format_italic</v-icon>
      </v-btn>
      <v-btn @click="$emit('underlined')">
        <v-icon>format_underlined</v-icon>
      </v-btn>

    </v-btn-toggle>
    <v-spacer></v-spacer>


  </v-toolbar>


</template>

<script>


  export default {
    name: "ControlPanel",
    props: {toggle: Array, wordSelected: String},
    data: function () {
      return {
      }
    }

  };
</script>
<style scoped>

  .card--flex-toolbar {
    margin-top: -64px;
  }

</style>
