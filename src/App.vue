<script lang="ts">
import { defineComponent, reactive, ref } from 'vue';
import { NConfigProvider, NCard, NModal, NSpace, NButton, NLayout, NLayoutHeader, NLayoutContent, NRadio, NRadioGroup, NTabPane, NTabs } from 'naive-ui';
import { createTheme, modalDark, cardDark, radioDark, tabsDark } from 'naive-ui';
// locale & dateLocale
import { zhCN, dateZhCN } from 'naive-ui';
import MarqueeVue from './components/Marquee.vue';
import LiveStage from './components/LiveStage.vue';
import WatchStage from './components/WatchStage.vue';
import RouteStage from './components/RouteStage.vue';
import MoreStage from './components/MoreStage.vue'
import { subject, pipe, subscribe, switchMap, timer } from 'fastrx';
export default defineComponent({
  components: {
    MarqueeVue,
    NRadioGroup,
    NRadio,
    NConfigProvider,
    NCard,
    NModal,
    NSpace,
    NButton,
    NLayoutContent,
    NLayout, NTabPane, NTabs, WatchStage,
    NLayoutHeader, LiveStage, RouteStage,MoreStage
  },
  setup() {
    const changePayOb = subject<'alipay' | 'wechat'>();
    const checkedValue = ref('alipay');
    const payClass = reactive({
      alipay: '',
      wechat: ''
    });
    let lastValue = 'alipay';
    pipe(changePayOb, switchMap(value => {
      payClass[lastValue] = 'animate__flipOutY';
      lastValue = value;
      return timer(250);
    }), subscribe(() => {
      checkedValue.value = lastValue;
      payClass[lastValue] = 'animate__flipInY';
    }));
    return {
      version: 'v3.0.7',
      payClass,
      darkTheme: createTheme([modalDark, cardDark, radioDark, tabsDark]),
      zhCN,
      dateZhCN,
      showModal: ref(false),
      showStage: ref(false),
      checkedValue,
      onChangePay(value) {
        changePayOb.next(value);
      }
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
      <div class="download-btn">
        <a
          target="_blank"
          :href="`https://github.com/langhuihui/monibuca/releases/download/${version}/linux.tgz`"
        >Linux</a>
        <a
          target="_blank"
          :href="`https://github.com/langhuihui/monibuca/releases/download/${version}/windows.tgz`"
        >Windows</a>
        <a
          target="_blank"
          :href="`https://github.com/langhuihui/monibuca/releases/download/${version}/mac.tgz`"
        >Mac</a>
      </div>
      <div class="tips">点击上面的按钮下载可执行文件，可以在对应的操作系统上直接运行，无需安装环境</div>
    </n-space>
    <n-modal v-model:show="showStage">
      <n-card
        style="width: 800px; backdrop-filter: blur(5px);--color-modal:rgb(133 133 133 / 25%)"
        :bordered="false"
        size="huge"
      >
        <n-tabs type="line">
          <n-tab-pane name="live stage" tab="直播场景">
            <LiveStage />
          </n-tab-pane>
          <n-tab-pane name="watch stage" tab="监控场景">
            <WatchStage />
          </n-tab-pane>
          <n-tab-pane name="route stage" tab="中转场景">
            <RouteStage />
          </n-tab-pane>
          <n-tab-pane name="more stage" tab="自定义">
            <MoreStage/>
          </n-tab-pane>
        </n-tabs>
      </n-card>
    </n-modal>
    <n-modal v-model:show="showModal">
      <n-card
        style="width: 600px; backdrop-filter: blur(5px);--color-modal:rgb(133 133 133 / 25%)"
        title="支持开源项目更好的发展"
        :bordered="false"
        size="huge"
      >
        <template #header-extra>
          <n-radio-group
            v-model:value="checkedValue"
            name="radiogroup"
            :on-update:value="onChangePay"
          >
            <n-radio value="alipay">支付宝</n-radio>
            <n-radio value="wechat">微信</n-radio>
          </n-radio-group>
        </template>
        <n-space vertical align="center">
          <img
            src="./assets/alipay.jpg"
            height="456"
            v-if="checkedValue === 'alipay'"
            :class="payClass.alipay"
          />
          <img src="./assets/wechat.jpg" height="456" v-else :class="payClass.wechat" />
        </n-space>
        <template #footer>
          <marquee class="thank">感谢以下支持者：Sense、hshev99、兵、Leon、Jack、天空、李亚宁</marquee>
        </template>
      </n-card>
    </n-modal>
  </n-config-provider>
  <div class="menu">
    <div class="title">{{ `>MONIBUCA_ ${version}` }}</div>
    <div class="menu-item">
      <a target="_blank" href="http://docs.m7s.live">文档</a>
    </div>
    <div class="menu-item" @click="showStage = true">
      <a>使用场景</a>
    </div>
    <div class="menu-item" @click="showModal = true">
      <a>支持</a>
    </div>
    <div class="menu-item">
      <a href="https://github.com/langhuihui/monibuca/issues" target="_blank">提bug</a>
    </div>
    <div class="menu-item">
      <a href="https://j.m7s.live" target="_blank">H5播放器</a>
    </div>
  </div>
  <div class="qcode-container">
    <div class="qcode">
      <img src="./assets/qcode.jpg" />
    </div>
    <div class="line"></div>
  </div>
  <marquee
    class="bottom-marquee"
    scrollamount="16"
  >Monibuca(简称m7s)是一个开源的Go语言实现的流媒体服务器开发框架，独创的插件机制专为二次开发而设计，可以方便用户定制个性化的功能组合，更高效率的利用服务器资源，纯Go编写，不依赖cgo，不依赖FFMpeg或者其他运行时，部署极其方便，对服务器的要求极为宽松，可直接从本页下载可执行文件一键部署</marquee>
</template>

<style lang="less">
@font-face {
  font-family: "keros";
  src: url("./assets/Kerox-NonCommercial.otf");
}
@qcode: "./assets/qcode.jpg";
@import url(./assets/an.less);
.tips {
  animation: debounce 0.1s infinite;
  width: 600px;
  padding: 10px;
  color: white;
  text-shadow: 0 0 5px #ff7a7a, 0 0 10px #ffd0d0, 0 0 15px #ff6868,
    0 0 20px #ff1177, 0 0 35px #ff1177;
}
.thank {
  font-size: 30px;
  animation: debounce2 0.1s infinite;
  padding: 10px;
  color: white;
  text-shadow: 0 0 5px #ffd07a, 0 0 10px #fffcd0, 0 0 15px #ffe868,
    0 0 20px #ffac11, 0 0 35px #ffac11;
}
#app {
  perspective: calc(100vw / 2);
  -webkit-perspective: calc(100vw / 2);
  height: 100%;
}
html {
  height: 100%;
}
body {
  background-image: linear-gradient(#030303 20%, #1e1e1e 40%, #030303);
  background-size: contain;
  background-attachment: fixed;
  color: white;
  margin: 0;
  border: 0;
  height: 100%;
}
a {
  user-select: none;
  cursor: pointer;
}
.bottom-marquee {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: repeating-linear-gradient(
    0deg,
    rgb(0 0 0 / 10%),
    rgb(0 255 255 / 20%) 1%
  );
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
  color: #0ff;
  & a {
    color: #0ff;
    font-size: 50px;
    transition: 0.2s ease-out;
    text-decoration: none;
    animation: debounce4 0.1s infinite;
  }
  & a:hover {
    color: #0ff;
    font-size: 55px;
    animation: debounce3 0.1s infinite;
  }
  & .title {
    font-family: keros;
    color: #0ff;
    font-size: 61px;
    mask: repeating-linear-gradient(0deg, #0ff, white 1%);
    -webkit-mask: repeating-linear-gradient(0deg, #0ff, white 1%);
    animation: debounce4 0.1s infinite;
  }
}
#logo {
  margin-top: 140px;
  width: 400px;
  height: 300px;
  position: relative;
  & > .content {
    animation: fadeIn; /* referring directly to the animation's @keyframe declaration */
    animation-duration: 5s; /* don't forget to set a duration! */
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
    color: cyan;
    display: inline-block;
    width: 150px;
    height: 30px;
    line-height: 30px;
    border: 1px solid cyan;
    margin: 20px;
    margin-top: 70px;
  }
}
.qcode-container {
  background: url(./assets/wall.jpg);
  background-repeat: no-repeat;
  position: fixed;
  right: 0;
  top: 0;
  width: 300px;
  height: 200px;
  & .line {
    transition: 0.2s ease-out;
    background-image: radial-gradient(
      farthest-side at 90% 10%,
      rgba(0, 0, 0, 0) 20%,
      rgba(0, 0, 0, 0.56) 35%,
      rgba(0, 0, 0, 0.76) 65%,
      #000000 100%
    );
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 10;
  }
  & .line:hover {
    background-image: radial-gradient(
      farthest-side at 90% 10%,
      rgba(0, 0, 0, 0) 20%,
      rgba(0, 0, 0, 0.56) 65%,
      rgba(0, 0, 0, 0.76) 100%,
      #000000 100%
    );
  }
  & .qcode {
    position: absolute;
    top: 50px;
    right: 50px;
    background: url(@qcode);
    // background: url(@qcode), #0ff;
    // background-blend-mode: lighten;
    background-size: contain;
    // &:after {
    //   content: "";
    //   position: absolute;
    //   margin-left: -99%;
    //   width: 200px;
    //   height: 266px;
    //   background: url(@qcode), #f00;
    //   background-size: contain;
    //   background-blend-mode: lighten;
    //   mix-blend-mode: darken;
    // }
    & img {
      width: 100px;
      visibility: hidden;
    }
  }
}
</style>