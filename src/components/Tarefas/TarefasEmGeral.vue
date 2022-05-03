<template>
  <div class="TarefasEmGeral">
    <template v-if="tarefas.length">
      <div
        id="classificarTarefa"
        class="tarefa"
        :class="estadoClasse"
        v-for="(tarefa, indice) in tarefas"
        :key="tarefa.nome"
        @click="alterarEstadoTarefa(indice)"
      >
        <span @click="deletarTarefa(indice)" class="fechar">X</span>
        <!-- <br>
        <br>
        <p><span @click="alterarEstadoTarefa(indice)" class="toggle">Alterar Estados</span></p> -->
        {{ tarefa.nome }}
      </div>
    </template>
    <p v-else class="semTarefas">Tudo Feito!</p>
  </div>
</template>

<script>
export default {
  component: {},
  data() {
    return {
      // contadorClickMudarEstado: 0,
      pendente: "pendente",
      feito: "feito",
    };
  },
  props: {
    tarefas: {
      type: Array,
      required: true,
    },
  },
  computed: {
    estadoClasse() {
      if (!this.tarefas.pendente === true) {
        return this.pendente;
      } else if (this.tarefas.pendente === true) {
        return this.feito;
      }
    },
  },
  methods: {
    deletarTarefa(indice) {
      this.tarefas.splice(indice, 1);
    },
    alterarEstadoTarefa(indice) {
      this.tarefas[indice].pendente = !this.tarefas[indice].pendente;

      if (!this.tarefas[indice].pendente === true) {
        return `class="tarefa ${this.pendente}"`;
      } else if (this.tarefas[indice].pendente === true) {
        return `class="tarefa ${this.feito}"`;
      }
    },
  },
};
</script>

<style scoped>
/* Grade com as tarefas */
.TarefasEmGeral {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.TarefasEmGeral .tarefa {
  margin: 10px;
}

.semTarefas {
  color: #aaa;
  font-size: 1.7rem;
}

/* Tarefas */
.tarefa {
  position: relative;
  box-sizing: border-box;
  width: 350px;
  height: 150px;
  padding: 10px;
  border-radius: 8px;
  font-size: 1.5rem;
  font-weight: 300;
  cursor: pointer;
  user-select: none;
  display: flex;
  justify-content: center;
  align-items: center;
}

.pendente {
  border-left: 12px solid #b73229;
  background-color: #f44336;
}

.feito {
  color: #ddd;
  border-left: 12px solid #0a8f08;
  background-color: #4caf50;
  text-decoration: line-through;
}

.pendente .fechar {
  background-color: #b73229;
}

.feito .fechar {
  background-color: #0a8f08;
}

.fechar {
  position: absolute;
  right: 10px;
  top: 10px;
  font-size: 0.9rem;
  font-weight: 600;
  height: 20px;
  width: 20px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
}

.toggle {
  position: absolute;
  right: 10px;
  top: 50px;
  font-size: 0.9rem;
  font-weight: 600;
  height: 20px;
  display: flex;
  justify-content: center;
  background: #0a8f08;
}
</style>