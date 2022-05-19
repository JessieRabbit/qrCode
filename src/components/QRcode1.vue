<template>
  <div class="qrcanvas">
    <!-- onUpdated 搭配 computed 使用 -->
    <QRCanvas
      :width="200"
      :height="230"
      :options="options1"
      @updated="onUpdated"
    />
    <br />
    <input v-model="text" />
    <br />
    <QRCanvas
      :width="150"
      :height="130"
      :options="options2"
      @updated="onUpdated"
    />
    <QRCanvas :width="150" :height="130" :options="options3" />
    <br />
    <QRCanvas :options="options4" />
    <br />
    <QRCanvas :options="options5" />
    <br />
    <QRCanvas
      :width="200"
      :height="230"
      :options="options6"
      @updated="onUpdated6"
    />
    <br />
    <input v-model="text6" />
    <br />
    <QRCanvas :width="200" :height="230" :options="options7" />
    <QRCanvas :width="130" :height="150" :options="options8" />
    <br />
    <QRCanvas :width="130" :height="150" :options="options9" />
  </div>
</template>

<script>
import { QRCanvas } from "qrcanvas-vue";
import srcLogo from "../assets/logo-app.svg";

export default {
  name: "QRcode1",
  components: {
    QRCanvas,
  },
  data() {
    return {
      text: "https://tanji.104.com.tw",
      srcLogo,
      image: null,
      text6: "tanji",
    };
  },
  computed: {
    options1() {
      return {
        background: "green",
        cellSize: 10,
        data: this.text,
      };
    },
    options2() {
      return {
        background: "#0074d9",
        cellSize: 8,
        data: this.text,
        correctLevel: "H", // "L" | "M" | "Q" | "H"
      };
    },
    options3() {
      return {
        background: "#FFDDAA",
        data: this.text,
        correctLevel: "M",
        logo: {
          image: this.image,
        },
        size: 200,
      };
    },
    options4() {
      return {
        background: "#FFDDAA",
        cellSize: 8,
        data: this.text,
        correctLevel: "L",
        logo: {
          image: this.image,
        },
        padding: 10,
      };
    },
    options5() {
      return {
        background: "#FFDDAA",
        cellSize: 10,
        data: this.text,
        correctLevel: "L",
        logo: {
          text: "tanji",
          options: {
            color: "green",
            fontSize: 24,
            fontFamily: "PingFangTC",
          },
        },
        padding: 20,
      };
    },
    options6() {
      return {
        data: this.text5,
        resize: false,
      };
    },
    options7() {
      return {
        foreground: "orange",
      };
    },
    options8() {
      return {
        foreground: [
          { style: "#55a" },
          // 外方格
          { row: 0, rows: 7, col: 0, cols: 7, style: "#c33" },
          // 內方格
          { row: 2, rows: 3, col: 2, cols: 3, style: "#621" },
        ],
      };
    },
    options9() {
      return {
        effect: { foregroundLight: "#55a", type: "spot", value: 1 },
      };
    },
  },
  created() {
    const image = new Image();
    image.src = this.srcLogo;
    image.onload = () => {
      this.image = image;
    };
  },
  methods: {
    onUpdated(canvas) {
      const ctx = canvas.getContext("2d");
      ctx.textAlign = "center";
      ctx.font = "20px Arial";
      ctx.fillStyle = "red";
      ctx.fillText(this.text, 250, 430);
    },
    onUpdated6(canvas) {
      const ctx = canvas.getContext("2d");
      ctx.clearRect(0, 200, 200, 30);
      ctx.textAlign = "center";
      ctx.font = "20px Arial";
      ctx.fillStyle = "dodgerblue";
      ctx.fillText(this.text6, 100, 220);
    },
  },
};
</script>

<style lang="scss" scoped>
#app canvas {
  border: 2px solid #FFD306;
}

canvas {
  display: inline-block;
}
</style>