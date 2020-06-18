<template>
  <div class="pokemon-flex">
    <div class="pokemon">
      <header class="pokemon-pics">
        <h1>{{ pokemon.name }}</h1>
        <img :src="pokemon.images.front" alt="" />
        <img :src="pokemon.images.back" alt="" />
        <router-link to="/" class="close-btn">X</router-link>
      </header>
      <section class="pokemon-stats">
        <div class="stats-container">
          <h3>Height</h3>
          <p>{{ pokemon.baseStats.height }} dm</p>
        </div>
        <div class="stats-container">
          <h3>Weight</h3>
          <p>{{ pokemon.baseStats.weight }} hg</p>
        </div>
        <div class="stats-container">
          <h3>HP</h3>
          <p>{{ pokemon.baseStats.hp }}</p>
        </div>
        <div class="stats-container">
          <h3>Speed</h3>
          <p>{{ pokemon.baseStats.speed }}</p>
        </div>
        <div class="stats-container">
          <h3>Attack</h3>
          <p>{{ pokemon.baseStats.attack }}</p>
        </div>
        <div class="stats-container">
          <h3>Defense</h3>
          <p>{{ pokemon.baseStats.defense }}</p>
        </div>
        <div class="stats-container">
          <h3>Special Attack</h3>
          <p>{{ pokemon.baseStats.specialAttack }}</p>
        </div>
        <div class="stats-container">
          <h3>Special Defense</h3>
          <p>{{ pokemon.baseStats.specialDefense }}</p>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Pokemon',
  data: function() {
    return {
      pokemon: {}
    };
  },
  methods: {},
  created: function() {
    const url = `https://pokeapi.co/api/v2/pokemon/${this.$route.params.name}/`;
    fetch(url)
      .then(res => res.json())
      .then(data => {
        this.pokemon = {
          name: data.name,
          images: {
            front: data.sprites.front_default,
            back: data.sprites.back_default
          },
          baseStats: {
            weight: data.weight,
            height: data.height,
            hp: data.stats[0].base_stat,
            attack: data.stats[1].base_stat,
            defense: data.stats[2].base_stat,
            specialAttack: data.stats[3].base_stat,
            specialDefense: data.stats[4].base_stat,
            speed: data.stats[5].base_stat
          }
        };
        console.log(this.pokemon);
      })
      .catch(err => console.log(err));
  }
};
</script>

<style>
.pokemon-pics {
  width: 30vw;
  height: auto;
}

.pokemon-pics img {
  margin-bottom: 10px;
  width: 15vw;
  height: auto;
}

.pokemon-pics h1 {
  border: 1px solid #000;
  box-shadow: 0px 0px 28px 1px rgba(0, 0, 0, 0.75);
  border-radius: 10px;
  width: 300px;
  margin-bottom: 30px;
}

.pokemon-flex {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 10vh;
  margin-bottom: 10vh;
}

.pokemon {
  min-height: 80vh;
  width: 75vw;
  border: 1px solid #000;
  border-radius: 10px;
  box-shadow: 0px 0px 28px 1px rgba(0, 0, 0, 0.75);
  display: flex;
  align-items: center;
  padding: 20px;
}

.pokemon h1 {
  text-transform: capitalize;
}

.pokemon-stats {
  display: flex;
  flex-wrap: wrap;
  width: 40vw;
  min-height: 40vh;
  justify-content: space-around;
  align-items: flex-start;
}

.pokemon-stats .stats-container {
  height: 80px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

.pokemon-stats .stats-container h3 {
  border: 1px solid #000;
  box-shadow: 0px 0px 28px 1px rgba(0, 0, 0, 0.75);
  border-radius: 10px;
  width: 250px;
}

.close-btn {
  position: absolute;
  left: 83vw;
  top: 13vh;
  color: red;
  font-weight: bold;
  border: 1px solid #000;
  box-shadow: 0px 0px 28px 1px rgba(0, 0, 0, 0.75);
  border-radius: 10px;
  padding: 10px 15px;
}

.close-btn:hover {
  background-color: #3a3a3d;
  transition: background-color 200ms ease-in;
}

@media only screen and (max-width: 720px) {
  .pokemon {
    flex-direction: column;
  }
  .close-btn {
    display: none;
  }
}
</style>
