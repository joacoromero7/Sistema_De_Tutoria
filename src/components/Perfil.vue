<script setup>
import { inject } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
const currentRole = inject('currentRole', 'Profesor/a')
</script>
<template><SistemaLayout breadcrumb="Perfil"><section class="panel"><h1>Mi perfil</h1><div class="grid grid-2"><div><p><b>Nombre:</b> {{ currentRole === 'Estudiante' ? 'Juan Pérez' : 'María Becerra' }}</p><p><b>Correo electrónico:</b> {{ currentRole === 'Estudiante' ? 'juan.perez@escuela.edu.ar' : 'maria.becerra@escuela.edu.ar' }}</p><p><b>Rol:</b> {{ currentRole }}</p><p><b>Teléfono:</b> 11 5555-1234</p></div><div class="notice"><b>Cuenta activa</b><p>{{ currentRole === 'Estudiante' ? 'Sólo podés consultar tus tutorías citadas.' : 'Tu perfil está habilitado para gestionar tutorías.' }}</p></div></div><div v-if="currentRole !== 'Estudiante'" class="actions"><button class="btn primary" @click="navigateView('editar-perfil')">Editar perfil</button><button class="btn soft" @click="navigateView('cambiar-contrasena')">Cambiar contraseña</button></div></section></SistemaLayout></template>




