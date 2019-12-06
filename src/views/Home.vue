<template>
  <div class="home">
    <h1>PokeDex</h1>
    <form>
      <input type="number" v-model="pokemonId" />
      <button @click="getAllPokemon">Check Pokedex</button>
    </form>
    <h2>{{ pokemonTitle }} {{ pokemonId }}</h2>
    <img :alt="pokemonName" :src="pokemonImage" />
    <HelloWorld :msg="pokemonTitle" />
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "home",
  components: {
    HelloWorld
  },
  data() {
    return {
      pokemonId: 1,
      pokemonName: "",
      pokemonImage: ""
    };
  },
  computed: {
    pokemonTitle() {
      return "Pokemon: " + this.pokemonName;
    }
  },
  mounted() {
    this.getAllPokemon();
  },
  methods: {
    async getAllPokemon() {
      const { data, status } = await axios.get(
        `https://pokeapi.co/api/v2/pokemon/${this.pokemonId}`
      );
      if (status === 200) {
        this.pokemonName = data.name;
        this.pokemonImage = data.sprites.front_default;
        // eslint-disable-next-line
        console.log(this.pokemonName, this.pokemonImage);
      } else {
        // eslint-disable-next-line
        console.log("didnt work yo");
      }
    }
  }
};
</script>
