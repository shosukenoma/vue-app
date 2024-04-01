<script setup>
import { ref } from 'vue'

let id = 0
const newActivity = ref('')
const country = ref('')
const filterCountry = ref('')

const activities = ref([
  { id: id++, activityName: 'Go on an onsen trip', country: 'Japan' },
  { id: id++, activityName: 'Visit the Grand Canyon', country: 'United States' },
  { id: id++, activityName: 'Go to a tacos party', country: 'Mexico' }
])

const addActivity = function () {
  activities.value.push({
    id: id++,
    activityName: newActivity.value,
    country: country.value
  })
}

const removeActivity = function (act) {
  activities.value = activities.value.filter((a) => a != act)
}
</script>

<template>
  <form @submit.prevent="addActivity">
    <select v-model="country" id="selectCountry" required>
      <option value="" disabled>Select a country</option>
      <option value="Japan">Japan</option>
      <option value="United States">United States</option>
      <option value="Mexico">Mexico</option>
    </select>
    <input placeholder="New activity" v-model="newActivity" type="text" required />
    <button>Add Activity</button>
  </form>
  <ul>
    <li v-for="act in activities" :key="act.id">
      <p>{{ act.activityName }} ({{ act.country }})</p>
      <button @click="removeActivity(act)">X</button>
    </li>
  </ul>
  <select v-model="filterCountry" @select="applyFilter" id="filterCountry" required>
    <option value="" selected>Show all</option>
    <option value="Japan">Japan</option>
    <option value="United States">United States</option>
    <option value="Mexico">Mexico</option>
  </select>
</template>

<style scoped></style>
