<template>
    <div>
        <h1 class="bg-info p-2 mb-0">Table with API</h1>
        <table class="table " >
             <thead>
                <tr class="table-primary">
                <th scope="col">id</th>
                <th scope="col">First Name</th>
                <th scope="col">Last Name</th>
                <th scope="col">email</th>
                <th scope="col">Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in list" :key="user.id" class="table-primary">

                    <th scope="row" >{{user.id}}</th>
                    <td >{{user.first_name}}</td>
                    <td >{{user.last_name}}</td>
                    <td >{{user.email}}</td>
                    <td  ><button v-on:click="getuser(userid=user.id)"  class="btn btn-primary px-4 mx-2" data-bs-toggle="modal" data-bs-target="#example_Modal" >Edit</button>
                     <button v-on:click="userid=user.id" type="button" class="btn btn-danger " data-bs-toggle="modal" data-bs-target="#exampleModal">
                        Delete
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>

        <!-- Button trigger modal new user -->
        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#addUserExampleModal">
        ADD NEW USER
        </button>
        <!--add new user form Modal -->
        <div class="modal fade" id="addUserExampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
            <div class="modal-header  ">
                <h5 class="modal-title " id="exampleModalLabel">Enter New User</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <form action="" class="p-5">
                     <div class="form-floating p-2">
                    <input v-model="employees.first_name" type="text" class="form-control" id="floatingPassword" placeholder="First Name">
                    <label for="floatingInput">First name</label>
                    </div> 
                    <div class="form-floating p-2">
                    <input v-model="employees.last_name" type="text" class="form-control" id="floatingPassword" placeholder="Last Name">
                    <label for="floatingInput">Last Name</label>
                    </div>
                    <div class="form-floating p-2">
                    <input v-model="employees.email" type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
                    <label for="floatingInput">Email address</label>
                    </div>              
                </form>
            </div>
            <div class="modal-footer ms-auto me-auto">
                <!-- <button type="button" class="btn btn-danger " data-bs-dismiss="modal">Cancel</button> -->
                <button v-on:click="creatuser()" type="button" class="btn btn-success "  data-bs-dismiss="modal">ADD USER</button>
            </div>
            </div>
        </div>
        </div>


        

        <!-- Modal -->
        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title " id="exampleModalLabel" >You want to delete?</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <h5>The selected user will be deleted permanently</h5>
            </div>
            <div class="modal-footer ms-auto me-auto">
                <button type="button" class="btn btn-primary " data-bs-dismiss="modal">Close</button>
                <button type="button" class="btn btn-danger " v-on:click="deleteuser(userid)" data-bs-dismiss="modal">delete</button>
            </div>
            </div>
        </div>
        </div>

        <!--form Modal -->
        <div class="modal fade" id="example_Modal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
            <div class="modal-header  ">
                <h5 class="modal-title " id="exampleModalLabel">Update User data</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <form action="" class="p-5">
                     <div class="form-floating p-2">
                    <input v-model="employees.first_name" type="text" class="form-control" id="floatingPassword" placeholder="First Name">
                    <label for="floatingInput">First name</label>
                    </div> 
                    <div class="form-floating p-2">
                    <input v-model="employees.last_name" type="text" class="form-control" id="floatingPassword" placeholder="Last Name">
                    <label for="floatingInput">Last Name</label>
                    </div>
                    <div class="form-floating p-2">
                    <input v-model="employees.email"  type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
                    <label for="floatingInput">Email address</label>
                    </div>              
                </form>
            </div>
            <div class="modal-footer ms-auto me-auto">
                <button type="button" class="btn btn-primary " data-bs-dismiss="modal">Close</button>
                <button v-on:click="updateuser(userid)" type="button" class="btn btn-primary "  data-bs-dismiss="modal">update</button>
            </div>
            </div>
        </div>
        </div>

        
    </div>
</template>

<script>
import Vue from 'vue'  
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios, axios)

export default {
    name:'tableApi',
    data(){
        return {
            
            list:{
                first_name:"",
                last_name:"",
                email:""
            },
            userid:null,
            employees:{
                first_name:"",
                last_name:"",
                email:""
            }
        }
    },
    
    methods:{
        getusers(){
             Vue.axios.get('http://localhost:3000/users').then(result=>{
            this.list=result.data
            console.warn(result.data)
            })

        },
        deleteuser(id){
            Vue.axios.delete('http://localhost:3000/users/' + id).then(result=>{
            console.warn(result)
            this.getusers()
            })

        },
        getuser(id){
            Vue.axios.get('http://localhost:3000/users/' + id).then(result=>{
            console.warn(result)
            this.employees=result.data
            })
        },
        async updateuser(id)
        {
            // const axios = require('axios');
            await axios.put('http://localhost:3000/users/'+id, {
            first_name: this.employees.first_name,
            last_name: this.employees.last_name,
            email: this.employees.email
           });

            this.getusers()

            this.employees.first_name=null;
            this.employees.last_name=null;
            this.employees.email=null;
        },
        async creatuser()
         {
            // const axios = require('axios');
            await axios.post('http://localhost:3000/users/', {
            first_name: this.employees.first_name,
            last_name: this.employees.last_name,
            email: this.employees.email
           });

            this.getusers();

            this.employees.first_name=null;
            this.employees.last_name=null;
            this.employees.email=null;
        }  

    },
    mounted()
    {
        this.getusers(); 
    }
}
</script>