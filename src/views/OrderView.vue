<template>
  <div class="main-container">
    <h1>Gerenciamento de pedidos:</h1>
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
