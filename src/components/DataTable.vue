<template>
  <div class="table-card">
    <div class="table-header">
      <h2 class="table-title">Registros Capturados</h2>
      <span class="badge">{{ records.length }} {{ records.length === 1 ? 'registro' : 'registros' }}</span>
    </div>

    <div v-if="records.length === 0" class="empty-state">
      <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" opacity="0.35">
        <rect x="3" y="3" width="18" height="18" rx="2"/>
        <path d="M9 9h6M9 13h4"/>
      </svg>
      <p>Aún no hay registros. Completa el formulario para agregar datos.</p>
    </div>

    <div v-else class="table-wrapper">
      <table>
        <thead>
          <tr>
            <th>#</th>
            <th>Nombre</th>
            <th>Apellido</th>
            <th>Género</th>
            <th>Carrera</th>
            <th>Acción</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(record, index) in records" :key="index" class="table-row">
            <td class="index-cell">{{ index + 1 }}</td>
            <td>{{ record.nombre }}</td>
            <td>{{ record.apellido }}</td>
            <td>
              <span class="gender-chip" :class="genderClass(record.genero)">
                {{ record.genero }}
              </span>
            </td>
            <td class="carrera-cell">{{ record.carrera }}</td>
            <td>
              <button class="btn-delete" @click="$emit('delete-record', index)" title="Eliminar">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
                  <path d="M18 6L6 18M6 6l12 12"/>
                </svg>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
defineProps({ records: Array })
defineEmits(['delete-record'])

function genderClass(genero) {
  if (genero === 'Masculino') return 'chip-m'
  if (genero === 'Femenino') return 'chip-f'
  return 'chip-n'
}
</script>

<style scoped>
.table-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  overflow: hidden;
}

.table-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1.5rem 2rem;
  border-bottom: 1px solid var(--border);
}

.table-title {
  font-family: 'DM Serif Display', serif;
  font-size: 1.4rem;
}

.badge {
  background: var(--accent);
  color: white;
  font-size: 0.75rem;
  font-weight: 700;
  padding: 0.25rem 0.75rem;
  border-radius: 999px;
  letter-spacing: 0.04em;
}

.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  padding: 3rem 2rem;
  color: var(--text-muted);
  text-align: center;
  font-size: 0.9rem;
}

.table-wrapper {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

thead tr {
  background: #f9f8f6;
}

th {
  text-align: left;
  padding: 0.65rem 1.25rem;
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.07em;
  color: var(--text-muted);
  border-bottom: 1px solid var(--border);
  white-space: nowrap;
}

td {
  padding: 0.8rem 1.25rem;
  border-bottom: 1px solid var(--border);
  font-size: 0.9rem;
  vertical-align: middle;
}

.table-row:last-child td {
  border-bottom: none;
}

.table-row:hover {
  background: #faf9f7;
}

.index-cell {
  color: var(--text-muted);
  font-weight: 600;
  font-size: 0.8rem;
}

.carrera-cell {
  max-width: 200px;
}

.gender-chip {
  display: inline-block;
  padding: 0.2rem 0.65rem;
  border-radius: 999px;
  font-size: 0.78rem;
  font-weight: 600;
}

.chip-m { background: #dbeafe; color: #1d4ed8; }
.chip-f { background: #fce7f3; color: #be185d; }
.chip-n { background: #f3f4f6; color: #4b5563; }

.btn-delete {
  background: none;
  border: 1.5px solid #e0ddd8;
  color: #9ca3af;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-delete:hover {
  border-color: var(--accent-light);
  color: var(--accent-light);
  background: #fff5f5;
}
</style>
