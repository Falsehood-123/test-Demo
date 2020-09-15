<template>
  <div>
    <div class="left">
      <img class="leftImg" src="../../public/image/test.jpg" alt="">
      <!-- 层罩 -->
      <div v-show="topShow" class="top" :style="topStyle"></div>
      <div class="maskTop"
      @mouseenter="enterHandler"
      @mousemove="moveHandler"
      @mouseout="outHandler"></div>
    </div>
    <div v-show="rShow" class="right">
      <img :style="r_img" class="rightImg" src="../../public/image/test.jpg" alt="">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      topStyle:{transform:''},
      r_img: {},
      topShow:false,
      rShow:false
    }
  },
  mounted() {},
  methods : {
    enterHandler() {
      // 层罩及放大空间的显示
      this.topShow = true
      this.rShow = true
    },
    moveHandler(event) {
      // 鼠标的坐标位置
      let x = event.offsetX
      let y = event.offsetY
      // 层罩的左上角坐标位置，并对其进行限制：无法超出原图区域左上角
      let topX = (x-100) < 0 ? 0:(x-100)
      let topY = (y-100) < 0 ? 0:(y-100)
      // 对层罩位置再一次限制，保证层罩只能在原图区域空间内
      if(topX>200) {
        topX = 200
      }
      if(topY>200) {
        topY = 200
      }
      // 通过 transform 进行移动控制
      this.topStyle.transform = `translate(${topX}px,${topY}px)`
      this.r_img.transform = `translate(-${2*topX}px,-${2*topY}px)`
    },
    outHandler() {
      // 控制层罩与放大空间的隐藏
      this.topShow = false
      this.rShow = false
    }
  }
}
</script>

<style scoped>
/* 放大的图片，通过定位将左上角定位到(0,0) */
.rightImg {
  display: inline-block;
  width: 800px;
  height: 800px;
  position: absolute;
  top: 0;
  left: 0;
}
/* 右边的区域图片放大空间 */
.right {
  margin-left: 412px;
  width: 400px;
  height: 400px;
  border: 1px solid red;
  position: relative;
  overflow: hidden;
}
/* 一个最高层层罩 */
.maskTop {
  width: 400px;
  height: 400px;
  position: absolute;
  z-index: 1;
  top: 0;
  left: 0;
}
/* 层罩，通过定位将左上角定位到(0,0) */
.top {
  width: 200px;
  height: 200px;
  background-color: lightcoral;
  opacity: 0.4;
  position: absolute;
  top: 0;
  left: 0;
}
/* 原图的显示 */
.leftImg {
  width: 400px;
  height: 400px;
  display: inline-block;
}
/* 原图的容器 */
.left {
  width: 400px;
  height: 400px;
  border: 1px solid teal;
  float: left;
  position: relative;
}
</style>
