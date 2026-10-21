<script setup>
import { inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
const reserved = ref(false)
function reserve() { reserved.value = true }
</script>
<template><SistemaLayout breadcrumb="Espacio Curricular > Matemática > Reservar tutoría"><section class="panel"><h1>Reservar tutoría</h1><form class="form" @submit.prevent="reserve"><div class="form-row"><label>Estudiante<input value="Juan Pérez" /></label><label>Curso<select><option>5to año · 4° A</option><option>3er año · 3° B</option></select></label></div><div class="form-row"><label>Materia<input value="Matemática" /></label><label>Docente<select><option>María Becerra</option><option>Joaquín Pérez</option></select></label></div><div class="form-row"><label>Fecha<input type="date" /></label><label>Horario<select><option>Miércoles · 7:30 a 8:20</option><option>Jueves · 15:30 a 16:30</option></select></label></div><label>Motivo<textarea placeholder="Recuperación de contenidos"></textarea></label><button class="btn primary">Confirmar reserva</button><div v-if="reserved" class="notice">Solicitud registrada y pendiente de confirmación. <button type="button" class="btn soft" @click="navigateView('mis-tutorias')">Ver mis tutorías</button></div></form></section></SistemaLayout></template>
