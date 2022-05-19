<template>
  <div class="qrCode3">
    <VueQr
      text="https://tanji.104.com.tw"
      :size="300"
      :margin="10"
      colorDark="#0074d9"
      :logoSrc="src2"
      :logoMargin="10"
      logoBackgroundColor="#008000"
      :callback="test"
      qid="tanjiId"
    />
    <VueQr
      text="https://tanji.104.com.tw"
      :components="{
        cornerAlignment: {
          scale: 0.5,
          protectors: true,
        },
      }"
    />
    <VueQr
      text="https://tanji.104.com.tw"
      :components="{
        cornerAlignment: {
          scale: 1,
          protectors: true,
        },
      }"
    />
    <VueQr
      text="https://tanji.104.com.tw"
      colorDark="#28D905"
      colorLight="#EB0303"
      backgroundColor="#EB0303"
      :margin="10"
      :bindElement="true"
      :callback="test"
    />
    <VueQr
      text="https://tanji.104.com.tw"
      :correctLevel="0"
      backgroundColor="rgb(255,255,0)"
    />
    <VueQr
      text="https://tanji.104.com.tw"
      :correctLevel="1"
      colorLight="rgb(255,0,0)"
    />
    <VueQr
      text="https://tanji.104.com.tw"
      :correctLevel="1"
      colorLight="rgb(0,255,0)"
    />
    <VueQr text="https://tanji.104.com.tw" :correctLevel="2" />
    <VueQr
      :bgSrc="src"
      :logoSrc="src2"
      text="https://tanji.104.com.tw"
      :size="260"
      :margin="0"
      :dotScale="0.5"
    />
    <VueQr
      :bgSrc="src"
      :logoSrc="src2"
      text="https://tanji.104.com.tw"
      :size="260"
      :margin="50"
      :dotScale="0.5"
    />
    <VueQr
      :bgSrc="src"
      :logoSrc="src2"
      text="https://tanji.104.com.tw"
      :size="260"
      :margin="0"
      :dotScale="0.5"
      logoBackgroundColor="rgb(255,0,0)"
      :logoMargin="10"
    />

    <VueQr text="https://tanji.104.com.tw" :bgSrc="src" />
    <VueQr :text="time + ''" />
    <VueQr :bgSrc="src2" text="探吉" :size="260" :margin="0" :dotScale="0.6" />
    <VueQr :bgSrc="src2" text="探吉" :size="300" :dotScale="0.5" />
    <VueQr text="探吉" :callback="test" qid="testid" :size="300" />
    <VueQr
      text="123232312313133"
      :gifBgSrc="gifBgSrc1"
      :size="300"
      :dotScale="0.4"
      :logoSrc="src2"
    />
    <VueQr
      text="123232312313133"
      :gifBgSrc="gifBgSrc2"
      :size="300"
      :dotScale="0.4"
    />
    <VueQr
      text="123232312313133"
      :gifBgSrc="gifBgSrc2"
      :size="300"
      backgroundDimming="rgb(255,0,0)"
      colorDark="rgb(0,0,0)"
      :dotScale="0.5"
    />
  </div>
</template>

<script>
import VueQr from "vue-qr";
import src from "../assets/logo.png";
import src2 from "../assets/logo-app.svg";
import gifBgSrc1 from "../assets/baby.gif";
import gifBgSrc2 from "../assets/baby2.gif";

export default {
  name: "QRcode2",
  components: {
    VueQr,
  },
  data() {
    return {
      src,
      src2,
      time: 0,
      gifBgSrc1,
      gifBgSrc2,
    };
  },
  mounted() {
    setInterval(() => {
      this.time++;
    }, 1000);
  },
  methods: {
    test(dataUrl, id) {
      console.log(dataUrl, id);
    },
  },
};
</script>