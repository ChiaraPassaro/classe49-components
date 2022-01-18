<template>
  <div class="form-control">
    <input type="text" v-model="textSearch" @keyup.enter="sendSearch()">
  </div>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      textSearch: '',
    };
  },
  props: {

  },
  methods: {
    sendSearch() {
      console.log(this.textSearch);
      this.$emit('emitSearch', this.textSearch);
    },
  },
};
</script>

<style>

</style>
