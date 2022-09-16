<template>
  <div class="right-box">
    <div class="title-box">
      <div class="title-top-box">
        <span class="subheading">xxxxxxxxx</span>
        <span class="title">时代/XV</span>
      </div>
      <div class="title-bottom-box"></div>
    </div>
    <div class="image-lists-box">
      <ul class="image-list-box" ref="imageListBox">
        <li class="image-box" v-for="(imgSrc,index) in listImage.imgSrc" :key="index" :ref="'liIndex'">
          <img :src="imgSrc" alt="111">
        </li>
      </ul>
    </div>

    <div class="left-button" @click="leftChange"></div>
    <div class="right-button" @click="rightChange"></div>
  </div>
</template>

<script>
import {reactive, ref} from 'vue'

export default {
  name: "RightBox",
  props:['numberChange'],
  setup(props) {
    const liIndex = ref(null)
    const imageListBox = ref(null)
    const listImage = reactive({
      listNumber: 1,
      imgSrc: [
        require('@/assets/img/赤东-皮肤.png'),
        require('@/assets/img/史尔特尔-皮肤.png'),
        require('@/assets/img/羽毛笔-皮肤.png'),
        require('@/assets/img/铃兰-皮肤.png'),
        require('@/assets/img/罗小黑-皮肤.png'),
      ]
    })

// 左侧切换按钮
    function leftChange() {
      if (listImage.listNumber > 0) {
        liIndex.value.forEach((a) => {
          a.classList.remove('active')
        })
        listImage.listNumber--
        liIndex.value[listImage.listNumber].classList.add('active')
        imageListBox.value.style.left = imageListBox.value.offsetLeft + 64 + 'px'
        props.numberChange(listImage.listNumber)
      }
    }

    // 右侧切换按钮
    function rightChange() {
      if (listImage.listNumber < listImage.imgSrc.length - 1) {
        liIndex.value.forEach((a) => {
          a.classList.remove('active')
        })
        listImage.listNumber++
        liIndex.value[listImage.listNumber].classList.add('active')
        imageListBox.value.style.left = imageListBox.value.offsetLeft - 64 + 'px'
        props.numberChange(listImage.listNumber)
      }
    }

    return {
      liIndex,
      listImage,
      imageListBox,
      leftChange,
      rightChange
    }

  },
  mounted() {
    let startImage = this.$refs.liIndex[1]
    startImage.classList.add('active')
  }
}
</script>

<style scoped>
.right-box {
  position: relative;
  background: rgb(213, 213, 213);
  width: 385px;
  height: 580px;
}

.title-box {
  position: absolute;
  top: 0;
  left: 138px;
}

.title-top-box {
  height: 54px;
  width: 108px;
  background: rgb(111, 140, 154);
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.subheading {
  font-size: 10px;
  color: white;
}

.title {
  color: white;
  font-weight: bold;
}

.title-bottom-box {
  height: 0;
  width: 0;
  border-width: 30px 54px 30px 54px;
  border-style: solid;
  border-color: transparent;
  border-top-color: rgb(111, 140, 154);
}

.image-lists-box {
  position: absolute;
  top: 92px;
  left: 68px;
  width: 254px;
  height: 320px;
  overflow: hidden;
}

.image-list-box {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  list-style: none;
  display: flex;
  transition: 0.5s;
}

.image-box {
  position: relative;
  height: 100%;
  width: 64px;
  background: black;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.5s;
}

.active {
  background: lightskyblue;
  width: 126px;
}

.image-box img {
  height: 370%;
  transition: 0.3s;

}

.left-button {
  position: absolute;
  right: 328px;
  top: 262px;
  height: 0;
  width: 0;
  border-width: 10px 20px;
  border-color: transparent;
  border-style: solid;
  border-right-color: white;
}

.right-button {
  position: absolute;
  left: 328px;
  top: 262px;
  height: 0;
  width: 0;
  border-width: 10px 20px;
  border-color: transparent;
  border-style: solid;
  border-left-color: white;
}
</style>