<template>
    <v-app>
        <div v-for="user in users" :key="user.id">
            {{ user.name }} 
        </div>
        
    </v-app>
</template>

<script>

import axios from 'axios'

export default {
    data() {
        return {
            users: [
                { id: 1, name: 'Luís', birthdate: '03/06/1997', email: 'luis@gmail.com', isAdmin: true},
                { id: 2, name: 'Lucas', birthdate: '23/10/1996', email: 'lucas@gmail.com', isAdmin: false},
                { id: 3, name: 'Anderson', birthdate: '19/08/1995', email: 'anderson@gmail.com', isAdmin: false}
            ]
        }
    },
    methods: {
        getUsers() {
            axios.get('http://localhost:8081/users').then(({ data }) => {
                this.users = data
            })
        }
    }
}
</script>

<style>

</style>