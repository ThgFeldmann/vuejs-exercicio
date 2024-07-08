<script setup>
  import { reactive } from 'vue';

  const estado = reactive({
    inputA: '',
    inputB: '',
    operacoes: {
      adicao: (a, b) => a + b,
      subtracao: (a, b) => a - b,
      multiplicacao: (a, b) => a * b,
      divisao: (a, b) => (b !== 0 ? a / b : 'Calculo não existe (divisão por zero)'),
    },
    resultado: 0,
  });

  const calcular = () => {
    const { inputA, inputB, operacaoMatematica } = estado;
    estado.resultado = estado.operacoes[operacaoMatematica](parseFloat(inputA), parseFloat(inputB));
  }
</script>

<template>
  <div class="container">
    <h1>Calculadora Aritmética</h1>
    <div class="calculator">
      <label>Operação:</label>
      <br>
      <select v-model="estado.operacaoMatematica">
        <option value="adicao">Adição</option>
        <option value="subtracao">Subtração</option>
        <option value="multiplicacao">Multiplicação</option>
        <option value="divisao">Divisão</option>
      </select>
      <hr>
      <label>Primeiro número:</label>
      <br>
      <input @input="calcular" v-model="estado.inputA" type="number">
      <hr>
      <label>Segundo número:</label>
      <br>
      <input @input="calcular" v-model="estado.inputB" type="number">
      <hr>

      <p>Resultado: {{ estado.resultado }}</p>
    </div>
  </div>
</template>

<style scoped>
  label, p {
    font-size: large;
  }

  input, select {
    font-size: medium;
  }

  .container {
    position: relative;
    left: 30%;
    max-width: 30%;
    padding: 16px;
    background-color: #dddddd
  }

  .calculator {
    padding: 12px;
    border: 1px solid gray;
  }
</style>
