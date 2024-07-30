<script>
export default {
    props: {
        setCrypto: {
            type: Function,
            required: true,
        },
        cryptoNow: {
            type: String,
            required: true,
        }
    }
}
</script>

<template>
    <ul>
        <li @click="setCrypto('BTC')" :class="{ active: cryptoNow == 'BTC' }">BTC</li>
        <li @click="setCrypto('ETH')" :class="{ active: cryptoNow == 'ETH' }">ETH</li>
        <li @click="setCrypto('USDT')" :class="{ active: cryptoNow == 'USDT' }">USDT</li>
    </ul>
</template>


<style scoped>
ul {
    list-style: none;
    width: 200px;
    padding: 0;
    border-radius: 3px;
    border: 3px solid #000;
}

li {
    display: block;
    background: #1d0333;
    color: #fff;
    padding: 20px 0;
}

li:hover, li.active {
    background: #0b0213;
    cursor: pointer;
}
</style>
