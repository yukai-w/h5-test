<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div id="test" style="width: 200px; height: 20px;background:red">图片</div>
    <button @click="share">分享测试</button>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import jsBridge from './jsBridge'
import html2canvas from 'html2canvas'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  created () {
    // jsBridge.NativeNetworkRequest({
    //   url: 'internal.validationTokens',
    //   method: 'post',
    //   params: {
    //     token: 'c:app:67F1510767DC46CDB8DCAF6ABD99856A',
    //     greenElectricCode: '11111111111'
    //   }
    // })
    jsBridge.SetTitleBar({
      isShow: false
    })
    jsBridge.NativeNetworkRequest({
      ua: 'E卡',
      url: 'internal.validationTokens',
      encryption: '1',
      method: 'post',
      params: '{"token":"c:app:67F1510767DC46CDB8DCAF6ABD99856A","greenElectricCode":"11111111111"}'
    }, function (res) {
      console.log(res, 123123)
    })
  },
  methods: {
    share() {
      html2canvas(document.getElementById('test')).then(function (canvas) {
        console.log(canvas.toDataURL('image/png', 1).replace('data:image/png;base64,', ''))
        const params = {
          title: 'test',
          url: 'test',
          imageData: canvas.toDataURL('image/png', 1).replace('data:image/png;base64,', ''),
          type: 2
        }
        jsBridge.ShareEvent(params)
      })
    }
  }
}
</script>
