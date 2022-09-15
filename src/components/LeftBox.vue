<template>
  <div class="left-box">
    <img ref="backImageBox" class="back-image" :src="backImage.imgSrc[backImage.imgSrcNumber]" alt="1111"/>
    <div class="subject-name-box"></div>
    <div class="triangle-right"></div>
    <div class="triangle-left"></div>
    <div class="min-people-box">
      <div class="min-people-top">
        <div class="min-people-top-box"></div>
        <div class="min-people-top-box"></div>
      </div>
      <div class="min-people-bottom">
        <div class="min-people-bottom-box"></div>
        <div class="min-people-bottom-box"></div>
      </div>
    </div>
    <!--    时装简介-->
    <div class="intro-box" ref="introBox">
      <ul class="intro-title-box">
        <li class="intro-main-title">EPOQUE</li>
        <li class="intro-minor-title">NEW ARRIVALS</li>
        <li class="intro-author-box">
          <div class="intro-author-name">Akafuyu</div>
          <div class="intro-author-pseudonym">熊太</div>
        </li>
        <li class="intro-minor-text">EPOQUE系列新款/心性。利落的剪裁和用色极具现代感,装饰单品则在细节处保留了古典韵味,眼镜是品牌为顾客定制的赠礼。</li>
      </ul>
      <div class="intro-right-box"></div>
    </div>
    <!--    色彩条-->
    <ul class="color-lists">
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
    <!--    头像-->
    <div class="head-portrait-box">
      <div></div>
      <div class="head-portrait"></div>
    </div>
    <!--    半身像-->
    <div class="bust-box">
      <div></div>
      <div class="bust"></div>
    </div>
  </div>
</template>

<script>
import {ref,reactive,watch,computed} from 'vue'

export default {
  name: "LeftBox",
  props:['imgNumber'],
  setup(props) {
    const introBox = ref()
    const backImageBox = ref()
    const backImage = reactive({
      imgSrcNumber:1,
      imgSrc: [
        require('@/assets/img/赤东-皮肤.png'),
        require('@/assets/img/史尔特尔-皮肤.png'),
        require('@/assets/img/羽毛笔-皮肤.png'),
        require('@/assets/img/赤东-皮肤.png'),
        require('@/assets/img/史尔特尔-皮肤.png'),
      ]
    })
    const NumberChange = computed(()=>{
      return props.imgNumber
    })
    watch(NumberChange,(newValue,oldValue)=>{
      // 右下角介绍框移动
      introBox.value.style.right = '-100%'
      setTimeout(()=>{
        introBox.value.style.right = '26px'
      },500)
      // 图片变化
      backImageBox.value.style.top = '100%'
      setTimeout(()=>{
        backImageBox.value.style.top = '-5%'
        backImage.imgSrcNumber = newValue
      },200)
      console.log(introBox.value.style.right)
      console.log(newValue,oldValue)
    })
    return {
      introBox,
      backImageBox,
      backImage,
      NumberChange
    }

  }
}
</script>

<style scoped>
.left-box {
  position: relative;
  background: rgb(173, 173, 173);
  width: 650px;
  height: 580px;
  overflow: hidden;
}

.back-image {
  position: absolute;
  z-index: 2;
  top: -5%;
  left: -5px;
  height: 112%;
  transition: 0.5s;
}

.subject-name-box {
  position: absolute;
  top: 120px;
  left: 18px;
  z-index: 1;
  height: 80px;
  width: 150px;
  background: rgba(255, 255, 255, 0.44);
}

.triangle-left {
  position: absolute;
  left: 0;
  top: -222px;
  border-width: 222px 390px 222px 390px;
  border-style: solid;
  border-color: transparent;
  border-left-color: rgb(111, 140, 154);
  animation: ceshi 1s;
}

@keyframes ceshi {
  0% {
    transform: rotate(0deg);
  }
  50% {
    transform: rotate(30deg);
  }
  100% {
    transform: rotate(0deg);
  }
}

.triangle-right {
  position: absolute;
  right: 0;
  top: -222px;
  border-width: 222px 390px 222px 390px;
  border-style: solid;
  border-color: transparent;
  border-right-color: rgb(222, 222, 222);
}

.min-people-box {
  position: absolute;
  z-index: 4;
  left: 30px;
  top: 308px;
  height: 136px;
  width: 136px;
  background: rgba(255, 255, 255, 0.5);
}

.min-people-top-box:first-child {
  position: absolute;
  top: -17px;
  left: -11px;
  width: 61px;
  height: 24px;
  background: rgb(92, 81, 119);
}

.min-people-top-box:last-child {
  position: absolute;
  top: -17px;
  left: -11px;
  height: 64px;
  width: 24px;
  background: rgb(92, 81, 119);
}

.min-people-top {
  position: absolute;
  left: 0;
  top: 0;
}

.min-people-bottom {
  position: absolute;
  bottom: 0;
  right: 0;
}

.min-people-bottom-box:first-child {
  position: absolute;
  bottom: -8px;
  right: -11px;
  width: 61px;
  height: 24px;
  background: rgb(43, 80, 109);
}

.min-people-bottom-box:last-child {
  position: absolute;
  bottom: -8px;
  right: -14px;
  height: 64px;
  width: 24px;
  background: rgb(43, 80, 109);
}

/*右下角介绍框*/
.intro-box {
  position: absolute;
  z-index: 4;
  right: 26px;
  bottom: 18px;
  display: flex;
  height: 170px;
  width: 190px;
  background: rgb(43, 80, 109);
  transition: 0.5s;
}

.intro-title-box {
  flex: 1;
  list-style: none;
  margin-left: 8px;
}

.intro-main-title {
  font-size: 38px;
  font-weight: bold;
  color: white;
  text-align: left;
}

.intro-minor-title {
  background: white;
  color: rgb(43, 80, 109);
  width: 86px;
  height: 10px;
  font-size: 10px;
  line-height: 10px;
  font-weight: bold;
}

.intro-author-box {
  margin-top: 10px;
  height: 34px;
  width: 156px;
  background: rgb(113, 127, 132);
  font-size: 12px;
  color: white;
}

.intro-minor-text {
  padding-right: 10px;
  margin-top: 2px;
  font-size: 9px;
  line-height: 9px;
  text-align: left;
  color: white;
}

.color-lists {
  height: 170px;
  width: 3px;
  position: absolute;
  z-index: 4;
  right: 14px;
  bottom: 18px;
  list-style: none;
}

.color-lists li {
  height: 25%;
  width: 100%;
}

.color-lists li:nth-child(1) {
  background: rgb(0, 255, 255);
}

.color-lists li:nth-child(2) {
  background: rgb(255, 0, 255);
}

.color-lists li:nth-child(3) {
  background: rgb(255, 255, 0);
}

.color-lists li:nth-child(4) {
  background: rgb(0, 0, 0);
}

.intro-right-box {
  width: 18px;
  height: 100%;
  background: rgb(47, 47, 47);
}

/*头像相关*/
.head-portrait-box {
  height: 110px;
  width: 110px;
  position: absolute;
  z-index: 4;
  right: 26px;
  top: 40px;
}

.head-portrait-box div:first-child {
  box-sizing: border-box;
  height: 100%;
  width: 100%;
  border: white solid 12px;
}

/*半身像*/
.bust-box {
  height: 220px;
  width: 110px;
  position: absolute;
  z-index: 4;
  right: 26px;
  top: 162px;
}

.bust-box div:first-child {
  box-sizing: border-box;
  height: 100%;
  width: 100%;
  border: white solid 12px;
}
</style>