<template>
  <div class="app-wrapper">
    <!--Header-->
    <header class="app-header">
      <div class="header-inner">
        <h1 class="app-title">
          Formulario interactivo
        </h1>
      </div>
    </header>

    <!--Main-->
    <main class="main-content">
      <div class="content-grid">
        <StudentForm @add-record="addRecord" />
        <DataTable :records="records" @delete-record="deleteRecord" />
      </div>
    </main>

    <footer class="app-footer">
      <p></p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import StudentForm from './components/StudentForm.vue'
import DataTable from './components/DataTable.vue'

const records = ref([])

function addRecord(record) {
  records.value.push(record)
}

function deleteRecord(index) {
  records.value.splice(index, 1)
}
</script>

<style scoped>
.app-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/*Header*/
.app-header {
  background: #1a1a2e;
  color: #fff;
  padding: 2rem 0 1.75rem;
  border-bottom: 3px solid #c0392b;
}

.header-inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 2rem;
}

.app-title {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(1.4rem, 3vw, 2rem);
  line-height: 1.25;
  margin-bottom: 0;
  color: #fff;
}

/*Main*/
.main-content {
  flex: 1;
  max-width: 1100px;
  width: 100%;
  margin: 0 auto;
  padding: 2.5rem 2rem;
}

.content-grid {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

/*Footer*/
.app-footer {
  text-align: center;
  padding: 1.25rem;
  font-size: 0.78rem;
  color: #aaa;
  border-top: 1px solid var(--border);
  background: #faf9f7;
}

@media (max-width: 640px) {
  .header-inner, .info-inner, .main-content { padding: 0 1rem; }
  .main-content { padding-top: 1.5rem; }
}
</style>
