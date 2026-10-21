<script setup>
import { inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
const email = ref(''); const password = ref(''); const message = ref('')
function login() { if (email.value && password.value) navigateView('inicio'); else message.value = 'Completá correo y contraseña.' }
</script>
<template><SistemaLayout :show-sidebar="false"><section class="panel auth"><h1>Iniciar sesión</h1><p class="muted">Ingresá al Sistema de Tutorías</p><form class="form" @submit.prevent="login"><label>Correo electrónico<input v-model="email" type="email" placeholder="nombre@escuela.edu.ar" required /></label><label>Contraseña<input v-model="password" type="password" placeholder="••••••••" required /></label><button class="btn primary">Ingresar</button><button type="button" class="link-button" @click="navigateView('recuperar-contrasena')">¿Olvidaste tu contraseña?</button><p v-if="message" class="notice">{{ message }}</p></form></section></SistemaLayout></template>
<style scoped>.auth{max-width:520px;margin:7vh auto}.link-button{border:0;background:none;padding:0;text-align:left;color:#5279a7;cursor:pointer}</style>
