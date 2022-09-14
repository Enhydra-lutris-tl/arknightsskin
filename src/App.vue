<template>
<div class="main-box">
   <LeftBox></LeftBox>
  <RightBox></RightBox>
</div>


</template>

<script>
import LeftBox from '@/components/LeftBox'
import RightBox from '@/components/RightBox'
export default {
  name: 'App',
  components: {
    LeftBox,
    RightBox
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  text-align: center;
}
.main-box{
  position: absolute;
  left: calc(50% - 517px);
  top: calc(50% - 290px);
  display: flex;
  width: 1035px;
  height: 580px;
}
</style>
