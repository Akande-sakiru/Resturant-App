<template>
   <div class="all">
        <img class="logo" src="../assets/logo.png" alt="">
        <h1>Login</h1>
        <div class="register">
            <input type="email" name="" id=""  v-model="email"  placeholder="Enter email" required>
            <input type="password" name="" id=""  v-model="password"  placeholder="Enter password" required>
            <button @click="Login">Login</button>
            <p><b>Click Here To <router-link to="/sign-up">SignUp</router-link> </b>
                
            </p>
        </div>



    </div>
</template>

<script>
import axios from 'axios'
export default {
    name:'Login',
    data(){
        return{
            email:'',
            password:''
        }
    },
    methods:{
        async Login(){
            let result = await axios.get(`http://localhost:3000/user?email=${this.email}&password=${this.password}`);
            console.log(result);
            if(result.status==200 && result.data.length>0){
                localStorage.setItem('userAuth',JSON.stringify(result.data[0]))
                this.$router.push({name:'Home'})
            }
            else{
                alert('Details not found.........please sign up')
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