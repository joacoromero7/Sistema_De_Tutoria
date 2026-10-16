<script setup>
import SistemaLayout from './SistemaLayout.vue'
import { ref } from 'vue'
const email = ref(''); const password = ref(''); const message = ref('')
function login() { message.value = email.value && password.value ? 'Inicio de sesión listo para conectar con la API.' : 'Completá correo y contraseña.' }
</script>
<template><SistemaLayout :show-sidebar="false"><section class="panel auth"><h1>Iniciar sesión</h1><p class="muted">Ingresá al Sistema de Tutorías</p><form class="form" @submit.prevent="login"><label>Correo electrónico<input v-model="email" type="email" placeholder="nombre@escuela.edu.ar" /></label><label>Contraseña<input v-model="password" type="password" placeholder="••••••••" /></label><button class="btn primary">Ingresar</button><a href="#">¿Olvidaste tu contraseña?</a><p v-if="message" class="notice">{{ message }}</p></form></section></SistemaLayout></template>
<style scoped>.auth{max-width:520px;margin:7vh auto}.auth a{color:#5279a7}</style>
