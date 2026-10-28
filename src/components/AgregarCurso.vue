<script setup>
import { inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'

const navigateView = inject('navigateView', () => {})
const saved = ref(false)
</script>

<template>
  <SistemaLayout breadcrumb="Espacio Curricular > Agregar curso">
    <section class="panel form-panel">
      <span class="eyebrow">Nuevo espacio curricular</span>
      <h1>Agregar curso</h1>
      <p class="muted">Completá los datos para crear un curso y luego publicar sus tutorías.</p>
      <form class="form" @submit.prevent="saved = true">
        <label>Nombre del curso<input placeholder="Ej. Matemática" required /></label>
        <div class="form-row"><label>Año<select><option>1er año</option><option>3er año</option><option>5to año</option></select></label><label>División<input placeholder="Ej. 4° A" required /></label></div>
        <label>Descripción<textarea placeholder="Información del espacio curricular"></textarea></label>
        <div class="actions"><button class="btn primary">Guardar curso</button><button type="button" class="btn" @click="navigateView('cursos')">Cancelar</button></div>
        <div v-if="saved" class="notice">Curso guardado como borrador. <button type="button" class="btn soft" @click="navigateView('cursos')">Volver a cursos</button></div>
      </form>
    </section>
  </SistemaLayout>
</template>

<style scoped>.form-panel{max-width:820px}.eyebrow{display:block;color:#315fce;font-size:.78rem;font-weight:800;letter-spacing:.12em;text-transform:uppercase;margin-bottom:7px}.form-panel h1{margin-top:0}</style>




