<template>
  <div>
    <!-- ViewPort: This is where you can view the API being Outputted -->
    <div class="bg-gray-800 min-h-screen flex items-center justify-center p-13">
      <div class="text-center">
        <p class="text-lg font-bold text-white">{{ currentPokemon.name }}</p>
        <img v-if="currentPokemon.image" :src="currentPokemon.image" alt="Pokemon" class="mx-auto mb-4 rounded" />
        

        <!-- Controller: You can freely update the Pokemon being shown by this button -->
        <button @click="fetchRandomPokemon" class="bg-gray-900 font-bold text-white px-4 py-2 rounded">
          Who's Your Pokemon?
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentPokemon: {},
    };
  },
  methods: {
    async fetchRandomPokemon() {
      try {
        const randomPokemonId = Math.floor(Math.random() * 898) + 1; // There are 898 Pokemon in the PokeAPI
        const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${randomPokemonId}`);
        const data = await response.json();
        let capFC=(str)=>str.charAt(0).toUpperCase()+str.slice(1);

        this.currentPokemon = {
          name: capFC(data.name),
          image: data.sprites.front_default,
        };

      } catch (error) {
        console.error("Error fetching the Pokemon data:", error);
      }
    },
  },
  mounted() {
    this.fetchRandomPokemon();
  },
};
</script>
