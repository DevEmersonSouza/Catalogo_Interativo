<template>
  <div class="tshirt-preview">
    <h2>Veja Como sua nova Camiseta vai ficar:</h2>
    <div class="tshirt-row">
      <div
        class="tshirt zoom-container"
        @mouseover="isZoomed = true"
        @mouseleave="isZoomed = false"
      >
        <h3>Frente:</h3>
        <div :class="{ zoomed: isZoomed }">
          <img :src="tshirtImageUrl" class="tshirt-image" />
          <img
            v-if="selection.frontDesign"
            :src="frontDesignImageUrl"
            class="design"
          />
        </div>
      </div>
      <div
        v-if="selection.doubleSided"
        class="tshirt-back zoom-container"
        @mouseover="isZoomedBack = true"
        @mouseleave="isZoomedBack = false"
      >
        <div :class="{ zoomed: isZoomedBack }">
          <h3>Verso:</h3>
          <img :src="tshirtImageUrlVerso" class="tshirt-image" />
          <img
            v-if="selection.backDesign"
            :src="backDesignImageUrl"
            class="design"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TshirtPreview",
  props: ["selection"],
  data() {
    return {
      isZoomed: false,
      isZoomedBack: false,
    };
  },
  computed: {
    tshirtImageUrl() {
      return require(`../assets/${this.selection.color}-tshirt.png`);
    },
    tshirtImageUrlVerso() {
      return require(`../assets/${this.selection.color}-tshirtVERSO.png`);
    },
    frontDesignImageUrl() {
      return require(`../assets/${this.selection.frontDesign}.png`);
    },
    backDesignImageUrl() {
      return require(`../assets/${this.selection.backDesign}.png`);
    },
  },
};
</script>

<style scoped>
.tshirt-preview {
  margin: 20px;
  padding: 20px;
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

.tshirt-preview::before {
  content: '';
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


h2 {
  color: #de5a74;
  -webkit-text-stroke: 0.1px black;
  margin-top: 2px;
  margin-bottom: 2px;
  font-size: 30px;
}
h3 {
  color: #de5a74;
  -webkit-text-stroke: 0.1px black;
  margin-top: 2px;
  margin-bottom: 2px;
  font-size: 22px;
}

.tshirt {
  position: relative;
  width: 200px;
  overflow: hidden;
  cursor: zoom-in;
}

.tshirt-back {
  position: relative;
  width: 200px;
  overflow: hidden;
  cursor: zoom-in;
}

.tshirt-image {
  width: 100%;
  height: auto;
}

.design {
  position: absolute;
  top: 57%;
  left: 49%;
  width: 50%;
  height: auto;
  transform: translate(-50%, -50%);
  z-index: 10;
}

.zoom-container {
  position: relative;
}

.zoomed {
  transform: scale(2);
  transform-origin: center;
  cursor: zoom-out;
}

.tshirt-row {
  display: flex;
  justify-content: space-evenly;
}

</style>
