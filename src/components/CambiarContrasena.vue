<script setup>
import { inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
const saved = ref(false)
</script>
<template><SistemaLayout :show-sidebar="false"><section class="panel auth"><h1>Cambiar contraseña</h1><form class="form" @submit.prevent="saved=true"><label>Nueva contraseña<input type="password" required /></label><label>Repetir contraseña<input type="password" required /></label><button class="btn primary">Guardar contraseña</button><div v-if="saved" class="notice">Contraseña actualizada. <button type="button" class="btn soft" @click="navigateView('perfil')">Volver al perfil</button></div></form></section></SistemaLayout></template><style scoped>.auth{max-width:540px;margin:7vh auto}</style>
