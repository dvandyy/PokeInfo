<template>
  <div class="home">
    <header>
      <a class="logo">
        <img
          src="https://fontmeme.com/permalink/200615/98ca1cc5911afa73be85fd3bfd688874.png"
          alt="pokemon-font"
          border="0"
      /></a>
      <form>
        <input
          type="text"
          placeholder="Find pokemon..."
          autofocus
          v-model="searchPokemon"
        />
        <button @click.prevent="search"><i class="fas fa-search"></i></button>
      </form>
    </header>
    <PreviewContainer :filterValue="searchPokemon" ref="preview" />
  </div>
</template>

<script>
import PreviewContainer from '../components/PreviewContainer';

export default {
  name: 'Home',
  components: {
    PreviewContainer
  },
  data: function() {
    return {
      searchPokemon: ''
    };
  },

  methods: {
    search() {
      this.$refs.preview.searchPokemon();
      this.searchPokemon = '';
    }
  }
};
</script>

<style>
.home {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

header {
  height: 45vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.logo {
  margin-bottom: 50px;
}
form {
  border: solid 1px #000;
  border-radius: 30px;
  box-shadow: 0px 0px 28px 1px rgba(0, 0, 0, 0.75);
  background-color: #3a3a3d;
  height: 60px;
  width: 400px;
}

input {
  padding: 14px 20px;
  width: 320px;
  color: #fff;
  font-size: 24px;
  border: none;
  background-color: #3a3a3d;
}

button {
  position: relative;
  border: none;
  font-size: 24px;
  background-color: #3a3a3d;

  color: #fff;
  cursor: pointer;
}
</style>
