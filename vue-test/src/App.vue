<script>
import UsersTableLogic from '@/components/UsersTableLogic.vue';

export default {
  name: 'App',
  components: {
    UsersTableLogic,
  },
};
</script>

<template>
  <div id="app">
    <UsersTableLogic/>
  </div>
</template>

<style>
#app {
  font-family: 'Roboto', sans-serif;
}
</style>
