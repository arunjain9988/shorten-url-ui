<template>
  <div class="h-screen" id="main">
    <AppHeader />
    <!-- <router-view /> -->
    <Main />
  </div>
  <AppFooter />
  <!-- <div id="footer">
      <p>footer</p>
    </div> -->
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import Main from "./pages/Main.vue";
export default {
  name: "App",
  components: {
    // HelloWorld
    AppHeader,
    Main,
    AppFooter,
  },
};
</script>

<style>
#footer {
  /* text-size-adjust: 13px;*/
  position: absolute;
  bottom: 0%;
}

#main {
  background: url("https://phe.email/static/assets/img/bg-03-02.svg") center center no-repeat,
    url("https://phe.email/static/assets/img/bg-03-01.svg") center center no-repeat;
  background-color: hsla(216, 33%, 97%, 1);
  background-color: var(--forny-color-gray-100);
}
</style>
