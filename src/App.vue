<template>
  <v-app>
    <v-main>
      <fileRead/>
    </v-main>
  </v-app>
</template>

<script>
import fileRead from './components/fileRead';

export default {
  name: 'App',

  components: {
    fileRead,
  },

  data: () => ({
    //
  }),
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>