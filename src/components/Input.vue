<script>
export default {
    props: {
        changeAmount: {
            type: Function,
            requiret: true,
        },
        convert: {
            type: Function,
            requiret: true,
        },
        favorite: {
            type: Function,
            requiret: true,
        }
    }
}
</script>

<template>
    <input type="number" min=0 @input="changeAmount($event.target.value)" placeholder="Введите число"><br>
    <button @click="convert()" >Конвертировать</button>
    <button @click="favorite()" class="fav-buttom">В избранное</button>
</template>


<style scoped>
input {
    width: 500px;
    position: relative;
    top: -20px;
    font-size: 1.2em;
    outline: none;
    border-radius: 3px;
    border: 0;
    padding: 10px 15px;
    background: #fafafa;
    color: #333
}
button {
    position: relative;
    top: -10px;
    padding: 15px 20px;
    text-transform: uppercase;
    color: #f3f3f3f3;
    cursor: pointer;
    background: #210542;
    border: 0;
    border-radius: 8px;
}
.fav-buttom {
    margin-left: 20px;
}
</style>
