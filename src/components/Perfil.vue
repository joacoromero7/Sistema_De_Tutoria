<script setup>
import { inject } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
</script>
<template><SistemaLayout breadcrumb="Perfil"><section class="panel"><h1>Mi perfil</h1><div class="grid grid-2"><div><p><b>Nombre:</b> María Becerra</p><p><b>Correo electrónico:</b> maria.becerra@escuela.edu.ar</p><p><b>Rol:</b> Profesor/a</p><p><b>Teléfono:</b> 11 5555-1234</p></div><div class="notice"><b>Cuenta activa</b><p>Tu perfil está habilitado para gestionar tutorías.</p></div></div><div class="actions"><button class="btn primary" @click="navigateView('editar-perfil')">Editar perfil</button><button class="btn soft" @click="navigateView('cambiar-contrasena')">Cambiar contraseña</button></div></section></SistemaLayout></template>




