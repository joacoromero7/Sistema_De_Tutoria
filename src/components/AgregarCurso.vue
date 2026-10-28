<script setup>
import { inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'

const navigateView = inject('navigateView', () => {})
const saved = ref(false)
const bannerPreview = ref('')
const bannerColor = ref('#6b9bf2')
const course = ref({ name: 'Matemática', year: '5to año', division: '4° A', description: '' })

function onBannerChange(event) {
  const file = event.target.files?.[0]
  if (file) bannerPreview.value = URL.createObjectURL(file)
}
function saveCourse() { saved.value = true }
</script>

<template>
  <SistemaLayout breadcrumb="Espacio Curricular > Agregar curso"><section class="panel form-panel"><span class="eyebrow">Nuevo espacio curricular</span><h1>Agregar curso</h1><p class="muted">Completá los datos y personalizá el banner que aparecerá en la tarjeta del curso.</p><form class="form" @submit.prevent="saveCourse"><label>Nombre de la materia<input v-model="course.name" placeholder="Ej. Matemática" required /></label><div class="form-row"><label>Año<select v-model="course.year"><option>1er año</option><option>3er año</option><option>5to año</option></select></label><label>División<input v-model="course.division" placeholder="Ej. 4° A" required /></label></div><label>Descripción<textarea v-model="course.description" placeholder="Información del espacio curricular"></textarea></label><div class="banner-section"><div><h2>Banner del curso</h2><p class="muted">Elegí un color o subí una imagen para personalizarlo.</p></div><div class="banner-preview" :style="{ backgroundColor: bannerColor, backgroundImage: bannerPreview ? `url(${bannerPreview})` : '' }"><strong>{{ course.name || 'Nombre de la materia' }}</strong><span>{{ course.year }} · {{ course.division }}</span></div><div class="banner-controls"><label>Color del banner<input v-model="bannerColor" type="color" /></label><label for="course-banner" class="btn soft upload-label">Subir imagen</label><input id="course-banner" class="visually-hidden" type="file" accept="image/png,image/jpeg,image/webp" @change="onBannerChange" /></div></div><div class="actions"><button class="btn primary">Guardar curso</button><button type="button" class="btn" @click="navigateView('cursos')">Cancelar</button></div><div v-if="saved" class="notice">Curso guardado como borrador. <button type="button" class="btn soft" @click="navigateView('cursos')">Volver a cursos</button></div></form></section></SistemaLayout></template>

<style scoped>.form-panel{max-width:900px}.eyebrow{display:block;color:#315fce;font-size:.78rem;font-weight:800;letter-spacing:.12em;text-transform:uppercase;margin-bottom:7px}.form-panel h1{margin-top:0}.banner-section{display:grid;gap:14px;padding:20px;border:1px solid #e1e8f3;border-radius:18px;background:#fbfcff}.banner-section h2{margin:0 0 4px;font-size:1.1rem}.banner-preview{min-height:130px;display:flex;flex-direction:column;justify-content:flex-end;gap:4px;padding:20px;border-radius:15px;background-position:center;background-size:cover;color:#fff;box-shadow:inset 0 -80px 80px rgba(14,28,57,.35)}.banner-preview strong{font-size:1.35rem}.banner-preview span{font-size:.9rem}.banner-controls{display:flex;align-items:end;gap:18px;flex-wrap:wrap}.banner-controls input[type=color]{width:62px;height:43px;padding:4px}.upload-label{display:inline-flex;align-items:center;min-height:43px}.visually-hidden{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);white-space:nowrap;border:0}</style>
