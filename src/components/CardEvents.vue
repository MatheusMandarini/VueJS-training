<script setup>
    import { defineProps } from 'vue'
    function formartDate(date){
        return date.split('-').reverse().join('/')
    }
    defineProps({
        evento: Object
    })
    
</script>
<template>
    <article>
        <div>title: {{ evento.titulo }}</div>
        <div>date: {{ formartDate(evento.data) }}</div>
        <div>location: {{ evento.local }}</div>
        <div>category: {{ evento.categoria }}</div>
        <hr/>
    </article>
</template>
<style scoped>

</style>