<template>
  <div>
    <base-card>
      <base-button
        @click="setSelectedTab('resource-stored')"
        :mode="storedResButtonMode"
      >
        Lista de arquivos</base-button
      >
      <base-button
        @click="setSelectedTab('resource-add')"
        :mode="addResButtonMode"
      >
        Adicionar arquivos</base-button
      >
    </base-card>
    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </div>
</template>

<script>
import ResourceStored from './ResourceStored.vue';
import ResourceAdd from './ResourceAdd.vue';

export default {
  components: {
    ResourceStored,
    ResourceAdd,
  },
  data() {
    return {
      selectedTab: 'resource-stored',
      objetosArmazenados: [
        {
          id: 'meu-timao',
          titulo: 'Meu Timão',
          descricao: 'O melhor site de notícias do Corinthians',
          link: 'https://www.meutimao.com.br/',
        },
        {
          id: 'google',
          titulo: 'Google',
          descricao: 'O melhor site de busca da internet',
          link: 'https://google.com',
        },
      ],
    };
  },
  provide() {
    return {
      objetos: this.objetosArmazenados,
      addResource: this.addResource,
      deleteResource: this.removeResource
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'resource-stored' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'resource-add' ? null : 'flat';
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(titulo, descricao, url) {
      const newResource = {
        id: new Date().toISOString(),
        titulo: titulo,
        descricao: descricao,
        link: url,
      };
      this.objetosArmazenados.unshift(newResource);
      this.selectedTab = 'resource-stored';
    },
    removeResource(objId) {
      const objIndex = this.objetosArmazenados.findIndex(obj => obj.id === objId);
      this.objetosArmazenados.splice(objIndex, 1);
    },
  },
};
</script>
