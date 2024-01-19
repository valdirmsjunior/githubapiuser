<script setup>
    import { reactive, ref } from "vue"
    import { useSearchHistoryStore } from '../stores/useSearchHistoryStore';

    const emit = defineEmits(['formSubmit', 'update:modelValue'])
    const searchInput = ref('')

    const searchHistory = useSearchHistoryStore()
    
    function handleSubmit(ev) {
        ev.preventDefault();
        searchHistory.pushToHistory(searchInput.value)
        emit('formSubmit', searchInput.value);
    }

    function showSearchHistory() {
        alert(`Histórico de Pesquisa: \n${searchHistory.users.join('\n')}`)
    }
</script>

<template>
    <form @submit="handleSubmit">
        <input type="text" v-model="searchInput"
            @input="$emit('update:modelValue', $event.target.value)"
        />

        <button>Carregar Usuário</button>
        <button type="button" @click="showSearchHistory">Ver Histórico</button>
    </form>
</template>