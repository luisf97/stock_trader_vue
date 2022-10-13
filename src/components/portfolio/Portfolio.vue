<template>
    <v-main>
        <h1>Minhas Ações</h1>
        <v-layout row wrap>
            <Stock v-for="stock in stocks" :key="stock.id" :stock="stock" />
        </v-layout>
    </v-main>
    
</template>

<script>

import { mapGetters } from 'vuex'
import Stock from './Stock.vue'

export default {
    components: { Stock },
    computed: {
        ...mapGetters({
            stocks: 'stockPortfolio'
        })
    }
}
</script>

<style>

</style>