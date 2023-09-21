<template>
  <div class="all">
    <div class="nav">
        <div>
            <router-link to="/">Home</router-link>
        </div>
        <div>
            <router-link to="/Add">Add Resturant</router-link>
            <a  @click="Logout" href="#">Logout</a>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name:'Header',
    methods:{
        Logout(){
            localStorage.clear();
            this.$router.push({name:'SignUp'})
        }
    }

}
</script>

<style scoped>

.all{
    text-align: center;
}
.nav{
    background-color: #333;
    overflow: hidden;
    display: flex;
    justify-content: space-between;
}
.nav a{
    float: left;
    color:white;
    padding:14px 16px!important;
    font-size:17px;
    cursor: pointer;
    text-decoration: none;
    margin-right: 5px;
    text-align: center;
}
.nav a:hover{
    background-color: #ddd;
    color: #333;
}
</style>