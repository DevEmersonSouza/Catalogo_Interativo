<template>
  <div class="tshirt-selector">
    <h2>Personalize Sua Camiseta!</h2>

    <div>
      <label for="type">Tipo:</label>
      <select v-model="localSelection.type" @change="handleTypeChange">
        <option value="normal">Normal</option>
        <option value="oversized">Oversized</option>
      </select>
    </div>

    <div>
      <label for="color">Cores disponíveis:</label>
      <div class="color-options">
        <div v-for="color in availableColors" :key="color.name" 
             @click="selectColor(color.name)" 
             :class="{ selected: localSelection.color === color.name }" 
             class="color-button"
             :style="{ backgroundColor: color.hex }">
          {{ color.label }}
        </div>
      </div>
    </div>

    <div>
      <label for="design">Estampa:</label>
      <div class="design-options">
        <img v-for="design in designs" :key="design.name" :src="design.image" 
             :alt="design.name" @click="selectDesign(design.name)" 
             :class="{ selected: localSelection.design === design.name }" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TshirtSelector',
  data() {
    return {
      localSelection: {
        type: 'normal',
        color: 'white',
        design: null
      },
      normalColors: [
        { name: 'white', hex: '#FFFFFF', label: 'White' },
        { name: 'royal-blue', hex: '#4169E1', label: 'Royal Blue' },
        { name: 'black', hex: '#000000', label: 'Black' },
        { name: 'baby-blue', hex: '#89CFF0', label: 'Baby Blue' },
        { name: 'pink', hex: '#ff0066', label: 'Pink' },
        { name: 'green', hex: '#008000', label: 'Green' },
        { name: 'grey', hex: '#808080', label: 'Grey' },
        { name: 'red', hex: '#FF0000', label: 'Red' },
        { name: 'off-white', hex: '#FDF5E6', label: 'Off White' },
        { name: 'marine-blue', hex: '#3C3B6E', label: 'Marine Blue' },
        { name: 'brown', hex: '#8B4513', label: 'Brown' },
        { name: 'mostard', hex: '#FFDB58', label: 'Mustard' },
        { name: 'orange', hex: '#FFA500', label: 'Orange' },
        { name: 'purple', hex: '#800080', label: 'Purple' },
        { name: 'red-wine', hex: '#722F37', label: 'Red Wine' },
        { name: 'bege', hex: '#ffe6b5', label: 'Bege' },
        { name: 'yellow', hex: '#FFFF00', label: 'Yellow' },
        { name: 'petrol-blue', hex: '#095c86', label: 'Petrol Blue' },
        { name: 'baby-green', hex: '#ccffcc', label: 'Baby Green' },
      ],
      oversizedColors: [
        { name: 'off-whiteOversized', hex: '#FDF5E6', label: 'Off White' },
        { name: 'redOversized', hex: '#FF0000', label: 'Red' },
        { name: 'baby-pinkOversized', hex: '#ffcccc', label: 'Baby Pink' },
        { name: 'begeOversized', hex: '#ffe6b5', label: 'Bege' },
        { name: 'blackOversized', hex: '#000000', label: 'Black' },
        { name: 'brownOversized', hex: '#8B4513', label: 'Brown' },
        { name: 'green-gabOversized', hex: '#848420', label: 'Green Gab' },
        { name: 'marine-blueOversized', hex: '#3C3B6E', label: 'Marine Blue' },
        { name: 'purpleOversized', hex: '#800080', label: 'Purple' },
      ],
      designs: [
        { name: 'design1', image: require('../assets/design1.png') },
        { name: 'design2', image: require('../assets/design2.png') }
      ]
    };
  },
  computed: {
    availableColors() {
      return this.localSelection.type === 'normal' ? this.normalColors : this.oversizedColors;
    }
  },
  methods: {
    updateParent() {
      this.$emit('updateSelection', this.localSelection);
    },
    selectColor(color) {
      this.localSelection.color = color;
      this.updateParent();
    },
    selectDesign(design) {
      this.localSelection.design = design;
      this.updateParent();
    },
    handleTypeChange() {
      this.localSelection.color = this.availableColors[0].name;
      this.updateParent();
    }
  }
};
</script>

<style scoped>
.tshirt-selector {
  margin: 20px;
}
label {
  margin-right: 10px;
}
.color-options {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.color-button {
  width: 50px;
  height: 50px;
  margin: 5px;
  cursor: pointer;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  text-shadow: 1px 1px 2px #5C6594, 0 0 1em #FFFBD6, 0 0 0.2em #DE5A74;
  font-size: 10px;
  text-align: center;
  border: 2px solid transparent;
}
.color-button.selected {
  border: 2px solid #000;
}
.design-options img {
  width: 50px;
  margin: 5px;
  cursor: pointer;
  border: 2px solid transparent;
}
.design-options img.selected {
  border: 2px solid #000;
}
</style>
