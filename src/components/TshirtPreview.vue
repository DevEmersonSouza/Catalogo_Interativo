<template>
    <div class="tshirt-preview">
      <h2>Veja Como sua nova Camiseta vai ficar:</h2>
      <div class="tshirt">
        <img :src="tshirtImageUrl" class="tshirt-image" />
        <img v-if="selection.design" :src="designImageUrl" class="design" />
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TshirtPreview',
    props: ['selection'],
    computed: {
      tshirtImageUrl() {
        return require(`../assets/${this.selection.color}-tshirt.png`);
      },
      designImageUrl() {
        return require(`../assets/${this.selection.design}.png`);
      }
    }
  };
  </script>
  
  <style scoped>
  .tshirt {
    position: relative;
    margin: 20px auto;
    width: 200px;
  }
  .tshirt-image {
    width: 100%;
    height: auto;
  }
  .design {
    position: absolute;
    top: 28%; /* Ajuste para alinhar a estampa */
    left: 23%; /* Ajuste para alinhar a estampa */
    width: 50%; /* Ajuste o tamanho da estampa */
    height: auto;
    z-index: 10;
  }
  </style>  