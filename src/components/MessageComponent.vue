<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: "Message-alert",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
.message-container {
  color: #004085;
  background-color: #64e952;
  border: solid 2px #b8daff;
  border-radius: 5px;
  padding: 10px;
  max-width: 400px;
  margin: 30px auto;
}
</style>
