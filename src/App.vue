<template>
  <div class="example">
    <MyCanvas :distance="distance"/>
    <p><input type="range" min="1" max="100" v-model.number="distance"></p>
    <p>{{distance}}</p>
  </div>
</template>

<script>
// キャンバス用コンポーネントの読み込み
import MyCanvas from './components/MyCanvas.vue'
export default {
  components: {
    MyCanvas
  },
  data() {
    return {
      distance: 50
    }
  }
}
</script>
