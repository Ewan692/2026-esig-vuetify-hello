<script setup>
  const newPokemon = ref('Charizard')
  const inputNewPokemon = useTemplateRef('inputNewPokemon')
  const showElectricOnly = ref(false)
  const pokemons = ref([
    { name: 'Pikachu', type: 'Electric' },
    { name: 'Bulbasaur', type: 'Grass' },
    { name: 'Charmander', type: 'Fire' },
    { name: 'Squirtle', type: 'Water' },
    { name: 'Jolteon', type: 'Electric' },
  ])

  // TODO: ref pour le nom
  // TODO: ref pour le filtre
  // TODO: computed filteredPokemons
  // TODO: function addPokemon()
  function addPokemon () {
    // Ajoute un pokémon à la fin du tableau
    pokemons.value.push({ name: newPokemon.value, type: 'Electric' })
    // On vide le champ
    newPokemon.value = ''
    // Remet le focus au champ
    inputNewPokemon.value.focus()
  }

  // Computed qui filtre les pokémons
  const filteredPokemons = computed(() => {
    if (showElectricOnly.value) {
      return pokemons.value.filter(pokemon => pokemon.type === 'Electric')
    }
    return pokemons.value
  })
</script>

<template>
  <main>
    <h1>Mon Pokédex</h1>
    <p>{{ newPokemon }}</p>

    <div>
      <input ref="inputNewPokemon" v-model="newPokemon" type="text" @keyup.enter="addPokemon()">
      <button @click="addPokemon()">Ajouter</button>
    </div>

    <h2>Mes pokémons</h2>
    <div>
      <label>
        <input v-model="showElectricOnly" type="checkbox">
        Afficher uniuqment les types électriques
      </label>
    </div>

    <p v-if="filteredPokemons.length === 0">Auncun pokémon attrapé !</p>
    <ul v-else>
      <li v-for="p in filteredPokemons" :key="p.name">{{ p.name }} ({{ p.type }})</li>
    </ul>
  </main>
</template>

<style scoped>
  main {
    padding: 20px;
  }

  h1 {
    color: orange;
  }

  input {
    border: 2px solid orange;
    padding: 5px;
  }

  button {
    border: 2px solid orange;
    padding: 5px;
    margin: 0 1em;
  }
</style>
