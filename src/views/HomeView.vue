<script setup>
  import CardEvents from '../components/CardEvents.vue'
  import { onMounted, ref, computed } from 'vue'
  const carregando = ref(true)
  const mensagemErro = ref('')
  const eventos = ref([])
  const busca = ref('')
  const selecionada = ref('')

  onMounted(async () =>{
    try{
      const response = await fetch('/eventos.json')
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
    let copia = [...eventos.value]
    if (selecionada.value) {
        copia = copia.filter(evento =>
            evento.categoria === selecionada.value
        )
    }
    if (busca.value) {
        copia = copia.filter((evento) =>
            evento.titulo.toLowerCase().includes(busca.value.toLowerCase())
        )
    }
    return copia.sort((a, b) => new Date(a.data) - new Date(b.data))
  });

</script>
  
<template>
  <p v-if="carregando">carregando eventos...</p>
  <div v-else-if="mensagemErro">{{ mensagemErro }}</div> 
  <div v-else>
    <h1>Eventos</h1>  
    <label for="busque">Pesquise por eventos</label>
    <input type="text" id="busque" placeholder="Digite o nome do evento" v-model="busca"/>
    <select v-model="selecionada">
      <option value="">Todos</option>
      <option v-for="evento in eventos" :key="evento.id" :value="evento.categoria" multiple>{{ evento.categoria }}</option>
    </select>
    <hr/>
    
    <CardEvents v-for="evento in computedEventos" :key="evento.id" :evento="evento"/>
   
  </div>
</template>

<style scoped>

</style>