<script setup>
import { inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
const sent = ref(false)
function register() { sent.value = true; setTimeout(() => navigateView('inicio-sesion'), 500) }
</script>
<template><SistemaLayout :show-sidebar="false"><section class="panel auth"><h1>Registrarse</h1><p class="muted">Creá una cuenta para gestionar tutorías.</p><form class="form" @submit.prevent="register"><div class="form-row"><label>Nombre<input required /></label><label>Apellido<input required /></label></div><label>Correo electrónico<input type="email" required /></label><label>Contraseña<input type="password" required /></label><label>Rol<select><option>Profesor/a</option><option>Preceptor/a</option><option>Coordinador/a</option><option>Secretario/a</option><option>Director/a</option></select></label><button class="btn primary">Crear cuenta</button><p v-if="sent" class="notice">Cuenta creada. Redirigiendo al inicio de sesión...</p></form></section></SistemaLayout></template>
<style scoped>.auth{max-width:680px;margin:5vh auto}</style>




