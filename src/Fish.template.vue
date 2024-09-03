<template>
  <div class="w-36" ref="fish">
    <img :src="fishImage" alt="fish" :style="{transform :`scaleX(${directionX})`}">
    <div class="bg-gray-500 opacity-40 rounded-t">
      <h1 class="text-center">{{ fishName }} - {{fishId}}</h1>
      <div class="border-4 border-red-600" :style="{width: life + '%'}"></div>
    </div>
  </div>
</template>
<script setup>
import { computed, onMounted, onUnmounted, ref } from "vue";

const props = defineProps(['fishImage', 'fishName', 'life', 'fishId', 'aquariumHeight','aquariumWidth'])
const emit = defineEmits(['fishMove'])

const fish = ref()
const positionX = ref(0)
const positionY = ref(0)
const directionX = ref(Math.random() < 0.5 ? -1 : 1) // 1 pour droit -1 pour gauche
const directionY = ref(Math.random() < 0.5 ? -1 : 1); // 1 pour droit -1 pour gauche
const speedX = ref(1 + Math.random() * 2)
const speedY = ref(0.5 + Math.random())
const fishWidth = computed(()=> fish.value.offsetWidth)
const fishHeight = computed(()=> fish.value.offsetHeight)

let animationFrameId = null

const moveFish = () => {
  if(directionX.value === 1) {
    if(positionX.value + fishWidth.value >= props.aquariumWidth) {
      directionX.value = -1 // Change direction
    } else {
      positionX.value += speedX.value
    }
  } else {
    if(positionX.value <= 0) {
      directionX.value =1
    } else {
      positionX.value -= speedX.value
    }
  }

  if(directionY.value === 1) {
    if(positionY.value + fishHeight.value >= props.aquariumHeight) {
      directionY.value = -1 // Change direction
    } else {
      positionY.value += speedY.value
    }
  } else {
    if(positionY.value <= 0) {
      directionY.value =1
    } else {
      positionY.value -= speedY.value
    }
  }

  if (fish.value) {
    fish.value.style.transform = `translate(${positionX.value}px, ${positionY.value}px)`
  }

  animationFrameId = requestAnimationFrame(moveFish)
}


onMounted(() => {
  if (fish.value) {
    fish.value.style.position = 'absolute'
    fish.value.style.transform =  `translate(${positionX.value}px, ${positionY.value}px)`
  }
  animationFrameId = requestAnimationFrame(moveFish)
})

onUnmounted(() => {
  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId);
  }
});
</script>
<style scoped></style>
