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
  methods: {
    share() {
      html2canvas(document.getElementById('test')).then(function (canvas) {
        console.log(canvas.toDataURL('image/png', 1).replace('data:image/png;base64,', ''))
        jsBridge.ShareEvent({
          data: {
            title: 'test',
            url: 'test',
            imageData: canvas.toDataURL('image/png', 1).replace('data:image/png;base64,', ''),
            type: 2
          }
        })
      })
    }
  }
}
</script>
