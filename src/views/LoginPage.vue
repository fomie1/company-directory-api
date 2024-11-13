<template>
    <form class="m-10" @submit.prevent>
        <div>
            <label for="username" class="block mb-2 font-bold">Username</label>
            <input id="username" v-model="username" type="text" placeholder="Username">
        </div>
             <div>
            <label for="password" class="block mb-2 font-bold">Password</label>
            <input id="password" v-model="password" type="password" placeholder="Password">
        </div>

        <button @click="logUserIn" class="bg-green-500 mt-4 px-4 py-2 hover:bg-green-800 hover:text-white">LOGIN</button>

    </form>
</template>

<script setup>
import { ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'

import { useAuth } from '../composables/useAuth'

const { login, logout } = useAuth()

const router = useRouter()
const route = useRoute()

const username = ref('')
const password = ref('')

const logUserIn = async () => {
    if (await login(username.value, password.value)) {
        if (route.query.redirect) {
            router.push(route.query.redirect)
        } else {
            router.push({name: 'SettingsPage'})
        }
        
    } else {
        logout()
    }
    
}


</script>