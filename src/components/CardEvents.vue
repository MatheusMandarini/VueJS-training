<script setup>
    import { defineProps } from 'vue'

    defineProps({
        titulo: String,
        data: String,
        local: String,
        categoria: String
    })
    data.split('-').reverse().join('/')

</script>
<template>
    <article>
        <div>title: {{ titulo }}</div>
        <div>date: {{ data }}</div>
        <div>location: {{ local }}</div>
        <div>category: {{ categoria }}</div>

    </article>
</template>
<style scoped>

</style>