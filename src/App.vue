<template>
  <div id="app">
    <!-- https://github.com/gera2ld/qrcanvas-vue -->
    <!-- Docs: https://gera2ld.github.io/qrcanvas/docs/interfaces/qrcanvasoptions.html#background -->
    <!-- 11 kB 有支援 vue3 -->
    <!-- <QRcode1 /> -->

    <!-- 5.27 MB 有支援 vue3，Not support IE -->
    <!-- https://github.com/Binaryify/vue-qr -->
    <!-- Docs: https://github.com/SumiMakito/Awesome-qr.js#componentoptions -->
    <!-- <QRcode2 /> -->

    <!-- 列印與下載 開始 -->
    <PrintAndDownload />
    <!-- 列印與下載 結束 -->
  </div>
</template>

<script>
// import QRcode1 from "./components/QRcode1";
// import QRcode2 from "./components/QRcode2";
import PrintAndDownload from "./components/PrintAndDownload";

export default {
  name: "App",
  components: {
    // QRcode1,
    // QRcode2,
    PrintAndDownload,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
