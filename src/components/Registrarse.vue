<script setup>
import SistemaLayout from './SistemaLayout.vue'
import { ref } from 'vue'
const sent = ref(false)
</script>
<template><SistemaLayout :show-sidebar="false"><section class="panel auth"><h1>Registrarse</h1><p class="muted">Creá una cuenta para gestionar tutorías.</p><form class="form" @submit.prevent="sent=true"><div class="form-row"><label>Nombre<input required /></label><label>Apellido<input required /></label></div><label>Correo electrónico<input type="email" required /></label><label>Contraseña<input type="password" required /></label><label>Rol<select><option>Profesor/a</option><option>Preceptor/a</option><option>Coordinador/a</option><option>Secretario/a</option><option>Director/a</option></select></label><button class="btn primary">Crear cuenta</button><p v-if="sent" class="notice">Cuenta preparada para registrarse.</p></form></section></SistemaLayout></template>
<style scoped>.auth{max-width:680px;margin:5vh auto}</style>
