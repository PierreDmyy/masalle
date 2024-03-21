<template>
  <div>
    <!-- Affichage des salles du matin si l'heure est entre 8h30 et 12h00 -->
    <div v-if="isMorning">
      <div class="grid-container">
        <div class="card" v-for="room in morningRooms" :key="room.id" :style="{ backgroundColor: getCardBackgroundColor(room.res_name), color: getTextColor(room.res_name) }">
          <p class="roomP">{{ room.description }} </p>
          <p class="roomP">{{ room.res_name }}</p>
          <p class="person">Avec : {{ room.full_name }}</p>
          <p class="time">De :  {{ formatDateTime(room.start) }} - À : {{ formatDateTime(room.finish) }}</p> 
        </div>
      </div>
    </div>

    <!-- Affichage des salles de l'après-midi si l'heure est entre 13h25 et 16h30 -->
    <div v-else-if="isAfternoon">
      <div class="grid-container">
        <div class="card" v-for="room in afternoonRooms" :key="room.id" :style="{ backgroundColor: getCardBackgroundColor(room.res_name), color: getTextColor(room.res_name) }">
          <p class="roomP">{{ room.description }} </p>
          <p class="roomP">{{ room.res_name }}</p>
          <p class="person">Avec : {{ room.full_name }}</p>
          <p class="time">De :  {{ formatDateTime(room.start) }} - À : {{ formatDateTime(room.finish) }}</p> 
        </div>
      </div>
    </div>

    <!-- Message par défaut si aucune salle à afficher -->
   <div class="no-rooms" v-else>
      <p class="message">Aucune salle à afficher pour le moment.</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { format } from 'date-fns';

export default {
  data() {
    return {
      morningRooms: [],
      afternoonRooms: [],
    };
  },
  computed: {
    // Vérifie si l'heure actuelle est entre 8h30 et 12h00
    isMorning() {
      const now = new Date();
      const morningStart = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 8, 15, 0);
      const morningEnd = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 12, 0, 0);
      return now >= morningStart && now < morningEnd;
    },
    // Vérifie si l'heure actuelle est entre 13h25 et 16h30
    isAfternoon() {
      const now = new Date();
      const afternoonStart = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 13, 15, 0);
      const afternoonEnd = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 16, 30, 0);
      return now >= afternoonStart && now < afternoonEnd;
    },
  },
  mounted() {
    this.fetchRoomData();
  },
  methods: {
    async fetchRoomData() {
      try {
        const response = await axios.get('https://www.supersaas.com/api/range/684392.json?limit=30&today=true&api_key=8mbnIvecVkw7pgPOPmiKdA');
        const inforooms = response.data.bookings;

        // Filtrer les salles du matin (de 8h30 à 12h)
        const morningStart = new Date();
        morningStart.setHours(8, 30, 0);
        const morningEnd = new Date();
        morningEnd.setHours(12, 0, 0);
        this.morningRooms = inforooms.filter(room => {
          const roomStart = new Date(room.start);
          return roomStart >= morningStart && roomStart < morningEnd;
        });

        // Filtrer les salles de l'après-midi (de 13h00 à 16h29)
        const afternoonStart = new Date();
        afternoonStart.setHours(13, 0, 0);
        const afternoonEnd = new Date();
        afternoonEnd.setHours(16, 30, 0);
        this.afternoonRooms = inforooms.filter(room => {
          const roomStart = new Date(room.start);
          return roomStart >= afternoonStart && roomStart < afternoonEnd;
        });
      } catch (error) {
        console.error('Error fetching room data:', error);
      }
    },
    getCardBackgroundColor(res_name) {
      const colorMap = {
        'Salle Parvis (verte)': '#008000', 
        'Salle Remparts (Jaune)': 'rgba(250, 241, 29, 0.9)', 
        'Salle Cordelier (Vert pâle)': '#99cc99', 
        'Salle Chatelaine (bleue)': '#3240a8',
        'Salle Cloître (Orange)' : '#ff9f31'
      };
      return colorMap[res_name] || '#D9FDFD';
    },
    getTextColor(res_name) {
      const colorMap = {
        'Salle Parvis (verte)': '#ffff', 
        'Salle Remparts (Jaune)': '#003681', 
        'Salle Cordelier (Vert pâle)': '#003681', 
        'Salle Chatelaine (bleue)': '#ffff' 
      };
      return colorMap[res_name] || '#003681';
    },
    formatDateTime(dateTimeString) {
      const date = new Date(dateTimeString);
      const formattedTime = `${padWithZero(date.getHours())}:${padWithZero(date.getMinutes())}`;
      return formattedTime;
    },
  },
};

function padWithZero(num) {
  return num.toString().padStart(2, '0');
}
</script>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr); /* 4 cartes par ligne */
  grid-gap: 15px; /* Espacement entre les cartes */
  justify-content: center;
  flex-wrap: wrap;
}

.card {
  width: 270px;
  height: auto;
  color: #003482;
  border: solid 5px #250f0f36;
  box-shadow: rgba(17, 17, 26, 0.1) 0px 0px 16px;
  padding: 5px;
}

.roomP {
  font-family: 'Poppins', sans-serif;
  align-items: center;
  text-align: center;
  font-weight: 900;
  font-size: 15px;
}

.person {
  align-items: center;
  text-align: center;
  font-weight: 500;
  font-size: 15px;
}

.time {
  align-items: center;
  text-align: center;
  font-weight: 700;
  font-size: 15px;
}

.no-rooms{
  margin: 0; /* Supprimer les marges par défaut pour centrer correctement */
}
.message {
  display: flex;
  justify-content: center; /* Centre horizontalement */
  align-items: center; /* Centre verticalement */
  height: 100%; /* Hauteur de la div pour centrer verticalement */
  text-align: center; /* Centre horizontalement le texte */
  color: #003482;
  font-weight: bolder;
  font-family: Arial, Helvetica, sans-serif;
}

.titleRoom {
  color: #003482;
  margin-bottom: 40px;
  font-family: 'Poppins', sans-serif;
  font-size: 25px;

}
</style>
