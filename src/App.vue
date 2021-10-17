<script>
import { defineComponent } from 'vue';
import { NConfigProvider, NInput, NDatePicker, NSpace, NButton, NLayout, NLayoutHeader, NLayoutContent } from 'naive-ui';
// theme
import { createTheme, inputDark, datePickerDark } from 'naive-ui';
// locale & dateLocale
import { zhCN, dateZhCN } from 'naive-ui';

export default defineComponent({
  components: {
    NConfigProvider,
    NInput,
    NDatePicker,
    NSpace,
    NButton,
    NLayoutContent,
    NLayout,
    NLayoutHeader,
  },
  setup() {
    return {
      darkTheme: createTheme([inputDark, datePickerDark]),
      zhCN,
      dateZhCN
    };
  }
});
</script>

<template>
  <n-config-provider :theme="darkTheme" :locale="zhCN" :date-locale="dateZhCN">
    <n-space vertical align="center">
      <div id="logo">
        <div class="bg" />
        <div class="content" />
      </div>
      <div class="download-btn animate__animated animate__fadeInRightBig">
        <a target="_blank" to="/linux.tgz">Linux</a>
        <a target="_blank" to="/windows.tgz">Windows</a>
        <a target="_blank" to="/mac.tgz">Mac</a>
      </div>
      <marquee
        class="bottom-marquee"
        scrollamount="16"
      >Monibuca(简称m7s)是一个开源的Go语言实现的流媒体服务器开发框架，独创的插件机制专为二次开发而设计，可以方便用户定制个性化的功能组合，更高效率的利用服务器资源，纯Go编写，不依赖cgo，不依赖FFMpeg或者其他运行时，部署极其方便，对服务器的要求极为宽松，可直接从本页下载可执行文件一键部署</marquee>
    </n-space>
  </n-config-provider>
  <div class="menu">
    <div class="title">&gt;MONIBUCA_ V3.2.2</div>
    <div class="menu-item">
      <a>文档</a>
    </div>
    <div class="menu-item">
      <a>插件</a>
    </div>
    <div class="menu-item">
      <a>支持</a>
    </div>
    <div class="menu-item">
      <a>Jessibuca</a>
    </div>
  </div>
  <div class="qcode-container">
    <div class="qcode">
      <img src="./assets/qcode.jpg" />
    </div>
    <div class="line"></div>
    <marquee>掃描二維碼加微信交流群SCANNING QR CODE PLUS WECHAT COMMUNICATION GROUP 二次元コードと微信交流グループをスキャンする。</marquee>
  </div>
</template>

<style lang="less">
@font-face {
  font-family: "keros";
  src: url("./assets/Kerox-NonCommercial.otf");
}
@qcode: "./assets/qcode.jpg";
#app {
  perspective: calc(100vw / 2);
  -webkit-perspective: calc(100vw / 2);
}
@keyframes debounce {
  from {
    background: repeating-linear-gradient(
      0deg,
      rgb(122 237 255 / 10%),
      rgb(218 146 255 / 20%) 1%
    );
  }
  to {
    background: repeating-linear-gradient(
      0deg,
      rgb(218 146 255 / 20%),
      rgb(122 237 255 / 10%) 1%
    );
  }
}
@keyframes debounce2 {
  from {
    border: 2px solid #b3fffa;
    box-shadow: 0px 0px 20px 6px #0094ff;
  }
  to {
    border: 2px solid cyan;
    box-shadow: 0px 0px 20px 5px #0094ff;
  }
}
body {
  background-image: linear-gradient(#030303 20%, #1e1e1e 40%, #030303);
  background-size: contain;
  background-attachment: fixed;
  color: white;
}
a {
  user-select: none;
  cursor: pointer;
}
.bottom-marquee {
  background: repeating-linear-gradient(0deg, rgb(0 0 0 / 10%), rgb(0 255 255 / 20%) 1%);
  margin-top: 50px;
  padding: 10px;
  font-size: 40px;
  color: #0ff;
  text-shadow: 0 0 20px #0ff;
}
.menu {
  position: fixed;
  top: 20px;
  left: 10px;
  font-size: 40px;
  color: grey;
  & a {
    color: grey;
  }
  & a:hover {
    color: white;
  }
  & .title {
    font-family: keros;
    color: white;
    font-size: 60px;
  }
}
#logo {
  margin-top: 140px;
  width: 400px;
  height: 300px;
  position: relative;
  & > .content {
    background-image: url(./assets/logo.gif);
    background-size: contain;
    position: absolute;
    /* border-radius: 10px; */
    box-shadow: 0px 0px 20px 3px black inset;
    width: 146px;
    height: 110px;
    top: 125px;
    left: 112px;
    z-index: 9;
  }
  & > .bg {
    position: absolute;
    width: 400px;
    height: 300px;
    background-image: url(./assets/tv.png);
    z-index: 10;
  }
}
.download-btn {
  & a {
    text-align: center;
    color: black;
    display: inline-block;
    width: 150px;
    height: 30px;
    line-height: 30px;
    background: white;
    margin: 20px;
  }
}
.qcode-container {
  animation: debounce2 0.1s infinite;
  border: 2px solid #b3fffa;
  transform: rotateY(-60deg);
  box-shadow: 0px 0px 20px 5px #0094ff;
  border-radius: 10px;
  position: fixed;
  right: 50px;
  top: 100px;
  & marquee {
    padding: 40px;
    position: absolute;
    bottom: -120px;
    color: blanchedalmond;
    font-size: 40px;
    text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #fff, 0 0 20px #ff1177,
      0 0 35px #ff1177, 0 0 40px #ff1177, 0 0 50px #ff1177, 0 0 75px #ff1177;
  }
  & .line {
    animation: debounce 0.1s infinite;
    background: repeating-linear-gradient(
      0deg,
      rgb(122 237 255 / 10%),
      rgb(218 146 255 / 20%) 1%
    );
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
  }
  & .qcode {
    background: url(@qcode), #0ff;
    background-blend-mode: lighten;
    background-size: contain;
    box-shadow: 0 0 5px 2px #8cdaff inset;
    border-radius: 10px;
    &:after {
      border-radius: 10px;
      content: "";
      position: absolute;
      margin-left: -99%;
      width: 200px;
      height: 266px;
      background: url(@qcode), #f00;
      background-size: contain;
      background-blend-mode: lighten;
      mix-blend-mode: darken;
    }
    & img {
      width: 200px;
      visibility: hidden;
    }
  }
}
</style>