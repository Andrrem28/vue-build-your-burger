<template>
  <div class="main-container">
    <h1>Gerenciar pedidos.</h1>
    <h1>Pedidos</h1>
    <DashboardComponent />
  </div>
</template>

<script>
import DashboardComponent from "@/components/DashboardComponent.vue";
export default {
  name: "Orders-html",
  components: {
    DashboardComponent,
  },
};
</script>
