<script setup>
import SistemaLayout from './SistemaLayout.vue'
import { ref } from 'vue'; const sent=ref(false)
</script>
<template><SistemaLayout :show-sidebar="false"><section class="panel auth"><h1>Recuperar contraseña</h1><p class="muted">Te enviaremos un enlace para recuperar el acceso.</p><form class="form" @submit.prevent="sent=true"><label>Correo electrónico<input type="email" placeholder="nombre@escuela.edu.ar" required /></label><button class="btn primary">Enviar enlace</button><p v-if="sent" class="notice">Si el correo existe, recibirás instrucciones.</p></form></section></SistemaLayout></template><style scoped>.auth{max-width:540px;margin:7vh auto}</style>
