<template>
  <div id="footer">
    <p>
      Feito por Barquinho's Software &copy; <strong>{{ currentYear }}</strong
      >.
    </p>
  </div>
</template>

<script>
export default {
  name: "Footer-html",
  data() {
    return {
      currentYear: null,
    };
  },
  mounted() {
    this.currentYear = new Date().getFullYear();
  },
};
</script>

<style scoped>
#footer {
  height: 100px;
  background-color: #222;
  border-top: 4px solid #111;
  color: #fcba03;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}
</style>
