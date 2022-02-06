<template>
  <div>
    <base-dialog v-if="inputIsInvalid" titulo="Digito Inválido" @close="confirmError">
      <template #default>
        <p>Infelizmente, um dos campos digitados está invalido.</p>
        <p>Por favor, verifique se você digitou corretamente todos os campos.</p>
      </template>
      <template #actions>
          <base-button @click="confirmError">Ok</base-button>
      </template>
    </base-dialog>
    <base-card>
      <form @submit.prevent="submitData">
        <div class="form-control">
          <label for="titulo">Titulo</label>
          <input id="titulo" name="titulo" type="text" ref="tituloInput" />
        </div>
        <div class="form-control">
          <label for="descricao">Descrição</label>
          <textarea
            id="descricao"
            name="descricao"
            rows="3"
            ref="descInput"
          ></textarea>
        </div>
        <div class="form-control">
          <label for="link">Link</label>
          <input id="link" name="link" type="url" ref="linkInput" />
        </div>
        <div>
          <base-button type="submit">Salvar</base-button>
        </div>
      </form>
    </base-card>
  </div>
</template>

<script>
export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  methods: {
    submitData() {
      const enteredTitulo = this.$refs.tituloInput.value;
      const enteredDescricao = this.$refs.descInput.value;
      const enteredLink = this.$refs.linkInput.value;

      if (
        enteredTitulo.trim() === '' ||
        enteredDescricao.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }

      this.addResource(enteredTitulo, enteredDescricao, enteredLink);
    },
    confirmError() {
        this.inputIsInvalid = false;
    }
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
