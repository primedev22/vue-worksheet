<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <h2 class="d-flex align-center">My Worksheet Maker</h2>
    </v-app-bar>

    <v-main>
      <Sheet />
    </v-main>
  </v-app>
</template>

<script>
import Sheet from './components/Sheet';

export default {
  name: 'App',

  components: {
    Sheet,
  },

  data: () => ({
    //
  }),
};
</script>
