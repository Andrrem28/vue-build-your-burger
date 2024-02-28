<template>
  <NavBarComponent :logo="logo_src" :alt="app_name" />
  <router-view />
  <FooterComponent />
</template>

<script>
import NavBarComponent from "./components/NavBarComponent.vue";
import FooterComponent from "./components/FooterComponent.vue";

export default {
  components: {
    NavBarComponent,
    FooterComponent,
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "build-your-burguer",
    };
  },
};
</script>

<style>
* {
  font-family: Helvetica;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.main-container {
  margin: 50px;
  min-height: 250px;
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}
</style>
