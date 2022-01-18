<template>
  <div class="container">
    <div class="row">
      <Search
        @emitSearch="getCard($event)"
      />
    </div>
    <div class="row">
      <div class="col-12">
       <div class="card" v-if="card">
         <h1>{{ transformArtist }}</h1>
         <img :src="card.image" alt="">
       </div>
       <div v-else-if="error">
         {{ error }}
       </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Search from './Search.vue';

export default {
  name: 'Main',
  data() {
    return {
      queryPath: 'https://api.scryfall.com/cards/named',
      textSearch: '',
      card: null,
      error: false,
    };
  },
  components: {
    Search,
  },
  computed: {
    transformArtist() {
      const array = this.card.artist.split(' ');
      const name = `${array[1]} ${array[0]}`;
      return name;
    },
  },
  created() {

  },
  methods: {
    getCard(text) {
      this.textSearch = text;
      this.card = null;
      axios.get(
        this.queryPath, {
          params: {
            fuzzy: this.textSearch,
          },
        },
      ).then((result) => {
        // console.log(result.data);
        // console.log(this);
        this.card = {
          artist: result.data.artist,
          image: result.data.image_uris.small,
        };
        this.error = false;
        // console.log(this.error);
      }).catch(() => {
        this.error = 'La carta cercata non esiste';
        // console.log(this.error);
      });
    },
  },
};
</script>

<style lang="scss">
  @import '~bootstrap/scss/bootstrap';
</style>
