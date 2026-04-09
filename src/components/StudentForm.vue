<template>
  <div class="form-card">
    <h2 class="form-title">Registro de Estudiante</h2>
    <div class="form-grid">
      <div class="field">
        <label for="nombre">Nombre</label>
        <input
          id="nombre"
          v-model="form.nombre"
          type="text"
          placeholder="Ej. María"
          :class="{ error: errors.nombre }"
        />
        <span v-if="errors.nombre" class="error-msg">Campo requerido</span>
      </div>

      <div class="field">
        <label for="apellido">Apellido</label>
        <input
          id="apellido"
          v-model="form.apellido"
          type="text"
          placeholder="Ej. González"
          :class="{ error: errors.apellido }"
        />
        <span v-if="errors.apellido" class="error-msg">Campo requerido</span>
      </div>

      <div class="field full">
        <label>Género</label>
        <div class="radio-group">
          <label class="radio-label" v-for="g in generos" :key="g.value">
            <input type="radio" v-model="form.genero" :value="g.value" />
            <span class="radio-custom"></span>
            {{ g.label }}
          </label>
        </div>
        <span v-if="errors.genero" class="error-msg">Selecciona un género</span>
      </div>

      <div class="field full">
        <label for="carrera">Carrera</label>
        <select
          id="carrera"
          v-model="form.carrera"
          :class="{ error: errors.carrera }"
        >
          <option value="" disabled>Selecciona tu carrera...</option>
          <option v-for="c in carreras" :key="c" :value="c">{{ c }}</option>
        </select>
        <span v-if="errors.carrera" class="error-msg">Selecciona una carrera</span>
      </div>
    </div>

    <button class="btn-submit" @click="handleSubmit">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
        <path d="M12 5v14M5 12l7 7 7-7"/>
      </svg>
      Agregar Registro
    </button>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

const emit = defineEmits(['add-record'])

const form = reactive({
  nombre: '',
  apellido: '',
  genero: '',
  carrera: ''
})

const errors = reactive({
  nombre: false,
  apellido: false,
  genero: false,
  carrera: false
})

const generos = [
  { value: 'Masculino', label: 'Masculino' },
  { value: 'Femenino', label: 'Femenino' },
]

const carreras = [
  'Ingenieria de Software',
  'Ingeniería Informática',
  'Ingeniería Civil',
  'Medicina',
  'Derecho',
  'Enfermeria'
]

function validate() {
  errors.nombre = !form.nombre.trim()
  errors.apellido = !form.apellido.trim()
  errors.genero = !form.genero
  errors.carrera = !form.carrera
  return !Object.values(errors).some(Boolean)
}

function handleSubmit() {
  if (!validate()) return
  emit('add-record', { ...form })
  form.nombre = ''
  form.apellido = ''
  form.genero = ''
  form.carrera = ''
}
</script>

<style scoped>
.form-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 2rem 2.5rem;
  box-shadow: var(--shadow);
}

.form-title {
  font-family: 'DM Serif Display', serif;
  font-size: 1.4rem;
  color: var(--text);
  margin-bottom: 1.5rem;
  padding-bottom: 0.75rem;
  border-bottom: 2px solid var(--accent);
  display: inline-block;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.25rem;
  margin-bottom: 1.5rem;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.field.full {
  grid-column: 1 / -1;
}

label {
  font-size: 0.8rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: var(--text-muted);
}

input[type="text"],
select {
  padding: 0.6rem 0.85rem;
  border: 1.5px solid var(--border-dark);
  border-radius: var(--radius);
  font-family: 'DM Sans', sans-serif;
  font-size: 0.95rem;
  color: var(--text);
  background: var(--bg);
  transition: border-color 0.2s, box-shadow 0.2s;
  outline: none;
}

input[type="text"]:focus,
select:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px rgba(192, 57, 43, 0.1);
  background: #fff;
}

input.error, select.error {
  border-color: #e74c3c;
}

.error-msg {
  font-size: 0.75rem;
  color: var(--accent-light);
  font-weight: 500;
}

.radio-group {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap;
  padding: 0.5rem 0;
}

.radio-label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.95rem;
  font-weight: 400;
  text-transform: none;
  letter-spacing: 0;
  color: var(--text);
  cursor: pointer;
}

.radio-label input[type="radio"] {
  display: none;
}

.radio-custom {
  width: 18px;
  height: 18px;
  border: 2px solid var(--border-dark);
  border-radius: 50%;
  display: inline-block;
  position: relative;
  transition: border-color 0.2s;
  flex-shrink: 0;
}

.radio-label input[type="radio"]:checked + .radio-custom {
  border-color: var(--accent);
}

.radio-label input[type="radio"]:checked + .radio-custom::after {
  content: '';
  position: absolute;
  top: 3px;
  left: 3px;
  width: 8px;
  height: 8px;
  background: var(--accent);
  border-radius: 50%;
}

.btn-submit {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: var(--accent);
  color: white;
  border: none;
  padding: 0.7rem 1.5rem;
  border-radius: var(--radius);
  font-family: 'DM Sans', sans-serif;
  font-size: 0.9rem;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s, transform 0.15s;
  letter-spacing: 0.03em;
}

.btn-submit:hover {
  background: var(--accent-light);
  transform: translateY(-1px);
}

.btn-submit:active {
  transform: translateY(0);
}

@media (max-width: 560px) {
  .form-grid { grid-template-columns: 1fr; }
  .form-card { padding: 1.5rem; }
}
</style>
