<script>
  import { defineComponent } from 'vue'
  import { NConfigProvider, NInput, NDatePicker, NSpace } from 'naive-ui'
  // theme
  import { createTheme, inputDark, datePickerDark } from 'naive-ui'
  // locale & dateLocale
  import { zhCN, dateZhCN } from 'naive-ui'

  export default defineComponent({
    components: {
      NConfigProvider,
      NInput,
      NDatePicker,
      NSpace
    },
    setup() {
      return {
        darkTheme: createTheme([inputDark, datePickerDark]),
        zhCN,
        dateZhCN
      }
    }
  })
</script>

<template>
  <n-config-provider :theme="darkTheme" :locale="zhCN" :date-locale="dateZhCN">
    <n-space vertical>
      <n-space justify="center">
        <div id="logo" >
          <div/>
        </div>
          
      </n-space>
    </n-space>
  </n-config-provider>
</template>

<style>
  body {
    background-image:linear-gradient(#030303 20%, #1e1e1e 40%,#030303);
    background-size: contain;
    background-attachment: fixed;
  }
  #logo{
    margin-top: 100px;
    width: 400px;
    height: 300px;
    background-image: url(./assets/tv.jpeg);
    position: relative;
  }
  #logo>div {
    background-image: url(./assets/logo.gif);
    background-size: contain;
    position: absolute;
    border-radius: 10px;
    box-shadow: 0px 0px 20px 7px black inset;
    width: 140px;
    height: 105px;
    top: 130px;
    left: 118px;
  }
</style>