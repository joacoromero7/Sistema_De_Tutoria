<script setup>
import { inject } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
</script>
<template><SistemaLayout breadcrumb="Mis tutorías"><section class="panel"><h1>Mis tutorías</h1><p class="muted">Tutorías reservadas y su estado actual.</p><table class="table"><thead><tr><th>Materia</th><th>Curso</th><th>Fecha y horario</th><th>Estado</th><th></th></tr></thead><tbody><tr><td>Matemática</td><td>5to · 4° A</td><td>12/08 · 7:30</td><td><span class="status">Confirmada</span></td><td><button class="btn" @click="navigateView('detalle-tutoria')">Ver detalle</button></td></tr><tr><td>Física</td><td>3er · 3° B</td><td>15/08 · 12:30</td><td><span class="status">Pendiente</span></td><td><button class="btn" @click="navigateView('detalle-tutoria')">Ver detalle</button></td></tr></tbody></table></section></SistemaLayout></template>




