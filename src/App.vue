<script setup>
  import { ref, onMounted } from "vue"
  import axios from "axios"

  const peoples = ref([])
  const vehicles = ref([])

  const fetchData = () => {
    fetch("https://swapi.dev/api/vehicles/")
      .then((res) => res.json())
      .then((data) => {
        console.log(data)
        vehicles.value = data.results
      })
      .catch((err) => {
        console.log(err)
      })
  }

  onMounted(() => {
    axios
      .get("https://swapi.dev/api/people/")
      .then((data) => {
        console.log(data.data.results)
        peoples.value = data.data.results
      })
      .catch((err) => {
        console.log(err)
      })

    fetchData()
  })
</script>

<template>
  <div class="peoples">
    <h2>Peoples</h2>
    <div class="peoples__items">
      <div v-for="people in peoples" class="people">
        <p class="name"><span>Name:</span> {{ people.name }}</p>
        <p class="eye-color"><span>Eye color:</span> {{ people.eye_color }}</p>
        <p class="gender"><span>Gender:</span> {{ people.gender }}</p>
        <p class="height"><span>Height:</span> {{ people.height }}</p>
      </div>
    </div>
  </div>

  <div class="vehicles">
    <h2>Vehicles</h2>
    <div class="vehicles__items">
      <div v-for="vehicle in vehicles" class="vehicle">
        <p><span>Name:</span> {{ vehicle.name }}</p>
        <p><span>Model:</span> {{ vehicle.model }}</p>
        <p><span>Manufacturer:</span> {{ vehicle.manufacturer }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
