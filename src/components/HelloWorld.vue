<script>

import axios from 'axios';

export default {
  data() {
    return {
      inforooms: null,
    };
  },
  mounted() {
    this.fetchBitcoinPrice();
  },
  methods: {
    async fetchBitcoinPrice() {
      try {
        const response = await axios.get('https://www.supersaas.com/api/range/684392.json?today=true&api_key=8mbnIvecVkw7pgPOPmiKdA');
        this.inforooms = response.data.bookings;

      } catch (error) {
        console.error('Error fetching Bitcoin price:', error);
      }
    },
  },
};
</script>


<template>
  <div class="row">
  <h1>Localisez ma salle/bureau : </h1>
  </div>
 
  <div>
    <div class="ag-format-container">
      <div class="ag-courses_box">
    <div class="card" v-for="inforooms in inforooms">
      <p class="roomP">Groupe : {{ inforooms.description }} </p>
    <p class="roomP">Salle : {{ inforooms.res_name }}</p>
    <p>Avec : {{ inforooms.full_name }}</p>
  </div>
</div>
    </div>

  </div>
</template>
<style>
h1 {
  color: #003482;
  font-weight: bold;
  font-size: 40px;
  font-family: Arial, Helvetica, sans-serif;
  margin-top: 0px;
}
p{
  font-weight: 800;
}
.logo{
  width: 150px;
}
.roomP {
  color: #ED7412;
  font-weight: 900;
  font-size: 20px;
}
.card {
  width: 350px;
  height: auto;
  color: #003482;
  border: 7px solid;
  padding: 20px;
  margin: 20px;
  background-color: #D9FDFD;
}
.ag-format-container {
  width: 1390px;
  margin: 0 auto;
}
.ag-courses_box {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: start;
  -ms-flex-align: start;
  align-items: flex-start;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;

  padding: 50px 0;
}

</style>