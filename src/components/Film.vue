<template>
  <div class="film">
      <p class="film-title">{{ film.title }}</p>
      <ul class="character-list">
        <li v-for="character in film.people" :key="character.id" class="character">
          {{ character.name }}
        </li>
      </ul>
    </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    film: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.film {
  text-align: left;
  box-shadow: 0px 0px 16px -3px #5d5d5dd4;
  border-radius: 5px;
  background-color: #fffefa;
}

.film-title {
 font-weight: bold;
 padding: 0 20px;
}

.character-list {

}

.character {

}
</style>
