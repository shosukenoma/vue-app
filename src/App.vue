<script setup>
import { ref } from 'vue'

let id = 0
const newActivity = ref('')
const activites = ref([
  { id: id++, activityName: 'Go on an onsen trip', country: 'Japan' },
  { id: id++, activityName: 'Visit the Grand Canyon', country: 'United States' },
  { id: id++, activityName: 'Go to a tacos party', country: 'Mexico' }
])
</script>

<template>
  <form @submit.prevent="addActivity">
    <select name="" id="">
      <option default value="default">Select Country</option>
      <option value="japan">Japan</option>
      <option value="us">United States</option>
      <option value="mexico">Mexico</option>
    </select>
    <input v-model="newActivity" type="text" />
    <button>Add Activity</button>
  </form>
  <ul>
    <li v-for="act in activites" key="act.id">
      <p>{{ act.activityName }}</p>
      <button @click="removeActivity(act)">X</button>
    </li>
  </ul>
</template>

<style scoped>
header {
  line-height: 1.5;
}
</style>
