<template>
  <BannerComponent />
  <div class="main-container">
    <h1>HOME</h1>
    <FormComponent />
  </div>
</template>

<script>
import BannerComponent from "@/components/BannerComponent.vue";
import FormComponent from "@/components/FormComponent.vue";
export default {
  components: {
    BannerComponent,
    FormComponent,
  },
};
</script>
