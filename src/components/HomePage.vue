<template>
  <div class="all">
    <Header></Header>
    <h1>Hello {{name}},Welcome to Home Page</h1>
    <div class="gap">
      <table class="table table-hover table-bordered">
    <tr>
      <th>Id</th>
      <th>Name</th>
      <th>Contact</th>
      <th>Address</th>
      <th>Actions</th>
    </tr>
    <tr v-for="item in resturant" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.contact }}</td>
      <td>{{ item.address }}</td>
      <td class="space">
        <router-link class="link" :to="'/Update/'+item.id">Update </router-link>
        <button class="btn btn-danger" type="button" @click="deleteid(item.id)">Delete</button>
      </td>
    </tr>
</table>
    </div>
  </div>
</template>

<script>
import Header from '../components/Header.vue'
import axios from 'axios'
export default {
  name:'HomePage',
  data(){
    return{
        name:'',
        resturant:[],
    }
  },
  components:{
    Header,
  },
  methods:{
     async deleteid(id){
        let result =await axios.delete("http://localhost:3000/resturant/" +id);
        console.log(result.status);
        if(result.status==200){
          this.loadData()
        }
      },
      async loadData(){
        let user = localStorage.getItem('userAuth')
        this.name =JSON.parse(user).name;
        if(!user){
            this.$router.push({name:'SignUp'})
        }
        let result =await axios.get("http://localhost:3000/resturant");
        console.log(result);
        this.resturant=result.data;
      }

  },
  async mounted(){
    this.loadData()
    }

}
</script>

<style scoped>
.all{
    text-align: center;
}
.gap{
  margin-top: 80px;
}
table,th,td{
  border: 1px solid black;
}
.space{
  padding: 10px;
}
.link{
  text-decoration: none;
  background-color: green;
  border-radius: 7px;
  padding: 10px;
  margin-left: 10px;
}
.btn{
  background-color: red;

}
</style>