<template>
    <div class="col-sm-7 col-md-5">
        <div class="panel panel-info">
            <div class="panel-heading">
                <h3 class="panel-title">{{ stock.name }}
                    <small>(Price: {{ stock.price }} | Quantity: {{ stock.quantity}})</small>
                </h3>
            </div>
            <div class="panel-body">
                <div class="pull-left">
                    <input type="number" 
                    class="form-control" 
                    placeholder="Quantity" 
                    :class="{danger: insufficientQuantity}"
                    v-model="quantity">
                </div>
                <div class="pull-right">
                    <button class="btn btn-success" @click="sellStock" 
                    v-bind:disabled="quantity <= 0|| insufficientQuantity">
                    {{ insufficientQuantity? 'No Enough stocks': 'Sell' }}</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { mapActions } from 'vuex';
export default {
    props: ['stock'],

    data() {
        return {
            quantity: 0
        }
    },
    computed: {
        insufficientQuantity() {
            return this.quantity > this.stock.quantity;
        }
    },
    methods: {
        ...mapActions({
            placeSellOrder: 'sellStock'
        }),

        sellStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            };
            this.placeSellOrder(order);
            this.quantity = 0;
        }
    }
}
</script>

<style scoped>
    .danger {
        border: 1px solid red;
    }
</style>


