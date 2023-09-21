<template>
    <div class="all">
        <img class="logo" src="../assets/logo.png" alt="">
        <h1>Sign Up</h1>
        <div class="register">
            <input type="text" name="" id="" v-model="name"  placeholder="Enter Name" required>
            <input type="email" name="" id=""  v-model="email"  placeholder="Enter email" required>
            <input type="password" name="" id=""  v-model="password"  placeholder="Enter password" required>
            <button @click="SignUp">SignUp</button>
            <p><b>Click Here To  <router-link to="/Login">Login</router-link></b>
                
            </p>
        </div>



    </div>
    
</template>
<script>
import axios from 'axios'
export default{
    name: 'SignUp',
    data(){
        return{
            name:'',
            email:'',
            password:''

        }
    },
    methods:{
        async SignUp(){
            let result =await axios.post("http://localhost:3000/user",{
                 name:this.name,
                email: this.email,
                password: this.password
            });
            console.log(result);
            if(result.status==201){
                // alert('signed Up')
                localStorage.setItem('userAuth',JSON.stringify(result.data))
                this.$router.push({name:'Home'})
            }
        }

    },
    mounted(){
        let user = localStorage.getItem('userAuth')
        if(user){
            this.$router.push({name:'Home'})
        }
    }
}
</script>
<style scoped>
.logo{
    width: 100px;
}
.all{
    text-align: center;
    font-size: 20px;
}
.register input{
    display: block;
    width: 300px;
    height: 40px;
    margin: 40px auto;
    padding-left: 20px;
    border: 1px solid skyblue;
    outline: none;
}
.register button{
    width: 300px;
    height: 40px;
    border: 1px solid skyblue;
    background:#67b9f5 ;
    color: white;
    cursor: pointer;


}

</style>