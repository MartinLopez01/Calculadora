<template >
  <div class="calculadora" >
    <h1>Calculadora</h1>
    <div class="display">
      <input type="text" v-model="input" readonly />
    </div>
    <div class="botones">
      <button
        v-for="btn in botones"
        :key="btn"
        @click="agregar(btn)"
        :class="{ operador: isOperador(btn) }"
      >
        {{ btn }}
      </button>
      <button class="igual" @click="calcular">=</button>
      <button class="borrar" @click="borrar">C</button>
    </div>
    <h2>Historial</h2>
    <ul class="historial">
      <li v-for="(item, index) in historial" :key="index">{{ item }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: "",
      historial: [],
      botones: ["7", "8", "9", "/", "4", "5", "6", "*", "1", "2", "3", "-", "0", ".", "+"],
    };
  },
  methods: {
    agregar(valor) {
      this.input += valor;
    },
    calcular() {
      try {
        const resultado = eval(this.input); // No recomendado en producción por riesgos de seguridad
        this.historial.push(`${this.input} = ${resultado}`);
        this.input = resultado.toString();
      } catch (error) {
        alert("Error en la operación");
      }
    },
    borrar() {
      this.input = "";
    },
    isOperador(valor) {
      return ["+", "-", "*", "/"].includes(valor);
    },
  },
  
};
</script>

<style scoped>

/* Contenedor principal */
.calculadora {
  max-width: 360px;
  margin: auto;
  padding: 20px;
  border-radius: 12px;
  background-color: #222222;
  color: #ffffff;
  text-align: center;
  font-family: 'Roboto', sans-serif;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
}

/* Título */
h1 {
  font-size: 1.8rem;
  margin-bottom: 20px;
  color: #f2f2f2;
}

/* Pantalla */
.display input {
  width: 95%;
  font-size: 1.8rem;
  text-align: right;
  margin-bottom: 15px;
  padding: 10px;
  border: none;
  border-radius: 8px;
  background-color: #2e2e3d;
  color: #ffffff;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.5);
}

/* Botones */
.botones {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.botones button {
  padding: 15px;
  font-size: 1.4rem;
  border: none;
  border-radius: 8px;
  background-color: #3e3e4e;
  color: #ffffff;
  cursor: pointer;
  transition: background-color 0.2s, transform 0.2s;
}

/* Botones especiales */
.botones button.operador {
  background-color: #ff9800;
}

.botones button.igual {
  grid-column: span 2;
  background-color: #4caf50;
}

.botones button.borrar {
  grid-column: span 2;
  background-color: #f44336;
}

/* Animación al presionar botones */
.botones button:active {
  transform: scale(0.95);
}

/* Historial */
h2 {
  margin-top: 25px;
  font-size: 1.4rem;
  color: #cfcfcf;
}

.historial {
  list-style: none;
  padding: 0;
  margin: 10px 0;
  text-align: left;
  max-height: 150px;
  overflow-y: auto;
}

.historial li {
  background-color: #2e2e3d;
  padding: 8px;
  margin-bottom: 5px;
  border-radius: 6px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}
</style>
