<template>


    <v-toolbar card prominent>


      <v-btn-toggle v-model="toggle" multiple>
        <v-btn >
          <v-icon>format_bold</v-icon>
        </v-btn>
        <v-btn >
          <v-icon>format_italic</v-icon>
        </v-btn>
        <v-btn >
          <v-icon>format_underlined</v-icon>
        </v-btn>

      </v-btn-toggle>
    </v-toolbar>


</template>

<script>
export default {
  name: "ControlPanel",
  data: function () {
    return {
      toggle: [0, 0, 0]
    }
  },
};
</script>
<style scoped>

  .card--flex-toolbar {
    margin-top: -64px;
  }

</style>
