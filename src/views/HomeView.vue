<script setup>
  import CardEvents from '../components/CardEvents.vue'
  import { onMounted, ref, computed } from 'vue'
  const carregando = ref(true)
  const mensagemErro = ref('')
  const eventos = ref([])

  onMounted(async () =>{
    try{
      const response = await fetch('http://localhost:3000/eventos')
      if(!response.ok){
        throw new Error('Erro ao buscar eventos')
      }
      const data = await response.json()
      eventos.value = data
      
    } catch (error) {
      mensagemErro.value = 'Erro ao buscar eventos'
    }finally{
      carregando.value = false
    }
  })
  
  const computedEventos = computed(() => {
    const copia = [...eventos.value]
    return copia.sort((a, b) => new Date(a.data) - new Date(b.data))
  });

</script>
  
<template>
  <p v-if="carregando">carregando eventos...</p>
  <div v-else-if="mensagemErro">{{ mensagemErro }}</div> 
  <div v-else>
    <CardEvents v-for="evento in computedEventos" :key="evento.id" :evento="evento"/>
  </div>
</template>

<style scoped>

</style>