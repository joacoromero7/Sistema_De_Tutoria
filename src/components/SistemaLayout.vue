<script setup>
defineProps({
  title: { type: String, default: 'Sistema de Tutorías' },
  breadcrumb: { type: String, default: '' },
  user: { type: String, default: 'Nombre de usuario' },
  role: { type: String, default: 'Profesor/a' },
  showSidebar: { type: Boolean, default: true },
})
</script>

<template>
  <div class="app-shell">
    <header class="topbar">
      <div class="brand">{{ title }}</div>
      <div class="account"><span>{{ user }}</span><small>{{ role }}</small><button class="icon-btn" aria-label="Notificaciones">🔔</button><button class="avatar">◯</button></div>
    </header>
    <div class="workspace">
      <aside v-if="showSidebar" class="sidebar">
        <h3>Cursos</h3><button class="course active">⑤ 5to año</button><button class="course">③ 3er año</button><button class="session">◉ Cerrar sesión</button>
      </aside>
      <main class="content"><div v-if="breadcrumb" class="breadcrumb">{{ breadcrumb }}</div><slot /></main>
    </div>
  </div>
</template>

<style>
:root { font-family: Inter, ui-sans-serif, system-ui, sans-serif; color: #253238; background: #f7f8fb; }
* { box-sizing: border-box; } button, input, select, textarea { font: inherit; } button { cursor: pointer; }
.app-shell { min-height: 100vh; background: #fafbfc; }.topbar { min-height: 76px; padding: 16px 28px; display:flex; align-items:center; justify-content:space-between; border-bottom:1px solid #d7dce2; background:#fff; }.brand { font-size:clamp(1.35rem,3vw,2rem); font-weight:800; letter-spacing:-.03em; }.account { display:flex; align-items:center; gap:12px; text-align:right; }.account span { font-weight:700; display:block; }.account small { display:block; color:#66727b; margin-left:auto; }.icon-btn,.avatar { border:0; background:transparent; font-size:1.35rem; }.avatar { font-size:1.8rem; }
.workspace { display:grid; grid-template-columns:235px 1fr; min-height:calc(100vh - 76px); }.sidebar { position:relative; border-right:1px solid #d7dce2; background:#fff; padding:20px 0; display:flex; flex-direction:column; }.sidebar h3 { margin:0 22px 10px; font-size:.95rem; text-transform:uppercase; letter-spacing:.08em; color:#68727a; }.course,.session { text-align:left; border:0; border-bottom:1px solid #e4e8ec; background:transparent; padding:14px 22px; font-weight:700; color:#3d4850; }.course.active { background:#e4ddf2; }.session { margin-top:auto; border-top:1px solid #e4e8ec; border-bottom:0; background:#e4ddf2; }
.content { padding:26px clamp(20px,4vw,56px); overflow:auto; }.breadcrumb { color:#65717a; font-size:.95rem; margin-bottom:18px; }.panel { background:#fff; border:1px solid #d9dfe4; border-radius:18px; padding:24px; box-shadow:0 8px 24px rgba(31,45,61,.05); }.panel h1,.panel h2 { margin:0 0 18px; }.muted { color:#6a757d; }.grid { display:grid; gap:18px; }.grid-2 { grid-template-columns:repeat(2,minmax(0,1fr)); }.grid-3 { grid-template-columns:repeat(3,minmax(0,1fr)); }.card { border:1px solid #d8dde2; border-radius:14px; overflow:hidden; background:#fff; }.card-head { height:76px; background:#70a0cc; }.card-head.red { background:#cc7b6f; }.card-body { padding:16px; }.card h3 { margin:0 0 6px; }.card p { margin:0 0 15px; color:#65717a; }
.actions { display:flex; gap:10px; flex-wrap:wrap; margin-top:20px; }.btn { border:1px solid #a9b4bc; border-radius:10px; padding:10px 16px; background:#fff; font-weight:700; }.btn.primary { background:#6b91c2; color:#fff; border-color:#6b91c2; }.btn.success { background:#b9d878; border-color:#9ebb5c; }.btn.danger { background:#dc8b80; border-color:#cf7166; }.btn.soft { background:#e7ddf2; border-color:#cdbde2; }
label { display:grid; gap:7px; font-weight:700; color:#40505a; } input,select,textarea { width:100%; border:1px solid #c8d0d6; border-radius:9px; padding:11px 12px; background:#fff; } textarea { min-height:100px; resize:vertical; }.form { max-width:760px; display:grid; gap:16px; }.form-row { display:grid; grid-template-columns:repeat(2,minmax(0,1fr)); gap:16px; }.notice { padding:14px 16px; border-radius:12px; background:#edf4d9; color:#4e6127; }.warning { background:#fff3d5; color:#795c1f; }.table { width:100%; border-collapse:collapse; }.table th,.table td { text-align:left; padding:13px 10px; border-bottom:1px solid #e1e5e8; }.table th { color:#68737b; font-size:.85rem; text-transform:uppercase; }.status { display:inline-flex; padding:5px 9px; border-radius:999px; background:#e4f0c9; color:#567026; font-size:.83rem; font-weight:700; }
@media (max-width:800px) { .workspace { grid-template-columns:1fr; }.sidebar { min-height:auto; }.session { margin-top:16px; }.grid-2,.grid-3,.form-row { grid-template-columns:1fr; }.topbar { align-items:flex-start; gap:12px; flex-direction:column; }.account { align-self:stretch; justify-content:flex-end; } }
</style>
