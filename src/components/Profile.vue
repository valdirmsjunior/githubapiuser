<script setup>
    import { computed, reactive, ref } from 'vue';
    import UserInfo from './UserInfo.vue';
    import Repository from './Repository.vue';
    import Form from './Form.vue';

    const username = ref('')

    const state = reactive({
        login: '',
        name: '',
        bio: '',
        company: '',
        avatar_url: '',
        repos: []
    })

    async function fetchGithubUser(searchInput) {
        const res = await fetch(`http://api.github.com/users/${searchInput}`)
        const { login, name, bio, company, avatar_url } = await res.json()

        state.login = login
        state.name = name
        state.bio = bio
        state.company = company
        state.avatar_url = avatar_url

        fetchUserRepositories(login)
    }

    async function fetchUserRepositories(username) {
        const res = await fetch(`https://api.github.com/users/${username}/repos`)
        const repos = await res.json()

        state.repos = repos
    }

    const reposCountMessage = computed(() => {
        return state.repos.length > 0
            ? `${state.name} possui ${state.repos.length} repositorios publicos`
            : `${state.name} não possui nenhum repositorio publico`
    })
</script>

<!-- v-on: ou @ serve para chamar os eventos javascript */
/** v-bind poder ser substituido apenas por : (forma mais comum) -->

<template>
	<slot></slot>
    <p>Pesquisando por: <strong>https://api.github.com/users/{{ username }}</strong></p>
    
    <Form @form-submit="fetchGithubUser" v-model="username" />

    <div v-if="state.login !== ''">
        <UserInfo :login="state.login" 
            :name="state.name" 
            :company="state.company" 
            :bio="state.bio" 
            :avatar_url="state.avatar_url"
        />
    </div>

    <section v-if="state.repos.length > 0">
        <h2>{{ reposCountMessage }}</h2>
        <article v-for="repo of state.repos" :key="repo.name">
            <Repository :full_name="repo.full_name"
                :description="repo.description"
                :html_url="repo.html_url" />
        </article>
    </section>
    
    <slot name="footer"></slot>
</template>