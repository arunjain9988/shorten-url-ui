<template>
  <div class="h-screen">
    <AppHeader />
    <router-view />
    <!-- <AppFooter /> -->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import AppHeader from "./components/AppHeader.vue";
// import AppFooter from "./components/AppFooter.vue";

export default {
  name: "App",
  components: {
    // HelloWorld
    AppHeader,
    // AppFooter,
  },
};
</script>

<style></style>
