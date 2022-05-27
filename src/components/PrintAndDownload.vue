<template>
  <div class="printAndDownlaod">
    <div class="qrCodeSetting notSection">
      <span>設定:</span>
      <!-- radio size 開始 -->
      <div class="radioBtn form-check-inline ms-2">
        <div class="form-check-inline">
          <input
            class="form-check-input"
            type="radio"
            name="flexRadio"
            v-model="selfSize"
            :value="500"
          />
          <label class="form-check-label" for="flexRadioLarge"> 大 </label>
        </div>
        <div class="form-check-inline">
          <input
            class="form-check-input"
            type="radio"
            name="flexRadio"
            v-model="selfSize"
            :value="300"
          />
          <label class="form-check-label" for="flexRadioSmall"> 中 </label>
        </div>
        <div class="form-check-inline">
          <input
            class="form-check-input"
            type="radio"
            name="flexRadio"
            v-model="selfSize"
            :value="100"
          />
          <label class="form-check-label" for="flexRadioSmall"> 小 </label>
        </div>
      </div>
      <!-- radio size 結束 -->

      <!-- 選擇檔案 input 開始 -->
      <div class="selectLogo mt-2">
        <div class="input-group">
          <input
            type="file"
            class="form-control"
            aria-describedby="inputGroupFileAddon04"
            aria-label="Upload"
            @change="selectLoadLogoImage($event)"
          />
        </div>
        <span v-if="hintShow" class="hint">
          只接受圖檔類型.png、.jpg、.svg
        </span>
      </div>
      <!-- 選擇檔案 input 結束 -->
    </div>

    <!-- 生成 qrCode 開始 -->
    <VueQr
      text="https://tanji.104.com.tw"
      :size="qrCodeSize"
      :margin="10"
      colorDark="#0074d9"
      :logoSrc="src2"
      :logoMargin="10"
      logoBackgroundColor="#008000"
      qid="tanjiId"
      :callback="qrCodeCallBack"
      class="mt-4"
    />
    <!-- 生成 qrCode 結束 -->

    <br />

    <!-- 按鈕 開始 -->
    <div class="btn notSection">
      <button type="button" class="btn btn-success" @click.capture="print">
        列印
      </button>
      <button type="button" class="btn btn-primary m-2" @click="download">
        下載 .pdf
      </button>
    </div>
    <!-- 按鈕 結束 -->
  </div>
</template>

<script>
import VueQr from "vue-qr";
import src2 from "../assets/logo-app.svg";
import axios from "axios";
import jsPDF from "jspdf";

export const getGuide = (param) => {
  return axios({
    url: "/download",
    method: "get",
    params: param,
    responseType: "blob",
  });
};

export default {
  name: "PrintAndDowload",
  components: {
    VueQr,
  },
  data() {
    return {
      src2,
      qrCodeSize: 300,
      imgAsBase64: "",
      hintShow: false,
    };
  },
  computed: {
    selfSize: {
      get() {
        return this.qrCodeSize;
      },
      set(data) {
        this.qrCodeSize = data;
      },
    },
  },
  methods: {
    // qrCode base64 callback
    qrCodeCallBack(dataUrl, id) {
      // console.log(dataUrl, id);
      this.imgAsBase64 = dataUrl;
    },
    // 列印
    print() {
      window.print();
    },
    // 下載 .pdf
    download() {
      // 利用 axios 方式
      /*getGuide()
        .then((res) => {
          let blob = new Blob([res], { type: "application/pdf" });
          let downloadElement = document.createElement("a");
          let href = window.URL.createObjectURL(blob);
          downloadElement.href = href;
          downloadElement.download = "qrCode";
          document.body.appendChild(downloadElement);
          downloadElement.click();
          document.body.removeChild(downloadElement);
          window.URL.revokeObjectURL(href);
        })
        .catch((error) => {
          console.log(error);
        });*/

      // 利用 jsPDF library
      // https://github.com/parallax/jsPDF
      // Docs: http://raw.githack.com/MrRio/jsPDF/master/docs/index.html
      const pdf = new jsPDF("p", "mm", "a4");
      const pxToMm = 0.26;
      const pageWidth = pdf.internal.pageSize.getWidth();
      const pageHeight = pdf.internal.pageSize.getHeight();
      const imgProps = pdf.getImageProperties(this.imgAsBase64);
      // px to mm
      const imgPropsWidth = imgProps.width * pxToMm;
      const imgPropsHeight = imgProps.height * pxToMm;
      // 計算 x、y 置中座標
      const x = (pageWidth - imgPropsWidth) / 2;
      const y = (pageHeight - imgPropsHeight) / 2;
      pdf.addImage(this.imgAsBase64, "PNG", x, y);
      pdf.save("qrCode.pdf");
    },
    // 選擇 Logo 檔案
    selectLoadLogoImage(e) {
      const file = e.target.files[0];
      this.hintShow = false;
      if (!file) return;
      if (!file.type.match("image.*")) {
        this.hintShow = true;
        return;
      }
      const reader = new FileReader();
      reader.onload = (load) => {
        this.src2 = load.srcElement.result;
      };
      reader.readAsDataURL(file);
    },
  },
};
</script>

<style lang="scss" scoped>
.hint {
  color: red;
}

/* 列印去除頭尾以及不顯示其他區塊 */
@media print {
  @page {
    size: A4;
    margin: 0;
    orphans: 4;
    widows: 2;
  }

  .notSection {
    display: none;
  }
}
</style>