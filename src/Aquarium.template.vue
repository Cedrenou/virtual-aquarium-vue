<template>
  <div class="w-full background-aquarium" ref="aquarium">
    <Fish v-for="fish in fishInTheAquarium"
          ref="fish"
          :fishImage="fish.fishImage"
          :fishName="fish.fishName"
          :life="fish.life"
          :fishId="fish.id"
          :aquariumHeight="aquariumHeight"
          :aquariumWidth="aquariumWidth"
          :key="fish.id"/>
  </div>
</template>

<script setup>
import Fish from './Fish.template.vue'
import { computed, onMounted, ref } from "vue";

defineProps(['fishInTheAquarium'])
const aquarium = ref()

const aquariumWidth = computed(()=> aquarium.value.offsetWidth)
const aquariumHeight = computed(()=> aquarium.value.offsetHeight)

function fishMove(fishId) {

  console.log('FISH move !')
  console.log(aquariumWidth.value)
  console.log(aquariumHeight.value)
}

onMounted(() => fishMove())

</script>

<style scoped>
.background-aquarium {
  background-image: url("../public/bg.jpg");
}
</style>
