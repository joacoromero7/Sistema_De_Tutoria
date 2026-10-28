<script setup>
import { inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
const saved = ref(false)
</script>
<template><SistemaLayout breadcrumb="Perfil > Editar"><section class="panel"><h1>Editar perfil</h1><form class="form" @submit.prevent="saved=true"><div class="form-row"><label>Nombre<input value="María" /></label><label>Apellido<input value="Becerra" /></label></div><label>Correo electrónico<input type="email" value="maria.becerra@escuela.edu.ar" /></label><label>Teléfono<input value="11 5555-1234" /></label><label>Rol<select><option>Profesor/a</option><option>Preceptor/a</option><option>Coordinador/a</option></select></label><div class="actions"><button class="btn primary">Guardar cambios</button><button type="button" class="btn" @click="navigateView('perfil')">Cancelar</button></div><p v-if="saved" class="notice">Perfil actualizado.</p></form></section></SistemaLayout></template>




