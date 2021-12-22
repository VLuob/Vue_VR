<template>
  <div id="wrapper">
    <img
      class="img_btn"
      src="../assets/qrcode.png"
      alt=""
      v-if="!show"
      @click="show = !show"
    />
    <transition
      name="qrcode-transition"
      enter-active-class="showUp"
      leave-active-class="hideDown"
    >
      <div>
        <qrcode v-if="show" @closeorder="getorder" @setFov="setFov"></qrcode>
      </div>
    </transition>
    <div id="pano"></div>
  </div>
</template>
<script>
import Qrcode from "@/components/Qrcode";
export default {
  name: "vtour",
  data() {
    return {
      show: false,
      krpano: null //krpano实例
    };
  },
  mounted() {
    embedpano({
      swf: "./static/vtour/tour.swf",
      xml: "./static/vtour/tour.xml",
      target: "pano",
      html5: "auto",
      mobilescale: this.selectmobilescaleusage(),
      onready: this.krpano_onready_callback,
      passQueryParameters: true
    });
  },
  methods: {
    krpano_onready_callback(krpano_interface) {
      this.krpano = krpano_interface;
    },
    getorder(msg) {
      this.show = msg;
    },
    setFov() {
      this.krpano.call("goto(scene2)"); //js跳转场景
      //set(variable, value) 设置属性值
      //get(variable) 获取属性值
      //call(action) 调用xml中的各种方法
      // var fov = Number(krpano.get("view.fov"));
      // console.log(fov);
      // fov += 10.0;
      // krpano.set("view.fov", fov);
    },
    selectmobilescaleusage() {
      // check for Android MQQBrowser:
      if (
        navigator.userAgent.indexOf("Android") >= 0 &&
        navigator.userAgent.indexOf("YYB") >= 0
      )
        return 0.5;

      // for all other cases use 1:
      return 1;
    }
  },
  components: {
    Qrcode
  }
};
</script>
<style scoped>
#wrapper {
  width: 100%;
  height: 100%;
  position: absolute;
}
#pano {
  width: 100%;
  height: 100%;
}
.img_btn {
  width: 60px;
  height: 60px;
  position: absolute;
  top: 10px;
  right: 6px;
  z-index: 4010;
}
.showUp {
  animation: showup 0.4s ease-in;
}
.hideDown {
  animation: hidedown 0.4s ease-out;
}

@keyframes showup {
  from {
    transform: translateY(110%);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}
@keyframes hidedown {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(110%);
  }
}
</style>
