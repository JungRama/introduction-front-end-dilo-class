<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark>
      <v-btn>
        <span class="mr-2">Dilo Class</span>
      </v-btn>
    </v-app-bar>

    <v-main>
      <HelloWorld/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
