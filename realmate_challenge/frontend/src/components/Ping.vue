<template>
  <div>
    <h2>Ping Teste</h2>
    <button @click="fetchPing">Testar /ping</button>
    <p v-if="response">Resposta: {{ response }}</p>
    <p v-if="error" style="color:red">Erro: {{ error }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const response = ref('')
const error = ref('')

function getBackendUrl() {
  if (window.location.hostname === 'localhost' || window.location.hostname === '127.0.0.1') {
    return 'http://localhost:80/ping'
  } else {
    return 'http://backend/ping'
  }
}

async function fetchPing() {
  response.value = ''
  error.value = ''
  try {
    const res = await fetch(getBackendUrl())
    if (!res.ok) throw new Error('Erro na requisição')
    response.value = await res.text()
  } catch (e) {
    error.value = e.message
  }
}
</script>
