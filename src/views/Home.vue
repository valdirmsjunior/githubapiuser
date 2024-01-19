
<script setup>
    import { useSearchHistoryStore } from "@/stores/useSearchHistoryStore";

    const searchHistory = useSearchHistoryStore()
</script>
<template>

    <h1>Bem-Vindo</h1>        
    <p>Essa é a página inicial do App.</p>

    <section>
        <h2>Historico de Pesquisa:</h2>
        <p v-for="user in searchHistory.users" :key="user">{{ user }}</p>
    </section>

</template>

<style scoped>
section {
    margin: 1rem 0;
}
p {
    margin-top: 1rem;
}
</style>