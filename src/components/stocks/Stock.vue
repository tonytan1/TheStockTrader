<template>
    <div class="col-sm-7 col-md-5">
        <div class="panel panel-success">
            <div class="panel-heading">
                <h3 class="panel-title">{{ stock.name }}
                    <small>(Price: {{ stock.price }})</small>
                </h3>
            </div>
            <div class="panel-body">
                <div class="pull-left">
                    <input type="number" class="form-control" v-model="quantity" 
                    :class="{ danger: insufficientFunds}">
                </div>
                <div class="pull-right">
                    <button class="btn btn-success" placeholder="Quantity" @click="buyStock" 
                    :disabled="parseInt(quantity)<=0 || insufficientFunds">
                    {{insufficientFunds? "Insufficient Funds": "Buy"}}</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {

    props: ['stock'],

    data() {
        return {
            quantity: 0
        }
    },
    computed: {
        funds() {
            return this.$store.getters.funds;
        },
        insufficientFunds() {
            return this.stock.price * this.quantity > this.funds;
        }
    },

    methods: {
        buyStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            };
            this.$store.dispatch('buyStock', order);
            this.quantity = 0;
        },

        validInput(input) {
            return parseInt(input) <= 0 || !Number.isInteger(input)
        }
    }
}
</script>

<style scoped>
    .danger {
        border: 1px solid red;
    }
</style>


