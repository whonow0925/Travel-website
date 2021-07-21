<template>
  <div>
    <div
      class="drawingBoard"
      style="
        margin-bottom: 10px;
        display: flex;
        align-items: center;
        margin-left: 274px;
      "
    >
      <el-button @click="changeType('huabi')" type="primary">画笔</el-button>
      <el-button @click="changeType('rect')" type="success">正方形</el-button>
      <el-button
        @click="changeType('arc')"
        type="warning"
        style="margin-right: 10px"
        >圆形</el-button
      >
      <div>颜色</div>
      <el-color-picker v-model="color"></el-color-picker>
      <el-button @click="clear">清空</el-button>
      <el-button @click="saveImg">保存</el-button>
    </div>
    <canvas
      id="canvas"
      width="800"
      height="400"
      @mousedown="canvasDown"
      @mousemove="canvasMove"
      @mouseout="canvasUp"
      @mouseup="canvasUp"
    ></canvas>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  data() {
    return {
      type: "huabi",
      isDraw: false,
      canvasDom: null,
      ctx: null,
      beginX: 0,
      beginY: 0,
      color: "#000",
      imageData: null,
    };
  },
  mounted() {
    (this as any).canvasDom = document.getElementById("canvas");
    this.ctx = (this as any).canvasDom.getContext("2d");
  },
  methods: {
    changeType(type: any) {
      (this as any).type = type;
    },
    canvasDown(e: any) {
      this.isDraw = true;
      const canvas = this.canvasDom;
      this.beginX = e.pageX - (canvas as any).offsetLeft;
      this.beginY = e.pageY - (canvas as any).offsetTop;
    },
    canvasMove(e: any) {
      if (!this.isDraw) return;
      const canvas = this.canvasDom;
      const ctx = this.ctx;
      const x = e.pageX - (canvas as any).offsetLeft;
      const y = e.pageY - (canvas as any).offsetTop;
      (this as any)[`${this.type}Fn`](ctx, x, y);
    },
    canvasUp() {
      this.imageData = (this as any).ctx.getImageData(0, 0, 800, 400);
      this.isDraw = false;
    },
    huabiFn(ctx: any, x: any, y: any) {
      ctx.beginPath();
      ctx.arc(x, y, 5, 0, 2 * Math.PI);
      ctx.fillStyle = this.color;
      ctx.fill();
      ctx.closePath();
    },
    rectFn(ctx: any, x: any, y: any) {
      const beginX = this.beginX;
      const beginY = this.beginY;
      ctx.clearRect(0, 0, 800, 400);
      this.imageData && ctx.putImageData(this.imageData, 0, 0, 0, 0, 800, 400);
      ctx.beginPath();
      ctx.strokeStyle = this.color;
      ctx.rect(beginX, beginY, x - beginX, y - beginY);
      ctx.stroke();
      ctx.closePath();
    },
    arcFn(ctx: any, x: any, y: any) {
      const beginX = this.beginX;
      const beginY = this.beginY;
      this.isDraw && ctx.clearRect(0, 0, 800, 400);
      this.imageData && ctx.putImageData(this.imageData, 0, 0, 0, 0, 800, 400);
      ctx.beginPath();
      ctx.strokeStyle = this.color;
      ctx.arc(
        beginX,
        beginY,
        Math.round(
          Math.sqrt((x - beginX) * (x - beginX) + (y - beginY) * (y - beginY))
        ),
        0,
        2 * Math.PI
      );
      ctx.stroke();
      ctx.closePath();
    },
    saveImg() {
      const url = (this as any).canvasDom.toDataURL();
      const a = document.createElement("a");
      a.download = "volley";
      a.href = url;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
    },
    clear() {
      (this.imageData = null as any),
        (this as any).ctx.clearRect(0, 0, 800, 400);
    },
  },
});
</script>

<style lang="scss" scoped>
#canvas {
  border: 1px solid black;
}
</style>
