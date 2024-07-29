<template>
    <div class="user">
        <button @click="deleteUser(index)" >Удалить</button>
        <h3>{{ user.name }}</h3>
        <p>{{ user.email }} - <b>{{ user.password }}</b> </p>
    </div>

</template>


<script>
export default {
    props: {
        user: {
            type: Object,
            required: true,
        },
        index: {
            type: Number,
            required: true,
        },
        deleteUser: {
            type: Function,
            required: true,
        }
    }
}
</script>


<style scoped>
.user {
    background-color: #ffffff;
    border: 1px solid #ddd;
    border-radius: 5px;
    padding: 15px;
    margin: 10px 0;
    width: 320px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

button {
    align-self: flex-end;
    padding: 5px 10px;
    border: none;
    border-radius: 5px;
    background-color: #ee0000;
    color: white;
    font-size: 14px;
    cursor: pointer;
    margin-bottom: 10px;
}

button:hover {
    background-color: #aa0000;
}

h3 {
    margin: 0;
    font-size: 18px;
    color: #333;
}

p {
    margin: 5px 0;
    font-size: 14px;
    color: #555;
}

p b {
    color: #333;
}
</style>
