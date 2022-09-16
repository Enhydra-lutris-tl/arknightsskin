<template>
  <div class="left-box">
    <img ref="backImageBox" class="back-image" :src="backImage.imgSrc[backImage.imgSrcNumber]" alt="1111"/>
    <div class="subject-name-box" ref="subjectNameBox"></div>
    <div class="triangle-right"></div>
    <div class="triangle-left one" ref="triangleOne"></div>
    <div class="triangle-left two" ref="triangleTwo"></div>
    <div class="min-people-box">
      <div class="min-people-top" ref="minPeopleTop">
        <div class="min-people-top-box"></div>
        <div class="min-people-top-box"></div>
      </div>
      <div class="min-people-bottom" ref="minPeopleBottom">
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
    <ul class="color-lists" ref="colorLists">
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
    <!--    头像-->
    <div class="head-portrait-box" ref="headPortraitBox">
      <div></div>
      <div class="head-portrait"></div>
    </div>
    <!--    半身像-->
    <div class="bust-box" ref="bustBox">
      <div></div>
      <div class="bust"></div>
    </div>
  </div>
</template>

<script>
import {ref, reactive, watch, computed} from 'vue'

export default {
  name: "LeftBox",
  props: ['imgNumber'],
  setup(props) {
    // dom元素
    const triangleOne = ref()
    const triangleTwo = ref()
    const subjectNameBox = ref()
    const minPeopleTop = ref()
    const minPeopleBottom = ref()
    const bustBox = ref()
    const headPortraitBox = ref()
    const colorLists = ref()
    const introBox = ref()
    const backImageBox = ref()
    // 数据
    const backImage = reactive({
      imgSrcNumber: 1,
      imgSrc: [
        require('@/assets/img/赤东-皮肤.png'),
        require('@/assets/img/史尔特尔-皮肤.png'),
        require('@/assets/img/羽毛笔-皮肤.png'),
        require('@/assets/img/铃兰-皮肤.png'),
        require('@/assets/img/罗小黑-皮肤.png'),
      ]
    })
    const NumberChange = computed(() => {
      return props.imgNumber
    })
    // 函数
    // 框体移动
    function rightBottomChange() {
      // 皮肤系列名移动
      subjectNameBox.value.style.left = '-200px'
      // 左上颜色块移动
      minPeopleTop.value.style.left = '-200px'
      minPeopleTop.value.style.top = '-200px'
      // 右下颜色块移动
      minPeopleBottom.value.style.right = '-300px'
      minPeopleBottom.value.style.bottom = '-300px'
      // 其他框体移动
      bustBox.value.style.right = '-100%'
      headPortraitBox.value.style.right = '-100%'
      introBox.value.style.right = '-100%'
      colorLists.value.style.bottom = '-170px'
      setTimeout(() => {
        subjectNameBox.value.style.left = '18px'
        introBox.value.style.right = '26px'
        colorLists.value.style.bottom = '18px'
      }, 200)

      setTimeout(() => {
        bustBox.value.style.right = '26px'
        headPortraitBox.value.style.right = '26px'

        minPeopleTop.value.style.left = '0'
        minPeopleTop.value.style.top = '0'

        minPeopleBottom.value.style.right = '0'
        minPeopleBottom.value.style.bottom = '0'
      }, 400)

    }

    // function BackImgChange(){
    //
    // }
    watch(NumberChange, (newValue) => {
      rightBottomChange()
      // 图片变化
      if (newValue % 2 === 1) {
        triangleOne.value.style.transform = 'rotate(0)'
        triangleOne.value.style.zIndex = '1'
        triangleTwo.value.style.zIndex = '0'
        setTimeout(() => {
          triangleTwo.value.style.transform = 'rotate(30deg)'
        }, 500)

      } else {
        triangleTwo.value.style.transform = 'rotate(0)'
        triangleOne.value.style.zIndex = '0'
        triangleTwo.value.style.zIndex = '1'
        setTimeout(() => {
          triangleOne.value.style.transform = 'rotate(30deg)'
        }, 500)


      }

      backImageBox.value.style.top = '100%'
      setTimeout(() => {
        backImageBox.value.style.top = '-5%'
        backImage.imgSrcNumber = newValue
      }, 200)
    })
    return {
      triangleOne,
      triangleTwo,
      subjectNameBox,
      minPeopleTop,
      minPeopleBottom,
      bustBox,
      headPortraitBox,
      colorLists,
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
  z-index: 3;
  top: -5%;
  left: -5px;
  height: 112%;
  transition: 0.5s;
}

.subject-name-box {
  position: absolute;
  top: 120px;
  left: 18px;
  z-index: 2;
  height: 80px;
  width: 150px;
  background: rgba(255, 255, 255, 0.44);
  transition: 0.3s;
}

.triangle-left {
  position: absolute;
  left: 0;
  top: -222px;
  border-width: 222px 390px 222px 390px;
  border-style: solid;
  border-color: transparent;
  border-left-color: rgb(111, 140, 154);
  transition: 0.6s;
}

.triangle-left.two {
  z-index: 1;
  border-left-color: rgb(223, 70, 21);
  transform: rotate(30deg);
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
  transition: 0.5s;
}

.min-people-bottom {
  position: absolute;
  bottom: 0;
  right: 0;
  transition: 0.5s;
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
  transition: 0.3s;
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
  transition: 0.3s;
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
  transition: 0.5s;
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
  transition: 0.5s;
}

.bust-box div:first-child {
  box-sizing: border-box;
  height: 100%;
  width: 100%;
  border: white solid 12px;
}
</style>