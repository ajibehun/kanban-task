<template>
  <v-app>
    <v-app-bar app color="primary" flat>
      <v-app-bar-title class="white--text"> Kanban</v-app-bar-title>
    </v-app-bar>

    <v-main>
      <Board></Board>
    </v-main>
  </v-app>
</template>

<script>
  import Board from "./components/Board";

  export default {
    name: "App",
    components: {
      Board,
    },
  };
</script>
