<template>
    <div class="total-value">Balance: {{ total }}</div>
</template>

<script>
export default {
    name: 'TotalBalance',
    props: {
        total: {
            type: Number,
            default: 0
        }
    }
}
</script>

<style scoped>
    .total-value {
        font-style: 26px;
        font-weight: bold;
        text-transform: uppercase;
        padding: 20px;
        text-align: center;
    }
    

</style>
