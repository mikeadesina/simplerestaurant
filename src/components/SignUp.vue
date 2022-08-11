<template>
    <img  class="logo" alt="Vue logo" src="../assets/logo.png" />
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Enter Name" />
        <input type="text" v-model="email" placeholder="Enter Email" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button v-on:click="signUp"> Sign Up</button>
        <p><router-link to="/login">Login</router-link></p>
    </div>
</template>
<script>
    import axios from 'axios';
    export default {
    name: "SignUp",
    data(){
        return {
            name:'',
            email:'',
            password:''
        }
    },
    methods:{
        async signUp(){
           let result=await axios.post("http://localhost:3000/user",{
            name:this.name,
            email:this.email,
            password:this.password
           });
           if(result.status==201){
            console.log(result);
             //alert('successful')
             localStorage.setItem('user-info',JSON.stringify(result.data))
             this.$router.push({name:'Home'})
           }else{
            alert('not successful')
            console.log(result);
           }
        }
    },
    mounted(){
        let users=localStorage.getItem('user-info');
        if(users){
           this.$router.push({name:'Home'}) 
        }
    }

    };
</script>
<style scoped>
    .logo {
    width: 100px;
    }
    .register input{
        width:300px;
        height: 40px;
        padding-left: 20px;
        display: block;
        margin-bottom: 30px;
        margin-right: auto;
        margin-left: auto;
        border: 1px solid skyblue;
    }
    .register button{
        width:300px;
        height: 40px;
        border: 1px solid skyblue;
        background:skyblue;
        color:#fff;
        cursor: pointer;
    }
</style>
