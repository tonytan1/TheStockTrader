<template>
    <div>
        <nav class="navbar navbar-default">
            <div class="container-fluid">
                <!-- Brand and toggle get grouped for better mobile display -->
                <div class="navbar-header">
                    <router-link to="/" class="navbar-brand">Stock Trader</router-link>
                </div>
    
                <div class="collapse navbar-collapse">
                    <ul class="nav navbar-nav">
                        <router-link to="/portfolio" active-class="active" tag="li">
                            <a>Portfolio</a>
                        </router-link>
                        <router-link to="/stocks" active-class="active" tag="li">
                            <a>Stocks</a>
                        </router-link>
                    </ul>
                    <strong class="navbar-text navbar-right">
                        Funds: {{ funds | currency}}
                    </strong>
                    <ul class="nav navbar-nav navbar-right">
                        <li>
                            <a href="#" @click="endDay">End Day</a>
                        </li>
                        <li role="presentation" class="dropdown" :class="{open: isDropdown}" @click="isDropdown = !isDropdown">
                            <a class="dropdown-toggle" data-toggle="dropdown" href="#" role="button" aria-haspopup="true" aria-expanded="false">Save or Load
                                <span class="caret"></span>
                            </a>
                            <ul class="dropdown-menu">
                                <li>
                                    <a href="#" @click="saveData">Save Data</a>
                                </li>
                                <li>
                                    <a href="#" @click="loadData">Load Data</a>
                                </li>
                            </ul>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
    </div>
</template>

<script>

import { mapActions } from 'vuex';

export default {
    data() {
        return {
            isDropdown: false
        }
    },

    computed: {
        funds() {
            return this.$store.getters.funds;
        }
    },

    methods: {
        ...mapActions({
            'endDay': 'randomizeStocks'
        }),

        endDay() {
            this.endDay;
        },

        saveData() {
            const data = {
                funds: this.$store.getters.funds,
                stockPortfolio: this.$store.getters.stockPortfolio,
                stocks: this.$store.getters.stocks
            };
            this.$http.put('data.json', data);
        },

        loadData() {
            this.$store.dispatch('loadData');
        }
    }
}
</script>

