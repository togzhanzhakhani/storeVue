<template>
    <div class="city-selector">
      <p>Мой город:
      <span><v-select
        v-model="selectedCityCode"
        :items="cities"
        item-value="code"
        item-text="name"
        @change="handleChange"
        placeholder="Выберите город"
      /></span>
      </p>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        data() {
            return {
                cities: [],
                selectedCityCode: '',
                selectedCityName: ''
            }
        },
        created() {
            this.fetchCityData();
            this.loadSelectedCity();
        },
        methods: {
            async fetchCityData() {
                try {
                    const response = await axios.get('https://bitbucket.org/ilakhmotkin/front-end-assesment-ru/raw/7bc28b7ede222e25fe44fec52ad1e74a03168501/cities-response.json');
                    this.cities = response.data.cities;
                } catch (error) {
                    console.error('Error fetching city data:', error);
                }
            },
            handleChange() {
                localStorage.setItem('selectedCityCode', this.selectedCityCode);
                this.loadSelectedCityName();
            },
            loadSelectedCity() {
                const savedCityCode = localStorage.getItem('selectedCityCode');
                if (savedCityCode) {
                    this.selectedCityCode = savedCityCode;
                }
                this.loadSelectedCityName();
            },
            loadSelectedCityName() {
                const city = this.cities.find(city => city.code === this.selectedCityCode);
                if (city) {
                    this.selectedCityName = city.name;
                } else {
                    this.selectedCityName = '';
                }
            }

        }
    }
</script>
