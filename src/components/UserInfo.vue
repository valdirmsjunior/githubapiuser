<script setup>
    defineProps(['login', 'name', 'company', 'bio', 'avatar_url'])
</script>

<template>
    <img :src="avatar_url">
    <strong>@{{ login }}</strong>
    <h2>{{ name }}</h2>
    <h3>{{ company }}</h3>
    <span>{{ bio }}</span>
</template>