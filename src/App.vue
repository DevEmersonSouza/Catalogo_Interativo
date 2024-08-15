<template>
  <div id="app">
    <h1>Catálogo Interativo - Meu Traje Nerd</h1>
    <TshirtSelector @updateSelection="updateSelection" />
    <TshirtPreview :selection="selection" />
  </div>
</template>

<script>
import TshirtSelector from './components/TshirtSelector.vue';
import TshirtPreview from './components/TshirtPreview.vue';

export default {
  name: 'App',
  components: {
    TshirtSelector,
    TshirtPreview
  },
  data() {
    return {
      selection: {
        type: 'normal',
        color: 'white', // Cor padrão deve corresponder a uma imagem
        design: null
      }
    };
  },
  methods: {
    updateSelection(selection) {
      this.selection = selection;
    }
  }
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 50px;
}
</style>
