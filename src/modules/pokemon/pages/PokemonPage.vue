<template>
  <h1>
    Pokemon <span># {{ id }}</span>
    <div v-if="pokemon">
      <img :src="pokemon.sprites.front_default" :alt="pokemon.name">
    </div>
  </h1>
</template>

<script>
export default {
  props: {
    id: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      // id: this.$route.params.id
      pokemon: null
    }
  },
  created() {
    // const {id} = this.$route.params
    this.getPokemon()
  },
  methods: {
    async getPokemon(I) {
      try {
        const pokemon = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.id}`)
            .then(r => r.json())
        console.log(pokemon)
        this.pokemon = pokemon
      } catch (error) {
        console.log(error)
        this.$router.push('/')
        console.log('No hay nada que hacer aqui')
      }

    }
  },
  watch: {
    id(value, oldValue) {
      this.getPokemon()
    }
  }
}
</script>

<style lang="scss" scoped>

</style>