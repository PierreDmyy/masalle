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
        'Salle A': '#ffcccc', // Exemple de couleur pour Salle A
        'Salle B': '#ccffcc', // Exemple de couleur pour Salle B
        'Salle Cordelier (Vert pâle)': '#8fffbf', // Exemple de couleur pour Salle C
        'Salle Chatelaine (bleue)': '#3240a8' // Exemple de couleur pour Salle Chatelaine (bleue)
      };
      return colorMap[res_name] || '#D9FDFD'; // Couleur par défaut si aucun mapping trouvé
    }
  },
};
</script>


<template>
  <div>
    <!-- Body -->
    <main>
      <div class="grid-container">
        <div class="card" v-for="room in inforooms" :key="room.id" :style="{ backgroundColor: getCardBackgroundColor(room.res_name) }">
          <p class="roomP">{{ room.description }} </p>
          <p class="roomP">{{ room.res_name }}</p>
          <p>Avec : {{ room.full_name }}</p>
        </div>
      </div>
    </main>
  </div>
</template>

<style>
.grid-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr); /* 4 cartes par ligne */
  grid-gap: 20px; /* Espacement entre les cartes */
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
  color: #003482;
  font-weight: bold;
  font-size: 40px;
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
