<script setup>
import { inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'

const navigateView = inject('navigateView', () => {})
const saved = ref(false)
const photoPreview = ref('')
const profile = ref({ name: 'María', surname: 'Becerra', email: 'maria.becerra@escuela.edu.ar', phone: '11 5555-1234', role: 'Profesor/a', bio: 'Acompaño a estudiantes en sus procesos de aprendizaje.' })

function onPhotoChange(event) {
  const file = event.target.files?.[0]
  if (file) photoPreview.value = URL.createObjectURL(file)
}
function saveProfile() { saved.value = true }
</script>

<template>
  <SistemaLayout breadcrumb="Perfil > Editar"><section class="panel profile-editor"><div class="profile-editor-heading"><div><span class="eyebrow">Personalización</span><h1>Editar perfil</h1><p class="muted">Actualizá tus datos para que tu perfil se vea más personal.</p></div><div class="profile-avatar-large" :style="photoPreview ? { backgroundImage: `url(${photoPreview})` } : {}"><span v-if="!photoPreview">MB</span></div></div>
    <form class="form" @submit.prevent="saveProfile"><div class="photo-picker"><label for="profile-photo" class="btn soft">Cambiar foto de perfil</label><input id="profile-photo" class="visually-hidden" type="file" accept="image/png,image/jpeg,image/webp" @change="onPhotoChange" /><small>PNG, JPG o WEBP · Máximo recomendado: 2 MB</small></div>
      <div class="form-row"><label>Nombre<input v-model="profile.name" required /></label><label>Apellido<input v-model="profile.surname" required /></label></div><label>Correo electrónico<input v-model="profile.email" type="email" required /></label><label>Teléfono<input v-model="profile.phone" /></label><label>Rol<select v-model="profile.role"><option>Profesor/a</option><option>Preceptor/a</option><option>Coordinador/a</option></select></label><label>Sobre mí<textarea v-model="profile.bio" placeholder="Contale a la comunidad quién sos"></textarea></label><div class="actions"><button class="btn primary">Guardar cambios</button><button type="button" class="btn" @click="navigateView('perfil')">Cancelar</button></div><div v-if="saved" class="notice">Perfil actualizado correctamente.</div>
    </form>
  </section></SistemaLayout>
</template>

<style scoped>
.profile-editor{max-width:900px}.profile-editor-heading{display:flex;align-items:center;justify-content:space-between;gap:22px;margin-bottom:25px}.eyebrow{color:#315fce;font-size:.78rem;font-weight:800;letter-spacing:.12em;text-transform:uppercase}.profile-editor-heading h1{margin:7px 0}.profile-avatar-large{width:92px;height:92px;display:grid;place-items:center;border-radius:28px;background:#dce8ff center/cover no-repeat;color:#315fce;font-size:1.6rem;font-weight:850;box-shadow:0 10px 24px rgba(49,95,206,.16)}.photo-picker{display:flex;align-items:center;gap:12px;flex-wrap:wrap;margin-bottom:5px}.photo-picker small{color:#8996a9}.visually-hidden{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);white-space:nowrap;border:0}@media(max-width:600px){.profile-editor-heading{align-items:flex-start;flex-direction:column-reverse}}
</style>
