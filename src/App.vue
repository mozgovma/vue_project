
<template>
    <input type="text" v-model="userName" placeholder="Имя">
    <input type="password" v-model="userPass" placeholder="Пароль">
    <input type="email" v-model="userEmail" placeholder="Email">
    <p className="error"></p>
    <button @click="sendData()">Отправить</button>
    <div v-if="users.length == 0" className="user">
      На данный момент не внесенно ни одного пользователя
    </div>
    <div v-else-if="users.length > 0" className="user">
      На данный момент в список внесенно {{ users.length }} пользователей
    </div>
    <User v-for="(el, index) in users" :key="index" :user="el" :index="index" :deleteUser="deleteUser" />
</template>

<script>

import User from './components/User.vue'

 export default {
  components: { User },
  data(){
    return{
      users: [],
      error:'',
      userName: '',
      userPass: '',
      userEmail: '',
    }
  },
  methods: {
    sendData(){
      if(this.userName =='' || this.userPass == '' || this.userEmail == ''){
        alert("Все поля должны быть заполнены");
        return;
      }

      this.users.push({
        name : this.userName,
        password: this.userPass,
        email: this.userEmail
      })
    },
    deleteUser(index){
      this.users.splice(index, 1);
    }
  }
 }
</script>

<style scoped>
  input{
    display: block;
    margin-bottom: 10px;
    border-radius: 3px;
    border: 1px solid silver;
    outline: none;
    padding: 10px 15px;
    background: #fafafa;
    color: #333;
  }
  button{
    border: 0;
    border-radius: 5px;
    outline: none;
    padding: 10px 15px;
    background: #6cd670;
    color: #167f3d;
    cursor: pointer;
    transition: transform 500ms ease;
  }
  button:hover{
    transform: translateY(-5px)
  }
  .user{
    width: 500px;
    margin-top: 20px;
    border: 1px solid silver;
    background-color: #e3e3e3;
    color:#222;
    padding: 50px;
    border-radius: 5px;
  }
</style>
