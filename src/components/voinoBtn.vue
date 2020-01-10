<template>
  <div id="voinoBtn">
    <section class="voi_container" ref="voi_container">
      <section class="voi_child_box">
        <div class="voi_child" id="voiUpBtn">
          <div class="voi_child_content"></div>
        </div>
        <div class="voi_child" title="下一首">
          <div class="voi_arrow_right">
            <div class="voi_arrow_left_line"></div>
            <div class="voi_arrow_left_line"></div>
          </div>
          <div class="voi_child_content"></div>
        </div>
        <div class="voi_child">
          <div class="voi_child_content"></div>
        </div>
        <div class="voi_child" title="上一首">
          <div class="voi_arrow_left">
            <div class="voi_arrow_left_line"></div>
            <div class="voi_arrow_left_line"></div>
          </div>
          <div class="voi_child_content"></div>
        </div>
      </section>
      <!-- voi_child_box -->
      <section class="voi_main_box" ref="voi_main_box">
        <div class="voi_main_svg_box" ref="voi_main_svg_box">
          <svg viewBox="0 0 1024 1024" width="50">
            <path class="play_svg voi_svg" ref="play_svg" />
          </svg>
        </div>
        <div class="voi_main_content"></div>
      </section>
    </section>
    <!-- voi_container -->
  </div>
</template>
<script>
export default {
  name: "voinoBtn",
  data() {
    return {};
  },
  mounted() {
    let voi_is_on = true;
    this.$refs.voi_main_box.onmouseup = () => {
      if (voi_is_on) {
        this.$refs.play_svg.style.d = "path('M128 128h768v768H128z')";
        this.$refs.voi_main_svg_box.style.paddingLeft = "0px";
        voi_is_on = !voi_is_on;
      } else {
        this.$refs.play_svg.style.d =
          "path('M862.7 528L178.4 908.3c-7.9 4.4-14.7 5-20.4 1.5-5.6-3.5-8.5-9.6-8.5-18.5V132.8c0-8.9 2.8-15.1 8.5-18.5 5.6-3.5 12.5-2.9 20.4 1.5L862.7 496c7.9 4.4 11.8 9.8 11.8 15.9 0 6.3-4 11.7-11.8 16.1z')";
        this.$refs.voi_main_svg_box.style.paddingLeft = "10px";
        voi_is_on = !voi_is_on;
      }
    };
    //获取元素
    let wrapBtnListBigBox = this.$refs.voi_container;
    // let dragStage = document.getElementsByClassName('dragStage')[0];
    let x = 0;
    let y = 0;
    let l = 0;
    let t = 0;
    let isDown = false;
    //鼠标按下事件
    wrapBtnListBigBox.onmousedown = function(e) {
      //获取x坐标和y坐标
      x = e.clientX;
      y = e.clientY;
      // dragStage.style.zIndex = 1;
      //获取左部和顶部的偏移量
      l = wrapBtnListBigBox.offsetLeft;
      t = wrapBtnListBigBox.offsetTop;
      //开关打开
      isDown = true;
      //设置样式
      wrapBtnListBigBox.style.cursor = "move";
    };
    //鼠标移动
    window.onmousemove = function(e) {
      if (isDown == false) {
        return;
      }
      //获取x和y
      // dragStage.style.zIndex = 1;
      let nx = e.clientX;
      let ny = e.clientY;
      //计算移动后的左偏移量和顶部的偏移量
      let nl = nx - (x - l);
      let nt = ny - (y - t);

      wrapBtnListBigBox.style.left = nl + "px";
      wrapBtnListBigBox.style.top = nt + "px";
    };
    //鼠标抬起事件
    wrapBtnListBigBox.onmouseup = function() {
      //开关关闭
      isDown = false;
      // dragStage.style.zIndex = "-1";
      wrapBtnListBigBox.style.cursor = "default";
    };
  }
};
</script>
<style scoped>
body {
  margin: 0;
  padding: 0;
  background-color: #404355;
}
.voi_container {
  position: fixed;
  left: calc(100% - 150px);
  top: calc(100% - 200px);
  transform:scale(0.7);
  z-index: 3;
}
.voi_child {
  width: 60px;
  height: 60px;
  background: #ec5555;
  position: absolute;
  transform: rotate(45deg);
  cursor: pointer;
  transition: all 0.3s ease;
}
.voi_child:hover {
  background: #fff;
}
.voi_child:active {
  filter: brightness(85%);
}
.voi_child:hover .voi_arrow_left_line {
  background: #ec5555;
}
.voi_child_unable {
  cursor: default;
}
.voi_child_unable:hover {
  background: #ec5555;
}
.voi_child_unable:active {
  filter: brightness(100%);
}
.voi_child_content {
  position: relative;
  transform: rotate(-45deg);
}
.voi_child_box > .voi_child:nth-child(1) {
  top: 0px;
  left: 0px;
}
.voi_child_box > .voi_child:nth-child(2) {
  top: 50px;
  left: 50px;
}
.voi_child_box > .voi_child:nth-child(3) {
  top: 100px;
  left: 0px;
}
.voi_child_box > .voi_child:nth-child(4) {
  top: 50px;
  left: -50px;
}
.voi_main_box {
  top: 40px;
  width: 80px;
  left: -10px;
  height: 80px;
  background: #fff;
  position: absolute;
  transform: rotate(45deg);
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.4);
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.3s ease;
}
.voi_main_box:hover {
  background: #ec5555;
}
.voi_main_box:active {
  filter: brightness(85%);
}
.voi_main_content {
  transform: rotate(-45deg);
}
.voi_main_svg_box {
  display: flex;
  padding-left: 10px;
  align-items: center;
  justify-content: center;
  transform: rotate(-45deg);
}
.voi_svg {
  fill: #ec5555;
}
.play_svg {
  transition: all 0.3s ease;
  d: path(
    "M862.7 528L178.4 908.3c-7.9 4.4-14.7 5-20.4 1.5-5.6-3.5-8.5-9.6-8.5-18.5V132.8c0-8.9 2.8-15.1 8.5-18.5 5.6-3.5 12.5-2.9 20.4 1.5L862.7 496c7.9 4.4 11.8 9.8 11.8 15.9 0 6.3-4 11.7-11.8 16.1z"
  );
}
.voi_main_box:hover .voi_svg {
  fill: #fff;
}
.voi_arrow_left {
  position: relative;
  left: 10px;
  top: -10px;
}
.voi_arrow_right {
  position: relative;
  left: 50px;
  top: -50px;
}
.voi_arrow_left_line {
  background: #fff;
  position: absolute;
  transition: all 0.3s ease;
}
.voi_arrow_left .voi_arrow_left_line:nth-child(1) {
  width: 5px;
  height: 20px;
  top: 40px;
  left: 0px;
}
.voi_arrow_left .voi_arrow_left_line:nth-child(2) {
  width: 20px;
  height: 5px;
  top: 55px;
  left: 0px;
}
.voi_arrow_right .voi_arrow_left_line:nth-child(1) {
  width: 5px;
  height: 20px;
  top: 60px;
  left: -5px;
}
.voi_arrow_right .voi_arrow_left_line:nth-child(2) {
  width: 20px;
  height: 5px;
  top: 60px;
  left: -20px;
}
</style>