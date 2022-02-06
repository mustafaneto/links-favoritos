<template>
  <ul>
    <resource-item
      v-for="obj in objetos"
      :key="obj.id"
      :id="obj.id"
      :titulo="obj.titulo"
      :descricao="obj.descricao"
      :link="obj.link"
    ></resource-item>
  </ul>
</template>

<script>
import ResourceItem from './ResourceItem.vue'

export default {
    inject: ['objetos'],
    components: {
        ResourceItem
    }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>