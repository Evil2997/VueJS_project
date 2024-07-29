<template>
  <input type="text" v-model="userName" placeholder="Имя">
  <input type="password" v-model="userPassword" placeholder="Пароль">
  <input type="email" v-model="userEmail" placeholder="Email">

  <p class="error">{{ error }}</p>

  <button @click="sendData()">{{ registory }}</button>
  <div v-if="users.length == 0"><b>{{ registory_message }}</b></div>

  <User v-for="(el, index) in users" :key="index" class="user" :user="el" :index="index" :deleteUser="deleteUser" />
</template>

<script>
import User from './components/User.vue'

export default {
  components: { User },
  data() {
    return {
      users: [],
      error: "",
      userName: "",
      userPassword: "",
      userEmail: "",

      registory: "Зарегестрировать",
      registory_message: "У вас нет пользователей",

    }
  },  
  methods: {
    sendData() {
        if(this.userName=="") {
          this.error = "Имя не введено";
          return;
        }
        else if(this.userPassword=="") {
          this.error = "Пароль не введен";
          return;
        }
        else if(this.userEmail=="") {
          this.error = "Email не введен";
          return;
        }
        this.error = ""
        this.users.push({
          name: this.userName,
          password: this.userPassword,
          email: this.userEmail,
        })
    },
    deleteUser(index) {
      this.users.splice(index, 1)
    }
  }
}
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  background-color: #f7f9fc;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  margin: 0;
}

input[type="text"],
input[type="password"],
input[type="email"] {
  display: block;
  width: 300px;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-sizing: border-box;
}

button {
  display: block;
  width: 320px;
  padding: 10px;
  margin-top: 20px;
  border: none;
  border-radius: 5px;
  background-color: #007BFF;
  color: white;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.error {
  color: red;
  font-weight: bold;
  margin-top: 10px;
}

.user {
  background-color: #ffffff;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 10px;
  margin-top: 10px;
  width: 320px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h3 {
  margin: 0;
  font-size: 18px;
}

p {
  margin: 5px 0;
  font-size: 14px;
  color: #333;
}

p b {
  color: #555;
}

div {
  margin-top: 20px;
  font-size: 16px;
  color: #333;
}
</style>
