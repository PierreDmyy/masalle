<script>
import axios from 'axios';

export default {
  data() {
    return {
      inforooms: null,
    };
  },
  mounted() {
    this.fetchRoomData();
  },
  methods: {
    async fetchRoomData() {
      try {
        const response = await axios.get('https://www.supersaas.com/api/range/684392.json?today=true&api_key=8mbnIvecVkw7pgPOPmiKdA');
        this.inforooms = response.data.bookings;
      } catch (error) {
        console.error('Error fetching room data:', error);
      }
    },
    getCardBackgroundColor(res_name) {
      // Mapping des noms de salle aux couleurs correspondantes
      const colorMap = {
        'Salle A': '#ffcccc', 
        'Salle Remparts (Jaune)': 'rgba(250, 241, 29, 0.9)', 
        'Salle Cordelier (Vert pâle)': '#99cc99', 
        'Salle Chatelaine (bleue)': '#3240a8' 
      };
      return colorMap[res_name] || '#D9FDFD'; // Couleur par défaut si aucun mapping trouvé
    },
    getTextColor(res_name) {
      // Mapping des noms de salle aux couleurs correspondantes
      const colorMap = {
        'Salle A': '#ffcccc', 
        'Salle Remparts (Jaune)': '#003681', 
        'Salle Cordelier (Vert pâle)': '#003681', 
        'Salle Chatelaine (bleue)': '#ffff' 
      };
      return colorMap[res_name] || '#003681'; // Couleur par défaut si aucun mapping trouvé
    }
  },
};
</script>


<template>
  <div>
    <!-- Body -->
    <main>
      <div class="grid-container">
        <div class="card" v-for="room in inforooms" :key="room.id" :style="{ backgroundColor: getCardBackgroundColor(room.res_name), color: getTextColor(room.res_name) }">
          <p class="roomP">{{ room.description }} </p>
          <p class="roomP">{{ room.res_name }}</p>
          <p class="Person">Avec : {{ room.full_name }}</p>
        </div>
      </div>
    </main>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@700&display=swap');

main {
  display: flex;
  justify-content: center;
}
.grid-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr); /* 4 cartes par ligne */
  grid-gap: 15px; /* Espacement entre les cartes */
  margin-top: -30px;
  justify-content: center;
  flex-wrap: wrap;
}

/* CSS pour le menu */
nav {
  background-color: #333;
  padding: 10px 0;
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  text-align: center;
}

li {
  display: inline;
  margin: 0 10px;
}

a {
  color: white;
  text-decoration: none;
}

/* CSS pour le corps de l'application */
main {
  padding: 0;
}


h1 {
  font-family: 'Poppins', sans-serif;
  color: #003482;
  font-weight: bold;
  font-size: 25px;
  font-family: Arial, Helvetica, sans-serif;
  margin-top: 0px;
}

p {
  font-weight: 800;
}

.logo {
  width: 150px;
}

.roomP {
  font-family: 'Poppins', sans-serif;
  align-items: center;
  text-align: center;
  font-weight: 900;
  font-size: 15px;
}
.Person{
  align-items: center;
  text-align: center;
  font-weight: 500;
  font-size: 15px;
}

.card {
  width: 270px;
  height: auto;
  color: #003482;
  border: solid 5px #250f0f36;
  box-shadow: rgba(17, 17, 26, 0.1) 0px 0px 16px;

 padding: 20px;
  margin: -3px;
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
