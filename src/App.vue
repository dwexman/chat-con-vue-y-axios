<template>
  <div class="chat-container">
    <!-- Persona 1 (izquierda) -->
    <div class="person-container" v-if="person1">
      <img :src="person1.picture.thumbnail" alt="Foto de Persona 1" class="person-img" />
      <h3>{{ person1.name.first }} {{ person1.name.last }}</h3>
      <input v-model="messagePerson1" placeholder="Escribe un mensaje" />
      <button @click="sendMessage(person1, messagePerson1, '#FFCCCC')">Enviar</button>
    </div>

    <!-- Chat (centro) -->
    <div class="chat-box">
      <Chat :messages="messages" />
    </div>

    <!-- Persona 2 (derecha) -->
    <div class="person-container" v-if="person2">
      <img :src="person2.picture.thumbnail" alt="Foto de Persona 2" class="person-img" />
      <h3>{{ person2.name.first }} {{ person2.name.last }}</h3>
      <input v-model="messagePerson2" placeholder="Escribe un mensaje" />
      <button @click="sendMessage(person2, messagePerson2, '#CCCCFF')">Enviar</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Chat from './components/Chat.vue';

export default {
  data() {
    return {
      person1: null,
      person2: null,
      messagePerson1: '',
      messagePerson2: '',
      messages: []
    };
  },
  components: {
    Chat
  },
  methods: {
    async fetchUsers() {
      try {
        const response1 = await axios.get('https://randomuser.me/api/');
        const response2 = await axios.get('https://randomuser.me/api/');
        this.person1 = response1.data.results[0];
        this.person2 = response2.data.results[0];
      } catch (error) {
        console.error('Error fetching users:', error);
      }
    },
    sendMessage(person, content, color) {
      if (content.trim()) {
        this.messages.push({ name: `${person.name.first} ${person.name.last}`, content, color });
        this.messagePerson1 = '';
        this.messagePerson2 = '';
      }
    }
  },
  mounted() {
    this.fetchUsers();
  }
};
</script>

<style scoped>
.chat-container {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 20px;
  width: 800px;
  height: 600px;
  gap: 20px;
}

.person-container {
  width: 25%;
  text-align: center;
  padding: 10px;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 10px;
}

.person-img {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 10px;
}

.chat-box {
  width: 50%;
  border: 1px solid #ddd;
  padding: 10px;
  height: 100%;
  overflow-y: auto;
  background-color: #f5f5f5;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

button {
  margin-top: 10px;
  padding: 8px 12px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

input {
  width: 80%;
  padding: 8px;
  margin-top: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}
</style>
