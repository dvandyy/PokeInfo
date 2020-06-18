<template>
  <div class="preview">
    <img :src="img" />
    <h2>{{ name }}</h2>
  </div>
</template>

<script>
export default {
  name: 'PokemonPreview',
  props: {
    name: String,
    img: String
  }
};
</script>

<style>
.preview {
  min-width: 120px;
  margin: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 1px solid #000;
  padding: 10px 15px;
  border-radius: 10px;
  box-shadow: 0px 0px 28px 1px rgba(0, 0, 0, 0.75);
  text-transform: capitalize;
  color: #fff;
  width: 160px;
}

.preview:hover {
  background-color: #3a3a3d;
  transition: background-color 200ms ease-in;
}
</style>
