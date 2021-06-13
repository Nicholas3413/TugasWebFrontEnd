<template>
  <div>
    <h1>Berikut adalah daftar tugas kita</h1>
    <ul>
        <li v-for="(item,index) in todos" :key="item.id">{{item.deskripsi}}<button @click="hapus(item.id,index)">X</button></li>

    </ul>
    
    <input v-model="myText"/>
    <button @click="tambahkan">Add</button>
    
  </div>
</template>

<script>
import axios from 'axios'
export default{
    data:()=>{
        
        return {
        todos:[]
    ,
        myText:""
        }
    },
    mounted:function(){
        const username=localStorage.getItem("usr")
        const password=localStorage.getItem("pwd")
        axios.get('http://localhost:3000/todo',{headers:{username:username,password:password}})
        .then(result=>{
            this.todos=result.data
        })
    }
    ,
    methods:{
        tambahkan: function(){
            let newItem={deskripsi:this.myText}
            const username=localStorage.getItem("usr")
            const password=localStorage.getItem("pwd")
            axios.post('http://localhost:3000/todo',newItem,{headers:{username:username,password:password}})
            .then(()=>{
                this.todos.push(newItem)
            })
        },
        hapus:function(id,idx){ 
            const username=localStorage.getItem("usr")
            const password=localStorage.getItem("pwd")
            axios.delete(`http://localhost:3000/todo/${id}`,{headers:{username:username,password:password}})
            .then(()=>{
            this.todos.splice(idx,1)})
        }
    }
}
</script>

