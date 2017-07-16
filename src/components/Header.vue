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
                            <a href="#">End Day</a>
                        </li>
                        <li>
                            <a href="#">Save Data</a>
                        </li>
                        <li>
                            <a href="#">Load Data</a>
                        </li>
                        <!--<li role="presentation" class="dropdown">
                            <a class="dropdown-toggle" data-toggle="dropdown" href="#" role="button" aria-haspopup="true" aria-expanded="false">Save or Load
                                <span class="caret"></span>
                            </a>
                            <ul class="dropdown-menu">
                                <li>
                                    <a href="#">Save Data</a>
                                </li>
                                <li>
                                    <a href="#">Load Data</a>
                                </li>
                            </ul>
                        </li>-->
                    </ul>
                </div>
            </div>
        </nav>
    </div>
</template>

<script>
export default {
    computed: {
        funds() {
            return this.$store.getters.funds;
        }
    }
}
</script>

