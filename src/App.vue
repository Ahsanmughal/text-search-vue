<template>
  <h1 class="title"> Text Search Project</h1>
  <TextSearch/>
</template>

<script>
import TextSearch from './components/TextSearch.vue';

export default {
  name: 'App',
  components: {
    TextSearch
  }
}
</script>

<style>
.title {
  text-align: center;
  margin-top: 20px;
}
.highlight {
  background-color: yellow;
  font-weight: bold;
}
</style>
