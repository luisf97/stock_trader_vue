<template>
    <v-toolbar app xs12 md6 lg4>
        <v-toolbar-title class="headline text-uppercase mr-4">
            <span>Stock</span>
            <span class="font-weight-light">Trading</span>
        </v-toolbar-title>
        <v-toolbar-items>
        <v-btn flat to="/">Início</v-btn>
            <v-menu offset-y>
                <v-btn flat slot="activator">Ações</v-btn>
                <v-list>
                    <v-list-tile flat to="/portfolio">
                        <v-list-tile-title>Minhas Ações</v-list-tile-title>
                    </v-list-tile>
                    <v-list-tile flat to="/stocks">
                        <v-list-tile-title>Comprar Ações</v-list-tile-title>
                    </v-list-tile>
                </v-list>
            </v-menu>
        </v-toolbar-items>

        <v-toolbar-items>
            <v-btn flat to="/usuarios">Usuários</v-btn>
        </v-toolbar-items>

        <v-spacer></v-spacer>

        <v-toolbar-items>
            <v-btn @click="endDay" flat>Finalizar Dia</v-btn>
            <v-menu offset-y>
                <v-btn flat slot="activator">Salvar & Carregar</v-btn>
                <v-list>
                    <v-list-tile @click="saveData">
                        <v-list-tile-title>Salvar dados</v-list-tile-title>
                    </v-list-tile>
                    <v-list-tile @click="loadDataLocal">
                        <v-list-tile-title>Carregar Dados</v-list-tile-title>
                    </v-list-tile>
                </v-list>
            </v-menu>
            <v-layout align-center>
                <span class="text-uppercase grey--text text-darken-2">
                    Saldo: {{ funds | currency }}
                </span>
            </v-layout>
        </v-toolbar-items>
    </v-toolbar>
</template>

<script>

import { mapActions } from 'vuex'

export default {

    computed: {
        funds() {
            return this.$store.getters.funds
        }
    },
    methods: {
        ...mapActions(['randomizeStocks', 'loadData']),
        endDay() {
            this.randomizeStocks()
        },
        saveData() {
            const { funds, stockPortfolio, stocks } = this.$store.getters

            this.$http.put('/data.json', { funds, stockPortfolio, stocks })
        },
        loadDataLocal() {
            this.loadData()
        }
    }
}
</script>

<style>

</style>