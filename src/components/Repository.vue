<script setup>
    defineProps(['full_name', 'description', 'html_url'])
</script>

<template>
    <h3>{{ full_name }}</h3>
    <p>{{ description }}</p>
    <a :href="html_url" target="_blank">Ver no GitHub</a>
</template>