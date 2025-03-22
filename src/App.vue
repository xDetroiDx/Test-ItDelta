<template>
  <div id="app">
    <MainHeader />
    <UserProfile />
    <ImageGrid />
  </div>
</template>

<script>
import MainHeader from './components/MainHeader.vue';
import UserProfile from './components/UserProfile.vue';
import ImageGrid from './components/ImageGrid.vue';

export default {
  name: 'App',
  components: {
    MainHeader,
    UserProfile,
    ImageGrid,
  },
};
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #E5E5E5;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #E5E5E5;
  width: 1358px;

}
</style>