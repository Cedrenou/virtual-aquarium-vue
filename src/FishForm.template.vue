<template>
  <div class="flex flex-col w-1/6 h-full">
    <form class="flex flex-col mx-4 mt-8" @submit.prevent="$emit('addFish')">
      <h1 class="text-xl font-bold">Fish Type</h1>
      <div  v-for="(fish, index) in fishImages">
        <label :for="fish">
          <img class="w-36" :class="formModel.fishImage === fish ? 'border-4 border-blue-400 rounded-lg p-4' : ''" :src="fish" alt="fish" :key="index">
        </label>
        <input required type="radio" :id="fish" :value="fish" v-model="formModel.fishImage" class="hidden" name="fishImages">
      </div>

      <label class="text-xl font-bold mt-8">Name</label>
      <input type="text"
             required
             v-model="formModel.fishName"
             v-focus
             class="text-black text-3xl px-2 py-4 rounded">
      <button type="submit" class="px-8 py-4 bg-red-500 rounded mt-4 text-3xl">Add fish</button>
    </form>
  </div>

</template>

<script setup>
import { ref } from "vue";
import goldfish from '../public/goldfish.png'
import guppie from '../public/guppie.png'
import tropical from '../public/tropical-fish.png'
import tuna from '../public/tuna.png'
import goldenPurpleFish from '../public/golden-purple-fish.png'

const vFocus = {
  mounted: (el) => el.focus()
}
const fishImages = [goldfish, guppie, tropical, goldenPurpleFish, tuna]

defineProps(['fishInTheAquarium', 'formModel'])
defineEmits(['addFish'])
</script>

<style scoped></style>
