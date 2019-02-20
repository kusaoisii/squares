<template>
  <canvas ref="myCanvas" width="600" height="350"></canvas>
</template>

<script>
export default {
  props: {
    distance: {
      type: Number,
      default: 50
    }
  },
  watch: {
    distance() {
      this.draw(this.distance);
    }
  },
  data() {
    return {
      drawspotX: {
        p: this.csHeight / 2,
        m: this.csHeight / 2
      },
      drawspotY: {
        p: this.csWidth / 2,
        m: this.csWidth / 2
      },
      csWidth: this.cs.width,
      csHeight: this.cs.height
    }
  },
  methods: {
    setLength: function(length){
      return length*20;
    },
    // 横線を引く関数
    setHorizontalLine(drawY) {
      this.ctx.beginPath();
      this.ctx.setLineDash([5,15]);
      this.ctx.moveTo(0,drawY);
      this.ctx.lineTo(this.csWidth, drawY);
      this.ctx.closePath();
      this.ctx.stroke();
    },
    //縦線を引く関数
    setVerticalLine(drawX) {
      this.ctx.beginPath();
      this.ctx.setLineDash([5, 15]);
      this.ctx.moveTo(drawX, 0);
      this.ctx.lineTo(drawX, this.csHeight);
      this.ctx.closePath();
      this.ctx.stroke();
    },
    //描写部分 横
    drawHorizontalLine(distance) {
      var Length = this.setLength(distance);
      while(!(this.drawspotX.p >= this.Height || this.drawspotX.m <= 0)){
        this.setHorizontalLine(this.drawspotX.p);
        this.setHorizontalLine(this.drawspotX.m);
        this.drawspotX.p += Length;
        this.drawspotX.m -= Length;
      }
    },
    //描写部分 縦
    drawVeticalLine(distance) {
      var Length = this.setLength(distance);
      while(!(this.drawspotX.p >= this.Height || this.drawspotX.m <= 0)) {
        this.setVerticalLine(this.drawspotY.p);
        this.setVerticalLine(this.drawspotY.m);
        this.drawspotY.p += Length;
        this.drawspotY.m -= Length;
      }
    },
    draw(distance) {
      this.drawHorizontalLine(distance);
      this.drawVeticalLine(distance);
    }
  },
  mounted() {
    // mounted 以降で canvas の DOM にアクセスできる
    // console.log(this.$el)
    this.cs = this.$refs.myCanvas;
    this.ctx = this.cs.getContext('2d');

    this.draw(this.distance);
  }
}
</script>

<style scoped>
.canvas {
  border: 1px solid #000;
}
</style>
