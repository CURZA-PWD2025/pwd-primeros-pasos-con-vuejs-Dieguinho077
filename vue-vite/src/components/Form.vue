<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const nombreUser = ref("")
const email = ref("")
const password = ref("")  
const birthDate = ref("")
const datos = ref({
  nombre: "",
  email: "",
  password: "",
  birthDate: "",
  edad: 0,
})


  function calcularEdad(birthDate: string): number {
  const hoy = new Date();
  const cumpleanos = new Date(birthDate);
  let edad = hoy.getFullYear() - cumpleanos.getFullYear();
  const diferenciaMeses = hoy.getMonth() - cumpleanos.getMonth();
  if (diferenciaMeses < 0 || (diferenciaMeses === 0 && hoy.getDate() < cumpleanos.getDate())) {
    edad--;
  }
  return edad;
}

function datosGuardados() {
  if (nombreUser.value && email.value && password.value && birthDate.value) {
  datos.value = {
    nombre: nombreUser.value,
    email: email.value,
    password: password.value,
    birthDate: birthDate.value,
    edad: calcularEdad(birthDate.value)
  }

  console.log(datos.value)
  nombreUser.value = ""
  email.value = ""
  password.value = ""
  birthDate.value = "" 

 alert("Datos guardados con éxito") 
}
else {
  alert("Rellene todos los campos")
}
}

</script>

<template>
  <h1>{{ msg }}</h1>

<form @submit.prevent="datosGuardados">
    <input type="text" placeholder="Escribe tu nombre" v-model="nombreUser">
    <input type="email" placeholder="Escribe tu email" v-model="email">
    <input type="password" placeholder="Escribe tu contraseña" v-model="password">
    <input type="date" placeholder="Escribe tu fecha de nacimiento" v-model="birthDate">
    <input type="submit" value="Enviar">
</form>

<p>Nombre: {{ datos.nombre }}</p>
<p>Email: {{ datos.email }}</p>
<p>Contraseña: {{ datos.password }}</p>
<p>fecha de nacimiento: {{ datos.birthDate }}</p>
<p>Edad: {{ datos.edad }}</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}

form {
  display: flex;
  flex-direction: column;
  width: 500px; 
  padding: 20px;
  border: 2px solid #ccc;
  border-radius: 5px;
} 

input {
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  border: 2px solid #ccc;
}

input[type="submit"] {
  background-color: #4CAF50;
  color: white;
  cursor: pointer;
}

</style>