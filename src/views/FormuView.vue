<script setup lang="ts">
import { ref } from 'vue';

const nombre = ref('');
const apellido = ref('');
const edad = ref(0);
const genero = ref('');
const telefono = ref('');
const error = ref('');
const mostrarDatos = ref(false);

const validarFormulario = () => {

  error.value = '';


  if (nombre.value.length > 18 || apellido.value.length > 18) {
    error.value = 'Nombre y apellido deben tener máximo 18 caracteres.';
    return;
  }

  if (nombre.value.toLowerCase() === apellido.value.toLowerCase()) {
    error.value = 'Nombre y apellido no pueden ser iguales.';
    return;
  }

  if (edad.value < 0 || edad.value > 60) {
    error.value = 'Edad debe estar entre 0 y 60.';
    return;
  }

  const generosValidos = ['Hombre', 'Mujer', 'Otro'];
  if (!generosValidos.includes(genero.value)) {
    error.value = 'Género debe ser Hombre, Mujer u Otro.';
    return;
  }

  if (telefono.value.length > 10) {
    error.value = 'Número de teléfono no puede tener más de 10 dígitos.';
    return;
  }

  mostrarDatos.value = true;
};

</script>

<template>
  <main>
    <h2>Formulario!</h2>
    <form @submit.prevent="validarFormulario" class="formulario">
      <label for="nombre">Nombre:</label>
      <input type="text" v-model="nombre" id="nombre">

      <label for="apellido">Apellido:</label>
      <input type="text" v-model="apellido" id="apellido">

      <label for="edad">Edad:</label>
      <input type="number" v-model="edad" id="edad">

      <label for="genero">Género:</label>
      <select v-model="genero" id="genero">
        <option value="Hombre">Hombre</option>
        <option value="Mujer">Mujer</option>
        <option value="Otro">Otro</option>
      </select>

      <label for="telefono">Teléfono:</label>
      <input type="tel" v-model="telefono" id="telefono">

      <button type="submit">Enviar</button>
    </form>

    <h3>Información en tiempo real:</h3>
    <div v-if="mostrarDatos" class="resultado">
      <p><strong>Nombre:</strong> {{ nombre }}</p>
      <p><strong>Apellido:</strong> {{ apellido }}</p>
      <p><strong>Edad:</strong> {{ edad }}</p>
      <p><strong>Género:</strong> {{ genero }}</p>
      <p><strong>Teléfono:</strong> {{ telefono }}</p>
    </div>


    <div v-if="error" class="error">{{ error }}</div>
  </main>
</template>

<style scoped>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 20px;
  }

  .formulario {
    width: 300px;
    background-color: #f4f4f4;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }

  label {
    margin-top: 10px;
    display: block;
  }

  input, select {
    width: 100%;
    padding: 8px;
    margin-top: 5px;
    margin-bottom: 10px;
    box-sizing: border-box;
  }

  button {
    background-color: #4caf50;
    color: white;
    padding: 10px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  button:hover {
    background-color: #45a049;
  }

  .resultado {
    margin-top: 20px;
    font-size: 18px;
    color: #333;
  }

  .error {
    color: red;
    margin-top: 10px;
  }
</style>
