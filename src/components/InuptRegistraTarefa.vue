<template>
  <div class="nova-tarefa">
    <input
      class="formulario-padrao nova-tarefa"
      v-model="nome"
      @keydown.enter="adicionar"
      type="text"
      name="AdicionarTarefa"
    />
    <button class="formulario-padrao" @click="adicionar">+</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nome: "",
    };
  },
  methods: {
    adicionar() {
      this.$emit("tarefaAdicionada", { nome: this.nome });
      this.nome = "";
    },
  },
};
</script>

<style scoped>
.nova-tarefa {
  margin-bottom: 20px;
}

.formulario-padrao {
  outline: none;
  font-size: 2rem;
  border: 1px solid #fff;
  padding: 5px 10px 8px;
  color: #fff;
}

input.formulario-padrao {
  width: 500px;
  background: #fff2;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}

button.formulario-padrao {
  border-left: none;
  background-color: #2196f3;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
}
</style>