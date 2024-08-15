<template>
  <div id="app">
    <header>
      <img src="@/assets/anime-logo.png" alt="Meu Traje Nerd" class="logo" />
      <h1>Catálogo Interativo <br> Meu Traje Nerd</h1>
    </header>
    <TshirtSelector @updateSelection="updateSelection" />
    <TshirtPreview :selection="selection" />
    <h1 class="boujee-text">Siga nosso instagram! <br> @meutrajenerd</h1>
  </div>
</template>

<script>
import TshirtSelector from "./components/TshirtSelector.vue";
import TshirtPreview from "./components/TshirtPreview.vue";

export default {
  name: "App",
  components: {
    TshirtSelector,
    TshirtPreview,
  },
  data() {
    return {
      selection: {
        type: "normal",
        color: "white",
        design: null,
      },
    };
  },
  methods: {
    updateSelection(selection) {
      this.selection = selection;
    },
  },
};
</script>

<style scoped>
#app {
  text-align: center;
  margin-top: 20px;
  background: linear-gradient(to bottom right, #f5f7fa, #c3cfe2);
  font-family: "New Amsterdam", sans-serif;
  font-weight: 400;
  font-style: normal;
  color: #333;
}

header {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  margin: 20px;
}

.logo {
  margin-top: 20px;
  width: 100px;
}

h1 {
  font-size: 2.5em;
  letter-spacing: 2px;
  color: #DE5A74; /* Tom vibrante */
  text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
  -webkit-text-stroke: 0.3px #412348;
  margin-top: 2px;
  margin-bottom: 2px;
}

.boujee-text {
  --bg-size: 400%;
  --color-one: red;
  --color-two: orange;
  --color-three: yellow;
  --color-four: green;
  --color-five: blue;
  --color-six: indigo;
  --color-seven: violet;
  font-size: clamp(1rem, 25vmin, 2rem);
  background: linear-gradient(
    90deg,
    var(--color-one),
    var(--color-two),
    var(--color-three),
    var(--color-four),
    var(--color-five),
    var(--color-six),
    var(--color-seven),
    var(--color-one)
  ) 0 0 / var(--bg-size) 100%;
  color: transparent;
  background-clip: text;
  -webkit-background-clip: text;
  animation: move-bg 8s infinite linear;
}

@keyframes move-bg {
  to {
    background-position: var(--bg-size) 0;
  }
}

@media (prefers-reduced-motion: no-preference) {
  .boujee-text {
    animation: move-bg 8s linear infinite;
  }
  @keyframes move-bg {
    to {
      background-position: var(--bg-size) 0;
    }
  }
}
</style>
