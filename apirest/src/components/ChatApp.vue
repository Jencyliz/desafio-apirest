<template>
    <div class="app-chat">
      <div class="seccion-usuarios" v-if="usuarios.length === 2">
        <div class="usuario">
          <img :src="usuarios[0].picture.large" alt="Foto del usuario" class="foto-usuario"/>
          <h4>{{ usuarios[0].name.first }} {{ usuarios[0].name.last }}</h4>
          <textarea v-model="mensajes[0].texto" placeholder="Escribe un mensaje"></textarea>
          <button @click="enviarMensaje(0)">Enviar</button>
        </div>

        <ChatMensajes :mensajes="chatMensajes" />

        <div class="usuario">
          <img :src="usuarios[1].picture.large" alt="Foto del usuario" class="foto-usuario"/>
          <h4>{{ usuarios[1].name.first }} {{ usuarios[1].name.last }}</h4>
          <textarea v-model="mensajes[1].texto" placeholder="Escribe un mensaje"></textarea>
          <button @click="enviarMensaje(1)">Enviar</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import ChatMensajes from './ChatMensajes.vue';
  
  export default {
    components: {
      ChatMensajes,
    },
    data() {
      return {
        usuarios: [],
        mensajes: [
          { texto: '', color: '#add8e6' }, 
          { texto: '', color: '#f0e68c' }, 
        ],
        chatMensajes: [],
      };
    },
    methods: {
      async obtenerUsuarios() {
        try {
          const res1 = await axios.get('https://randomuser.me/api/');
          const res2 = await axios.get('https://randomuser.me/api/');
          this.usuarios = [res1.data.results[0], res2.data.results[0]];
        } catch (error) {
          console.error("Error al obtener usuarios:", error);
        }
      },
      enviarMensaje(indice) {
        if (this.mensajes[indice].texto) {
          const mensaje = {
            usuario: this.usuarios[indice].name.first,
            texto: this.mensajes[indice].texto,
            color: this.mensajes[indice].color,
            alineacion: indice === 0 ? 'izquierda' : 'derecha',
          };
          this.chatMensajes.push(mensaje);
          this.mensajes[indice].texto = '';
        }
      },
    },
    created() {
      this.obtenerUsuarios();
    },
  };
  </script>
  
  <style scoped>
  .app-chat {
    display: flex;
    justify-content: space-around;
    margin: 20px;
  }
  
  .seccion-usuarios {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 100%;
  }
  
  .usuario {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 30%;
  }
  
  .foto-usuario {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    margin-bottom: 10px;
    margin: 10px;
  }
  
  textarea {
    width: 100%;
    height: 100px;
    margin-top: 10px;
  }
  
  button {
    margin-top: 10px;
  }
  </style>
  