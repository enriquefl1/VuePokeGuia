<template>
  <div id="app">
    <div class="container border">
      <div class="row">
        <div class="col-12">
          <img
            src="./assets/pokemon-logo.png"
            alt="Logo Pockemon"
            class="poke-logo"
          />
        </div>
        <div class="col-12">
          <h1>PokeGuía</h1>
        </div>
        <div class="col-12">
          <p>
            <strong>
              Bienvenido a la PokéGuía, una aplicación que te ayudará a
              encontrar a tus Pokémon favoritos.
            </strong>
          </p>
        </div>
        <div class="col-12">
          <label>Nombre:</label>
          <input type="text" v-model="pokeValorInicio" />
          <input type="button" value="Buscar Poke" @click="buscarPoke" />
        </div>
        <div class="col-12">
          <img class="poke-img border" :src="pokeImagen" :alt="pokenombre" />
        </div>
        <div class="col-6">
          <h2>Movimientos</h2>
          <ul class="poke-lista">
            <li v-for="pokeMove in pokeMovimientos" :key="pokeMove.name">
              <strong>{{ pokeMove.move.name }}</strong>
            </li>
          </ul>
        </div>
        <div class="col-6">
          <h2>Habilidades</h2>
          <ul class="poke-lista">
            <li v-for="pokeHabil in pokeHabilidades" :key="pokeHabil.name">
              <strong>{{ pokeHabil.ability.name }}</strong>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      pokeValorInicio: "pikachu",
      URL: "https://pokeapi.co/api/v2/pokemon/",
      pokeData: {},
    };
  },
  computed: {
    pokeNombre() {
      return this.pokeData.name;
    },
    pokeImagen() {
      return this.pokeData?.sprites?.front_default;
    },
    pokeMovimientos() {
      return this.pokeData?.moves;
    },
    pokeHabilidades() {
      return this.pokeData?.abilities;
    },
  },
  create() {
    this.buscarPoke();
  },
  methods: {
    buscarPoke() {
      this.TraePokeAPI();
    },
    async TraePokeAPI() {
      try {
        const resp = await fetch(this.URL + this.pokeValorInicio);
        const data = await resp.json();
        this.pokeData = data;
        console.log(this.pokeData);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.poke-logo {
  width: 400px;
  margin: 0 auto;
}

.poke-img {
  width: 150px;
  margin: 0 auto;
}

.poke-lista {
  width: 200px;
  margin: 0 auto;
}
</style>
