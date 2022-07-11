<template>
    <h2>Form Detail:</h2>

     <form class="emform"  @submit.prevent="registerUser" method="post">  
                 <input type="number" placeholder="Enter ID"  v-model="userid"/>

        <input type="text" placeholder="Enter name"  v-model="name" />

        <input type="email"  placeholder="Enter Email"  v-model="email  "/>


         <input type="text" placeholder="Enter status"  v-model="status" /><br>

         
         <p> what is your gender: </p>
          <input type="radio"
           name="Gender" value="HTML">
           <label for="male">Male</label><br>
           <input type="radio" name="Gender">
          <label for="female">Female</label><br>


<button type="submit" >Submit</button>

     </form>
</template>

<script>
 import axios from "axios";

export default {
    name : 'formPage',

    data(){
        return{
            userid : '',
            name:'',
            email:'',
            status:'',
            gender:'',

            users: [],


        };
    },

    methods: {
        registerUser () {
            let user = {
                userid: this.userid,
                name : this.name,
                email : this.email,
                status: this.status,
            };

            if (localStorage.users){
            let lsUsers =  localStorage.users;
            this.users = JSON.parse(lsUsers);
          }

            this.users.push(user);
            localStorage.setItem("users",JSON.stringify(this.users));
            this.userid = '';
            this.name = '';
            this.email = '';
            this.status = '';

            let url = 'https://gorest.co.in/public/v2/users'

            axios.post(`${url}`).then((response) => {
                console.log(response);
            })



            

        },


       // postData(e){
         //   console.warn(this.postData)
           // e.preventDefault();
        //}
    }
}
</script>


<style> 
.emform{
    width: 300px;
    height: 80px;
    padding-left: 1px;
    display:block;
    margin-bottom: 30px;
    margin-left: auto;
    margin-right: auto;
    //border: 250px solid skyblue;
    

}

.emform button {

    width: 320px;
    height: 40px;
    border: 2px solid skyblue;
    color: #fff;
    background-color: red;
    cursor: pointer; }

</style>
