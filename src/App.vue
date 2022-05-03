<template>
  <div id="app">
    <h1>Tarefas</h1>
    <BarraProgresso :progresso="progresso" />
    <InputRegistraTarefa @tarefaAdicionada="adicionarTarefa" />
    <TarefasEmGeral :tarefas="tarefas" />
  </div>
</template>

<script>
import TarefasEmGeral from "./components/Tarefas/TarefasEmGeral.vue";
import InputRegistraTarefa from "./components/InuptRegistraTarefa.vue";
import BarraProgresso from "./components/BarraProgresso.vue";

export default {
  components: {
    TarefasEmGeral,
    InputRegistraTarefa,
    BarraProgresso,
  },
  data() {
    return {
      tarefas: [],
    };
  },
  computed: {
    progresso() {
      const total = this.tarefas.length;
      const feito = this.tarefas.filter((t) => !t.pendente).length;
      return Math.round((feito / total) * 100) || 0;
    },
  },
  watch: {
    tarefas: {
      deep: true,
      handler() {
        localStorage.setItem("tarefas", JSON.stringify(this.tarefas));
      },
    },
  },
  methods: {
    adicionarTarefa(tarefa) {
      const tarefaComMesmoNome = (tarefaComparar) =>
        tarefaComparar.nome === tarefa.nome;
      const NovaTarefa = this.tarefas.filter(tarefaComMesmoNome).length == 0;

      if (NovaTarefa === true) {
        this.tarefas.push({
          nome: tarefa.nome,
          pendente: tarefa.pendente || true,
        });
      }
    },
  },
  created() {
    const json = localStorage.getItem("tarefas");
    const array = JSON.parse(json);
    this.tarefas = Array.isArray(array) ? array : [];
  },
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
  color: #fff;

  background: #41295a; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #2f0743,
    #41295a
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #2f0743,
    #41295a
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
}
</style>
