<template>
    <div class="contenedor-chat">
      <div 
        v-for="(mensaje, indice) in mensajes" 
        :key="indice" 
        class="mensaje-chat" 
        :class="{'izquierda': mensaje.alineacion === 'izquierda', 'derecha': mensaje.alineacion === 'derecha'}"
        :style="{ backgroundColor: mensaje.color }"
      >
        <strong>{{ mensaje.usuario }}:</strong> {{ mensaje.texto }}
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      mensajes: Array,
    },
  };
  </script>
  
  <style scoped>
  .contenedor-chat {
    width: 40%;
    border: 1px solid #ccc;
    padding: 10px;
    height: 300px;
    overflow-y: auto;
    background-color: #f9f9f9;
  }
  
  .mensaje-chat {
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 5px;
    color: #000;
    max-width: 70%;
  }
  
  .izquierda {
    text-align: left;
    float: left;
    clear: both;
  }
  
  .derecha {
    text-align: right;
    float: right;
    clear: both;
  }
  </style>
  