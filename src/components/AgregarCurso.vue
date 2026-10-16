<script setup>
import SistemaLayout from './SistemaLayout.vue'
import { ref } from 'vue'; const saved=ref(false)
</script>
<template><SistemaLayout breadcrumb="Espacio Curricular > Agregar curso"><section class="panel"><h1>Agregar curso</h1><form class="form" @submit.prevent="saved=true"><label>Nombre del curso<input placeholder="Ej. Matemática" required /></label><div class="form-row"><label>Año<select><option>1er año</option><option>3er año</option><option>5to año</option></select></label><label>División<input placeholder="Ej. 4° A" /></label></div><label>Descripción<textarea placeholder="Información del espacio curricular"></textarea></label><button class="btn primary">Guardar curso</button><p v-if="saved" class="notice">Curso guardado como borrador.</p></form></section></SistemaLayout></template>
