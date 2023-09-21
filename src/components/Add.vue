<template>
    <div class="all">
      <Header></Header>
      <h1>Hello {{ name }},Welcome to Add Resturant Page</h1>;
      <form class="register">
            <input type="text"  v-model="resturant.name"  placeholder="Enter Name" required>
            <input type="text" v-model="resturant.contact"  placeholder="Enter contact" required>
            <input type="text"  v-model="resturant.address"  placeholder="Enter Address" required>
            <button type="button" @click="addResturant">Add Resturant</button>
      </form>
    </div>
  </template>
  
  <script>
  import Header from '../components/Header.vue'
  import axios from 'axios'
  export default {
    name:'Add',
    components:{
      Header,
    },
    data(){
        return{
            name:'',
            resturant:{
                name:"",
                contact:"",
                address:""
            }
        }
    },
    methods:{
       async addResturant(){
            const result=   await axios.post("http://localhost:3000/resturant",{
                name:this.resturant.name,
                contact:this.resturant.contact,
                address:this.resturant.address,
            });
            if(result.status==201){
              this.$router.push({name:'Home'})
            }
            console.log(result);
        }

    },
    mounted(){
          let user = localStorage.getItem('userAuth');
        this.name =JSON.parse(user).name;
          if(!user){
              this.$router.push({name:'SignUp'})
          }
      }
  
  }
  </script>
  
  <style scoped>
  .all{
      text-align: center;
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