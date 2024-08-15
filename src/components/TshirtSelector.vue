<template>
  <div class="tshirt-selector">
    <h2>Personalize Sua Camiseta!</h2>

    <div>
      <multiselect
        v-model="localSelection.type"
        :options="['normal', 'oversized']"
        @input="handleTypeChange"
        :reduce="(val) => val"
        :searchable="false"
        :clearable="false"
        placeholder="Selecione um tipo"
      />
    </div>

    <div>
      <label for="color">Cores disponíveis:</label>
      <div class="color-options">
        <div
          v-for="color in availableColors"
          :key="color.name"
          @click="selectColor(color.name)"
          :class="{ selected: localSelection.color === color.name }"
          class="color-button"
          :style="{ backgroundColor: color.hex }"
        >
          {{ color.label }}
        </div>
      </div>
    </div>

    <div>
      <multiselect
        v-model="localSelection.anime"
        :options="animes"
        @input="handleAnimeChange"
        :reduce="(val) => val"
        :searchable="false"
        :clearable="false"
        placeholder="Selecione um anime"
        :max-height="100"
      />
    </div>

    <div class="estampa-row">
      <div>
        <label for="design">Estampa:</label>
        <div class="design-options">
          <img
            v-for="design in filteredDesigns"
            :key="design.name"
            :src="design.image"
            :alt="design.name"
            @click="selectDesign(design.name, 'front')"
            :class="{ selected: localSelection.frontDesign === design.name }"
          />
        </div>
      </div>
      <div v-if="localSelection.doubleSided">
        <label for="designBack">Estampa Verso:</label>
        <div class="design-options">
          <img
            v-for="design in filteredDesigns"
            :key="design.name"
            :src="design.image"
            :alt="design.name"
            @click="selectDesign(design.name, 'back')"
            :class="{ selected: localSelection.backDesign === design.name }"
          />
        </div>
      </div>
    </div>
    <div>
      <input
        type="checkbox"
        v-model="localSelection.doubleSided"
        id="doubleSided"
      />
      <label for="doubleSided">Estampa Frente e Verso</label>
    </div>
  </div>
</template>

<script>
import multiselect from "vue-multiselect";
import "/node_modules/vue-multiselect/dist/vue-multiselect.css";

export default {
  name: "TshirtSelector",
  components: {
    multiselect,
  },
  data() {
    return {
      localSelection: {
        type: "normal",
        color: "white",
        anime: "Hunter X Hunter", // Anime padrão
        frontDesign: null,
        backDesign: null,
        doubleSided: false, // Nova opção para estampa dupla
      },
      normalColors: [
        { name: "white", hex: "#FFFFFF", label: "White" },
        { name: "royal-blue", hex: "#4169E1", label: "Royal Blue" },
        { name: "black", hex: "#000000", label: "Black" },
        { name: "baby-blue", hex: "#89CFF0", label: "Baby Blue" },
        { name: "pink", hex: "#ff0066", label: "Pink" },
        { name: "green", hex: "#008000", label: "Green" },
        { name: "grey", hex: "#808080", label: "Grey" },
        { name: "red", hex: "#FF0000", label: "Red" },
        { name: "off-white", hex: "#FDF5E6", label: "Off White" },
        { name: "marine-blue", hex: "#010042", label: "Marine Blue" },
        { name: "brown", hex: "#8B4513", label: "Brown" },
        { name: "mostard", hex: "#FFDB58", label: "Mustard" },
        { name: "orange", hex: "#FFA500", label: "Orange" },
        { name: "purple", hex: "#800080", label: "Purple" },
        { name: "red-wine", hex: "#722F37", label: "Red Wine" },
        { name: "bege", hex: "#ffe6b5", label: "Bege" },
        { name: "yellow", hex: "#FFFF00", label: "Yellow" },
        { name: "petrol-blue", hex: "#095c86", label: "Petrol Blue" },
        { name: "baby-green", hex: "#ccffcc", label: "Baby Green" },
      ],
      oversizedColors: [
        { name: "off-whiteOversized", hex: "#FDF5E6", label: "Off White" },
        { name: "redOversized", hex: "#FF0000", label: "Red" },
        { name: "baby-pinkOversized", hex: "#ffcccc", label: "Baby Pink" },
        { name: "begeOversized", hex: "#ffe6b5", label: "Bege" },
        { name: "blackOversized", hex: "#000000", label: "Black" },
        { name: "brownOversized", hex: "#8B4513", label: "Brown" },
        { name: "green-gabOversized", hex: "#848420", label: "Green Gab" },
        { name: "marine-blueOversized", hex: "#010042", label: "Marine Blue" },
        { name: "purpleOversized", hex: "#800080", label: "Purple" },
      ],
      animes: [
        "Five Nights at Freddy's",
        "Chainsaw Man",
        "Coraline",
        "Hunter X Hunter",
        "Attack on Titan",
        "Senhor dos Anéis",
        "Black Clover",
        "The Eminence in the Shadows",
        "Friends",
        "Vintage",
        "One Piece",
      ], // Animes disponíveis
      designs: [
        {
          name: "fnaf1",
          image: require("../assets/fnaf1.png"),
          anime: "Five Nights at Freddy's",
        },
        {
          name: "chainsaw1",
          image: require("../assets/chainsaw1.png"),
          anime: "Chainsaw Man",
        },
        {
          name: "coraline1",
          image: require("../assets/coraline1.png"),
          anime: "Coraline",
        },
        {
          name: "coraline2",
          image: require("../assets/coraline2.png"),
          anime: "Coraline",
        },
        {
          name: "hunter1",
          image: require("../assets/hunter1.png"),
          anime: "Hunter X Hunter",
        },
        {
          name: "hunter2",
          image: require("../assets/hunter2.png"),
          anime: "Hunter X Hunter",
        },
        {
          name: "hunter3",
          image: require("../assets/hunter3.png"),
          anime: "Hunter X Hunter",
        },
        {
          name: "hunter4",
          image: require("../assets/hunter4.png"),
          anime: "Hunter X Hunter",
        },
        {
          name: "aot1",
          image: require("../assets/aot1.png"),
          anime: "Attack on Titan",
        },
        {
          name: "aot2",
          image: require("../assets/aot2.png"),
          anime: "Attack on Titan",
        },
        {
          name: "aot3",
          image: require("../assets/aot3.png"),
          anime: "Attack on Titan",
        },
        {
          name: "aot4",
          image: require("../assets/aot4.png"),
          anime: "Attack on Titan",
        },
        {
          name: "aot5",
          image: require("../assets/aot5.png"),
          anime: "Attack on Titan",
        },
        {
          name: "aot6",
          image: require("../assets/aot6.png"),
          anime: "Attack on Titan",
        },
        {
          name: "aot7",
          image: require("../assets/aot7.png"),
          anime: "Attack on Titan",
        },
        {
          name: "aot8",
          image: require("../assets/aot8.png"),
          anime: "Attack on Titan",
        },
        {
          name: "lotr1",
          image: require("../assets/lotr1.png"),
          anime: "Senhor dos Anéis",
        },
        {
          name: "lotr2",
          image: require("../assets/lotr2.png"),
          anime: "Senhor dos Anéis",
        },
        {
          name: "lotr3",
          image: require("../assets/lotr3.png"),
          anime: "Senhor dos Anéis",
        },
        {
          name: "lotr4",
          image: require("../assets/lotr4.png"),
          anime: "Senhor dos Anéis",
        },
        {
          name: "lotr5",
          image: require("../assets/lotr5.png"),
          anime: "Senhor dos Anéis",
        },
        {
          name: "bc1",
          image: require("../assets/bc1.png"),
          anime: "Black Clover",
        },
        {
          name: "bc2",
          image: require("../assets/bc2.png"),
          anime: "Black Clover",
        },
        {
          name: "eits1",
          image: require("../assets/eits1.png"),
          anime: "The Eminence in the Shadows",
        },
        {
          name: "friends1",
          image: require("../assets/friends1.png"),
          anime: "Friends",
        },
        {
          name: "friends2",
          image: require("../assets/friends2.png"),
          anime: "Friends",
        },
        {
          name: "friends3",
          image: require("../assets/friends3.png"),
          anime: "Friends",
        },
        {
          name: "friends4",
          image: require("../assets/friends4.png"),
          anime: "Friends",
        },
        {
          name: "friends5",
          image: require("../assets/friends5.png"),
          anime: "Friends",
        },
        {
          name: "friends6",
          image: require("../assets/friends6.png"),
          anime: "Friends",
        },
        {
          name: "friends7",
          image: require("../assets/friends7.png"),
          anime: "Friends",
        },
        {
          name: "friends8",
          image: require("../assets/friends8.png"),
          anime: "Friends",
        },
        {
          name: "vintage1",
          image: require("../assets/vintage1.png"),
          anime: "Vintage",
        },
        {
          name: "vintage2",
          image: require("../assets/vintage2.png"),
          anime: "Vintage",
        },
        {
          name: "vintage3",
          image: require("../assets/vintage3.png"),
          anime: "Vintage",
        },
        {
          name: "op1",
          image: require("../assets/op1.png"),
          anime: "One Piece",
        },
        {
          name: "op2",
          image: require("../assets/op2.png"),
          anime: "One Piece",
        },
        {
          name: "op3",
          image: require("../assets/op3.png"),
          anime: "One Piece",
        },
        {
          name: "op4",
          image: require("../assets/op4.png"),
          anime: "One Piece",
        },
        {
          name: "op5",
          image: require("../assets/op5.png"),
          anime: "One Piece",
        },
        {
          name: "op6",
          image: require("../assets/op6.png"),
          anime: "One Piece",
        },
      ],
    };
  },
  computed: {
    availableColors() {
      return this.localSelection.type === "normal"
        ? this.normalColors
        : this.oversizedColors;
    },
    filteredDesigns() {
      return this.designs.filter(
        (design) => design.anime === this.localSelection.anime
      );
    },
  },
  methods: {
    updateParent() {
      this.$emit("updateSelection", this.localSelection);
    },
    selectColor(color) {
      this.localSelection.color = color;
      this.updateParent();
    },
    selectDesign(design, side) {
      if (side === "front") {
        this.localSelection.frontDesign = design;
      } else if (side === "back") {
        this.localSelection.backDesign = design;
      }
      this.updateParent();
    },
    handleTypeChange() {
      this.localSelection.color = this.availableColors[0].name;
      this.updateParent();
    },
    handleAnimeChange() {
      this.localSelection.frontDesign = null;
      this.localSelection.backDesign = null;
      this.updateParent();
    },
  },
};
</script>

<style scoped>
.tshirt-selector {
  margin: 20px;
  padding: 15px;
  background: rgb(255, 251, 214);
  background: linear-gradient(
    180deg,
    rgba(255, 251, 214, 1) 70%,
    rgba(217, 181, 213, 1) 100%
  );
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  font-family: "New Amsterdam", sans-serif;
  font-weight: 400;
  font-style: normal;
  position: relative;
  z-index: 1;
  border: 5px solid transparent;
}

.tshirt-selector::before {
  content: "";
  position: absolute;
  top: -5px;
  left: -5px;
  right: -5px;
  bottom: -5px;
  border-radius: inherit;
  background: linear-gradient(
    90deg,
    red,
    orange,
    yellow,
    green,
    blue,
    indigo,
    violet,
    red
  );
  z-index: -1;
  background-size: 300% 300%;
  animation: move-border 4s infinite linear;
  mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: destination-out;
  mask-composite: exclude;
  border: 5px solid transparent;
}

@keyframes move-border {
  0% {
    background-position: 0% 50%;
  }
  100% {
    background-position: 200% 50%;
  }
}

label {
  font-weight: bold;
  color: #333;
}

.color-options {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 10px;
}

.color-button {
  color: white;
  width: 50px;
  height: 50px;
  margin: 5px;
  cursor: pointer;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-size: 18px;
  font-weight: 500;
  -webkit-text-stroke: 1px black;
  transition: transform 0.2s ease-in-out;
}

.color-button.selected {
  border: 2px solid #000;
  transform: scale(1.1);
}

.color-button:hover {
  transform: scale(1.1);
}

.design-options img {
  width: 50px;
  margin: 5px;
  cursor: pointer;
  border: 2px solid transparent;
  transition: transform 0.2s ease-in-out;
}

.design-options img.selected {
  border: 2px solid #000;
}

.design-options img:hover {
  transform: scale(1.1);
}

h2 {
  color: #de5a74;
  -webkit-text-stroke: 0.1px black;
  margin-top: 2px;
  margin-bottom: 2px;
  font-size: 30px;

}

label {
  -webkit-text-stroke: 0.1px black;
  color: #de5a74;
  font-size: 22px;
}

.estampa-row {
  display: flex;
  justify-content: space-evenly;
}
</style>
