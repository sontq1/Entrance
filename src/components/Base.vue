<template>
  <div class="wrapper loaded" data-frame="16" data-friction="0.33">
    <div>
      <div class="viewer">
        <span class="btn-left" @click="goToLeft()">
          <img :src="icon.left" alt="left" width="50" height="50">
        </span>
        <span class="btn-right" @click="goToRight()">
          <img :src="icon.right" alt="right" width="50" height="50">
        </span>
        <span class="btn-up" @click="goToUp()">
          <img :src="icon.up" alt="up" width="50" height="50" style="opacity: 0">
        </span>
        <div class="sprite"
             :class="currentDirection.class + ' ' + currentImage.bgClass"></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue'
import head from 'lodash/head'
import find from 'lodash/find'
import Image from './../data/image.json'

export default defineComponent({
  name: 'Base',
  setup () {
    const currentImage = ref(head(Image))
    const currentDirectionId = ref(2)
    const currentDirection = ref(find(currentImage.value.directions, {id: currentDirectionId.value}))
    const icon = {
      left: require('@/assets/icon/chevron-left.png'),
      right: require('@/assets/icon/chevron-right.png'),
      up: require('@/assets/icon/chevron-up.png'),
    }

    const goToLeft = () => {
      if (currentDirectionId.value < 2) return
      currentDirectionId.value -= 1
    }

    const goToRight = () => {
      if (currentDirectionId.value > 2) return
      currentDirectionId.value += 1
    }

    const goToUp = () => {
      const nextImage = find(Image, {id: currentDirection.value.goto})
      if (!nextImage) return
      currentImage.value = nextImage
      currentDirectionId.value = 2
    }

    watch(currentDirectionId, id => {
      currentDirection.value = find(currentImage.value.directions, { id })
    })

    return {
      goToLeft,
      goToRight,
      goToUp,
      currentImage,
      currentDirection,
      icon
    }
  }
})
</script>

<style scoped lang="scss">
.wrapper {
  text-align: center;
  padding: 2em 0;
}
.wrapper > div {
  display: inline-block;
}
.wrapper .viewer {
  /*position: relative;*/
  left: 50px;
  z-index: 1;
  display: inline-block;
  overflow: hidden;
}
.wrapper img {
  display: block;
  position: relative;
  z-index: 1;
}

.wrapper .sprite {
  position: absolute;
  z-index: 2;
  top: 0;
  left: 0;
  height: 100%;
  width: 256%;
  background-size: 100%;
  opacity: 0;
  -webkit-transition: opacity 0.3s;
  -moz-transition: opacity 0.3s;
}
.wrapper.loaded .sprite {
  opacity: 1;
  cursor: ew-resize;
}

.btn-left {
  z-index: 3;
  width: 20%;
  top: 0;
  left: 0;
  position: absolute;
  cursor: pointer;
  padding: 17% 0 20% 5%;
}

.btn-right {
  z-index: 3;
  width: 20%;
  top: 0;
  right: 0;
  position: absolute;
  cursor: pointer;
  padding: 17% 5% 20% 0;

  img {
    float: right;
  }
}

.btn-up {
  float: left;
  width: 51%;
  z-index: 3;
  top: 0;
  left: 20%;
  position: absolute;
  cursor: pointer;
  padding: 5% 2% 15% 2%;
}

.trans-0 {
  transform: translateX(-0.25%)
}
.trans-30 {
  transform: translateX(-30.25%)
}
.trans-40 {
  transform: translateX(-40.25%)
}
.trans-60 {
  transform: translateX(-60.25%)
}
.bg-1 {
  background: url('../assets/images/position-1.jpg') no-repeat center center;
}

.bg-2 {
  background: url('../assets/images/position-2.jpg') no-repeat center center;
}

.bg-3 {
  background: url('../assets/images/position-3.jpg') no-repeat center center;
}

.bg-4 {
  background: url('../assets/images/position-4.jpg') no-repeat center center;
}

.bg-5 {
  background: url('../assets/images/position-5.jpg') no-repeat center center;
}

.bg-6 {
  background: url('../assets/images/position-6.jpg') no-repeat center center;
}

.bg-7 {
  background: url('../assets/images/position-7.jpg') no-repeat center center;
}

.bg-8 {
  background: url('../assets/images/position-8.jpg') no-repeat center center;
}

.bg-9 {
  background: url('../assets/images/position-9.jpg') no-repeat center center;
}

.bg-10 {
  background: url('../assets/images/position-10.jpg') no-repeat center center;
}
</style>