<template>
  <div class="barraProgresso">
    <span class="valorBarraProgresso">{{ progresso }}%</span>
    <div class="itemBarraDeProgresso" :style="{ width: progresso + '%' }"></div>
  </div>
</template>

<script>
export default {
  props: {
    progresso: { type: Number, default: 0 },
  },
};
</script>

<style>
.barraProgresso {
  position: relative;
  width: 80%;
  border: 1px solid #fff;
  color: #fff;
  border-radius: 8px;
  margin-bottom: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.itemBarraDeProgresso {
  position: absolute;
  border-radius: 8px;
  height: 100%;
  background-color: #4caf50;
  align-self: flex-start;
}

.valorBarraProgresso {
  z-index: 1;
  font-size: 1.5rem;
}
</style>
