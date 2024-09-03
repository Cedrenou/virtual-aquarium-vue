<template>
  <div class="h-full flex flex-row">
    <FishForm @addFish="addFish" :fishInTheAquarium="fishInTheAquarium" :formModel="formModel"/>
    <Aquarium :fishInTheAquarium="fishInTheAquarium"/>
  </div>
</template>
<script setup>
import FishForm from './FishForm.template.vue'
import Aquarium from './Aquarium.template.vue'
import { ref } from "vue";

const fishInTheAquarium = ref([])
const formModel = ref({
  id: null,
  fishName: '',
  fishImage: '',
  life: null
})

let fishIdCounter = 0

const addFish = () => {
  const newFish = {
    ...formModel.value,
    life: 100,
    id: ++fishIdCounter
  }
  fishInTheAquarium.value = [...fishInTheAquarium.value, newFish]
  clearForm()
}

const clearForm = () => {
  formModel.value = {
    id: null,
    fishName: '',
    fishImage: '',
    life: null
  }
}
</script>
