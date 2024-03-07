<template>
  <div id="app">
    <v-app>
      <v-main>
        <div class="container">
        <main-dashboard />
        <city-selector />
        </div>
      </v-main>
    </v-app>
  </div>
</template>

<script>
  import MainDashboard from './components/MainDashboard.vue'
  import CitySelector from './components/CitySelector.vue'

  export default {
    components: {
      MainDashboard,
      CitySelector
    }
  }
</script>

<style>
  .container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }

  .company-info {
    border: 1px solid #ccc;
    padding: 20px;
  }

  .status {
    margin-top: 20px;
  }

  .city-selector {
    border: 1px solid #ccc;
    padding: 20px;
  }
</style>