<script setup>
import { ref, computed } from 'vue'

let id = 0
const newActivity = ref('')
const country = ref('')
const filterCountry = ref('')

const activities = ref([
  { id: id++, activityName: 'Go on an onsen trip', country: 'Japan' },
  { id: id++, activityName: 'Spend time with family and friends', country: 'Japan' },
  { id: id++, activityName: 'Visit the Grand Canyon', country: 'United States' },
  { id: id++, activityName: 'Eat lots of delicious tacos', country: 'Mexico' },
  { id: id++, activityName: 'Homestay to improve my Spanish', country: 'Mexico' }
])

const addActivity = function () {
  activities.value.push({
    id: id++,
    activityName: newActivity.value,
    country: country.value
  })

  newActivity.value = ''
  country.value = ''
}

const removeActivity = function (act) {
  activities.value = activities.value.filter((a) => a != act)
}

const filteredActivites = computed(() => {
  return filterCountry.value
    ? activities.value.filter((act) => act.country == filterCountry.value)
    : activities.value
})
</script>

<template>
  <body>
    <h1>Welcome to Sho's Bucket List!</h1>
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
      <li class="item-list" v-for="act in filteredActivites" :key="act.id">
        <p>{{ act.activityName }} ({{ act.country }})</p>
        <button class="delete-button" @click="removeActivity(act)">X</button>
      </li>
    </ul>
    <div>
      <span>Filter by Country: </span>
      <select v-model="filterCountry" id="filterCountry" required>
        <option value="" selected>Show all</option>
        <option value="Japan">Japan</option>
        <option value="United States">United States</option>
        <option value="Mexico">Mexico</option>
      </select>
    </div>
  </body>
</template>

<style scoped>
body {
  margin: 40px;
}

ul {
  list-style: none;
}

.item-list {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.delete-button {
  height: 1.5rem;
}
</style>
