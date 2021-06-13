<template>
  <div>
    <h1>Berikut adalah semua pengguna kita</h1>
    <ul>
        <li v-for="(item,index) in users" :key="item.id">nama: {{item.username}}, password: {{item.password}}{{item.passwd}}<button @click="hapus(item.id,index)">X</button></li>

    </ul>
    
    <input v-model="username"/>
    <input v-model="password"/>
    <button @click="tambahkan">Add</button>
    
  </div>
</template>

<script>
import axios from 'axios'
export default{
    data:()=>{
        
        return {
        users:[]
    ,
        username:"",
        password:""
        }
    },
    mounted:function(){
        const username=localStorage.getItem("usr")
        const password=localStorage.getItem("pwd")
        axios.get('http://localhost:3000/user',{headers:{username:username,password:password}})
        .then(result=>{
            this.users=result.data
        })
    }
    ,
    methods:{
        tambahkan: function(){
            const username=localStorage.getItem("usr")
            const passwordx=localStorage.getItem("pwd")
            let newItem={username:this.username,password:this.password}
            axios.post('http://localhost:3000/user',newItem,{headers:{username:username,password:passwordx}})
            .then(()=>{
                this.users.push(newItem)
            })
        },
        hapus:function(id,idx){ 
            const username=localStorage.getItem("usr")   
            const password=localStorage.getItem("pwd")
            axios.delete(`http://localhost:3000/user/${id}`,{headers:{username:username,password:password}})
            .then(()=>{
            this.users.splice(idx,1)})
        }
    }
}
</script>

