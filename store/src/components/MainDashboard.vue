<template>
        <div class="company-info">
      <h1>{{ companyName }}</h1>
      <div class="status">
        <p>Сегодня: {{ today }}</p>
        <p>Общее количество товаров: {{ totalProducts }}</p>
        <p>Товар в наличии: {{ availableProducts }}</p>
        <p>Товар без наличия: {{ nonAvailableProducts }}</p>
      </div>
    </div>
</template>
  
<script>
    import axios from 'axios';

    export default {
        data() {
            return {
                companyName: '',
                today: '',
                totalProducts: 0,
                availableProducts: 0,
                nonAvailableProducts: 0
            };
        },
        created() {
            this.fetchCompanyData();
        },
        methods: {
            async fetchCompanyData() {
                try {
                    const response = await axios.get('https://bitbucket.org/ilakhmotkin/front-end-assesment-ru/raw/09c0e12a2b5325e71f36c08e7e29dc8eefbdb081/company-response.json');
                    const { name, status } = response.data;
                    this.companyName = name;
                    this.today = new Date(status.today).toLocaleDateString('en-US', { timeZone: 'Asia/Almaty' });
                    this.totalProducts = status.totalProducts;
                    this.availableProducts = status.availableProducts;
                    this.nonAvailableProducts = status.nonAvailableProducts;
                } catch (error) {
                    console.error('Error fetching company data:', error);
                }
            }
        }
    };
</script>
