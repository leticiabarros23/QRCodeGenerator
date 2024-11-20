<template>
  <div id="app">
    <QrCodeGenerator />
  </div>
</template>

<script>
import QrCodeGenerator from './QrCodeGenerator.vue';

export default {
  components: {
    QrCodeGenerator
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
