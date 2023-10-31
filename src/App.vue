<script setup lang="ts">
import { onMounted, ref, watch, watchEffect } from 'vue';
import Searchbar from './Searchbar.vue';
import User from './User.vue';
import UserModal from './UserModal.vue'
import { type UserType } from './types';

const usersData = ref(null as UserType[] | null)

let usersFetchController: AbortController | undefined
const fetchUsers = (searchQuery = '') => {
    // usersData.value = null
    usersFetchController?.abort()
    usersFetchController = new AbortController()
    const url = new URL('http://localhost:3000')
    if (searchQuery) {
        url.searchParams.set('term', searchQuery)
    }

    void fetch(url, { signal: usersFetchController.signal })
        .then(async res => res.json())
        .then(data => {
            usersData.value = data
        })
}

onMounted(() => {
    fetchUsers()
})

const searchValue = ref('')

watch(searchValue, (value) => {
    // users.value = initialUsers.filter(u => u.name.toLowerCase().includes(value.toLowerCase()))
    fetchUsers(value)
})

// usually modal state is managed globally
const activeUserModal = ref(null as UserType | null)

</script>
<template>
    <div class="app-root">
        <Searchbar v-model="searchValue" />
        <div v-if="usersData" class="users-container">
            <User v-for="item in usersData" :key="item.email" :data="item" @click="activeUserModal = item" />
        </div>
        <UserModal :is-open="activeUserModal !== null" :user="activeUserModal!" @update:is-open="activeUserModal = null" />
    </div>
</template>
<style scoped lang="scss">
.app-root {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 0 80px;
    margin-top: 64px;
}

.users-container {
    margin-top: 32px;
    display: flex;
    flex-wrap: wrap;
    /* justify-content: space-between; */
    gap: 24px 25px;
}
</style>
<style lang="scss">
body {
    margin: 0;
    padding: 0;
    font-family: Proxima Nova, sans-serif;
    /* background-color: #f5f5f5; */
    color: #262C40;
}

h1,
h2,
h3,
h4,
h5,
h6 {
    margin: 0;
}

* {
    box-sizing: border-box;
}
</style>
