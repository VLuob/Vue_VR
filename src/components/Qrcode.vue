<template>
  <div class="qrcode">
    <img class="close_btn" src="../assets/close.png" alt="" @click="close" />
    <img class="qrcode_img" src="../assets/qrcode_bbt_tech_1.jpg" alt="" />
    <button class="btn" @click="$emit('setFov')">跳转场景</button>
  </div>
</template>
<script>
export default {
  name: "qrcode",
  methods: {
    close() {
      this.$emit("closeorder", false);
    }
  }
};
</script>
<style scoped>
.qrcode {
  width: 100%;
  height: 100%;
  position: absolute;
  z-index: 4000;
  background: rgba(40, 40, 40, 0.6);
}
.qrcode .close_btn {
  width: 40px;
  height: 40px;
  position: absolute;
  top: 10px;
  left: 10px;
}
.qrcode_img {
  width: 200px;
  height: 200px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-left: -100px;
  margin-top: -100px;
}
.btn {
  position: absolute;
  right: 50px;
  top: 0;
}
</style>
