<template>
<div>
  <h1>Trade or view you Portfolio</h1>
<p> Your Funds: {{ funds | currency}}</p>
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

